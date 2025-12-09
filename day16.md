## Day16

```
ipconfig /all

이더넷 어댑터 이더넷 4:

   연결별 DNS 접미사. . . . :
   설명. . . . . . . . . . . . : Realtek PCIe GbE Family Controller #2
   물리적 주소 . . . . . . . . : 4C-ED-FB-BC-23-03
   DHCP 사용 . . . . . . . . . : 아니요
   자동 구성 사용. . . . . . . : 예
   링크-로컬 IPv6 주소 . . . . : fe80::a96c:25e2:60e1:2616%19(기본 설정)
   IPv4 주소 . . . . . . . . . : 192.168.11.181(기본 설정)
   서브넷 마스크 . . . . . . . : 255.255.255.0
   기본 게이트웨이 . . . . . . : 192.168.11.1
   DHCPv6 IAID . . . . . . . . : 290254331
   DHCPv6 클라이언트 DUID. . . : 00-01-00-01-2A-50-7B-08-88-D7-F6-7F-02-89
   DNS 서버. . . . . . . . . . : 168.126.63.1
   Tcpip를 통한 NetBIOS. . . . : 사용



ncpa.cpl

169.254 : DHCP 할당 안됨

할당에서 제외할 IP 주소 192.168.1.253, 192.168.1.254
할당할 IP 주소 범위 192.168.1.1 ~ 192.168.1.254
서브넷 마스크 255.255.255.0
기본 게이트웨이 192.168.1.254
DNS 서버 192.168.1.253

@ R1
conf t
ip dhcp excluded-address 192.168.1.253 192.168.1.254
!
ip dhcp pool NET192
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.254
 dns-server 192.168.1.253
 end
!

show run
ipconfig /all
show ip dhcp binding
```

```
@ R2
conf t
ip dhcp excluded-address 192.168.1.25
ip dhcp excluded-address 192.168.1.254
!
ip dhcp pool NET192
 network 192.133.219.0 255.255.255.0
 default-router 192.133.219.254
 dns-server 192.133.219.25
 end
!

show run
ipconfig /all
show ip dhcp binding
```

DHCP Realy Agent : 클라이언트 게이트웨이에 설정
브로드케스트 -> 유니케스트 -> 브로드케스트

NAT :
사설 아이피를 사용하는 시스템이 요청에 대한 응답을 받기 위해 사용

목적지 outside
내부망 inside
inside global : 나가는 주소

SNAT : 출발지 변경 NAT
DNAT : 목적지 변경 NAT

inside Local 192.168.1.0/24
inside Global 13.13.12.1

@ R1
conf t
access-list 10 permit 192.168.1.0 0.0.0.255
!
ip nat inside source list 10 interface s1/0 overload
!
int s1/0
ip nat outside
!
int fa0/0
ip nat inside
end
!

overload : port 번호 변환 명령어

A -> 198.133.219.25

SA 1025
DA 80
------------ TCP

ip nat inside source static 192.168.1.253 13.13.12.100

port forwarding

### 시스코 3단계

내부 네트워크
