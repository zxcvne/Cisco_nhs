ip routing

<pre>
@ R1

en
conf t
hostname R1
enable secret cisco
no ip domain-lookup
!
line con 0
 password ciscocon
 login
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int fa0/0
 ip address 13.13.10.1 255.255.255.0
 no shutdown
!
int s1/0
 ip address 13.13.12.1 255.255.255.0
 no shutdown
 end
! 
마지막 느낌표 하기
</pre>

<pre>
@ R2

en
conf t
hostname R2
enable secret cisco
no ip domain-lookup
!
line con 0
 password ciscocon
 login
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int fa0/0
 ip address 13.13.20.1 255.255.255.0
 no shutdown
!
int s1/0
 ip address 13.13.23.2 255.255.255.0
 no shutdown
int s1/1
 ip address 13.13.12.2 255.255.255.0
 no shutdown
 end
! 
</pre>

<pre>
@ R3

en
conf t
hostname R3
enable secret cisco
no ip domain-lookup
!
line con 0
 password ciscocon
 login
 exec-timeout 0 0
 logg syn
!
line vty 0 4
 password ciscovty
 login
!
int fa0/0
 ip address 13.13.30.1 255.255.255.0
 no shutdown
!
int s1/1
 ip address 13.13.23.3 255.255.255.0
 no shutdown
 end
! 
</pre>

PreConfig
가상화 작업 -> 도커 /쿠버네티스
클라우드 -> AWS, MS Azure, CGP

ICMP 요청 8
실패 3 => 코드번호 1
