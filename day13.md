## day13

- 균등 로드 분산 (로드 밸런싱)

MTU : 1500

@ R1

conf t
router eigrp 100
no auto-summary
network 13.0.0.0
passive-interface fa0/0
end

show run
show ip eigrp neighbor
show ip route

@ R1
ping 13.13.20.1
ping 13.13.30.1

@ R2
ping 13.13.10.1
ping 13.13.30.1

@ R3
ping 13.13.10.1
ping 13.13.20.1

@ R3

conf t
int lo 1
ip address 168.126.63.1 255.255.255.0
!
int lo 2
ip address 198.133.219.1 255.255.255.0
!
int lo 3
ip address 211.241.228.1 255.255.255.0
!
int lo 4
ip address 8.8.8.8 255.255.255.0
end
!

show run
show ip brief
show ip route

FD 메트릭
AD 메트릭

@ R2
en
conf t
int s1/0
bandwidth 2048
end
!

@ R3

en
conf t
int s1/0
bandwidth 2048
!
int s1/1
bandwidth 2048
end

@ R4

en
conf t
int s1/1
bandwidth 2048
end
!

- Bandwidth = 10 ^ 10 / 목적지까지 가장 작은 Bandwidth(bps)
- Delay = 목적지까지 합산

@ R1
conf t
int lo 1
ip address 128.28.8.1 255.255.255.0
!
int lo 2
ip address 128.28.9.1 255.255.255.0
!
int lo 3
ip address 128.28.10.1 255.255.255.0
!
int lo 4
ip address 128.28.11.1 255.255.255.0
!
int lo 5
ip address 128.28.12.1 255.255.255.0
!

@ R3
conf t
int lo 1
ip address 100.100.1.1 255.255.255.0
!
int lo 2
ip address 100.100.1.1 255.255.255.0
!
int lo 3
ip address 100.100.1.1 255.255.255.0
!
router rip
version 2
no auto-summary
network 100.0.0.0
!
