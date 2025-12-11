## day17

IP라우팅 망
내부 네트워크 망

- 제안요청서

스위치 : L2계층
라우터 : L3계층

L4, L7 : 로드 분산

A(13.13.10.1) -> C(13.13.10.3)

icmp 요청 메시지
0, 8, 3
arp

### 스위치 기능

Learning : mac 주소 학습
Flooding : 브로드 캐스트
Forwarding : 유니케스트
Aging : 300초
Filtering : 루프방지

Transparent bridging : 관리자가 관리하지 않아도 굴러감

Unknown 유니케스트 : 목적지 모름 Flooding

ip address


@SW1
conf t
int vlan 1
 ip address 13.13.10.101 255.255.255.0
 no shutdown
end

@SW2
conf t
int vlan 1
 ip address 13.13.10.102 255.255.255.0
 no shutdown
end

@SW3
conf t
int vlan 1
 ip address 13.13.10.103 255.255.255.0
 no shutdown
end

lldp


@ R1
en
conf t
hostname R1
no ip domain-lookup
enable secret cisco
!
line con 0
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int fa0/0
 ip address 192.168.100.254 255.255.255.0
 no shutdown
 end
!

@ SW1
en
conf t
hostname SW1
no ip domain-lookup
enable secret cisco
!
line con 0
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int vlan 1
 ip address 192.168.100.1 255.255.255.0
 no shutdown
!
ip default-gateway 192.168.100.254
end
!

@ SW2
en
conf t
hostname SW2
no ip domain-lookup
enable secret cisco
!
line con 0
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int vlan 1
 ip address 192.168.100.2 255.255.255.0
 no shutdown
!
ip default-gateway 192.168.100.254
end
!

@ SW3
en
conf t
hostname SW3
no ip domain-lookup
enable secret cisco
!
line con 0
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int vlan 1
 ip address 192.168.100.3 255.255.255.0
 no shutdown
!
ip default-gateway 192.168.100.254
end
!

SW1# ping 192.168.100.2
SW1# ping 192.168.100.3
SW1# ping 192.168.100.254

SW1# telnet 192.168.100.2
SW1# telnet 192.168.100.3
SW1# telnet 192.168.100.254