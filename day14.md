서브넷 마스크 와일드카드 마스크

255.255.255.0 0.0.0.255
255.255.255.252 0.0.0.3

```
 @R1
conf t
router ospf 1
 router-id 1.1.1.1
 network 13.13.10.0 0.0.0.255 area 0
 network 13.13.12.0 0.0.0.255 area 0
 passive-interface fa0/0
end
!

 @R2
conf t
router ospf 1
 router-id 2.2.2.2
 network 13.13.20.0 0.0.0.255 area 0
 network 13.13.12.0 0.0.0.255 area 0
 network 13.13.23.0 0.0.0.255 area 0
 passive-interface fa0/0
end
!

 @R3
conf t
router ospf 1
 router-id 2.2.2.2
 network 13.13.30.0 0.0.0.255 area 0
 network 13.13.23.0 0.0.0.255 area 0
 passive-interface fa0/0
end
!

```

show run
show ip ospf neighbor
show ip route

- ospf 동기화

1. Down State
2. init State
3. Two Way State
4. Exstart State
5. Exchange State
6. Loagding state
7. Full State

```
conf t

int lo 1
ip address 100.100.1.1 255.255.255.0
int lo 2
ip address 100.100.2.1 255.255.255.0
int lo 3
ip address 100.100.3.1 255.255.255.0

int lo 11
ip address 200.200.1.1 255.255.255.0
int lo 12
ip address 200.200.2.1 255.255.255.0
int lo 13
ip address 200.200.3.1 255.255.255.0

router rip
version 2
no auto-summary
network 100.0.0.0

router ospf 1
network 200.200.0.0 0.0.255.255 area 13
redistribute rip subnets
end
R3#
```

```
@R11
en
conf t
int f0/1
ip ospf priority 255
end

@R12
en
conf t
int fa0/1
ip ospf priority 254
end
```

```
@ R13, R14, R15
en
conf t
int fa0/1
priority 0
end

```


199.172.1.0/24 ~ 199.12.3.0/24, 199.172.8.0/24 ~ 199.172.11.0/24 를 한줄로

199.172.0000000 1.0
199.172.0000001 1.0
