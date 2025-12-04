Ex1) 출발지 '13.13.10.1'인 PC가, FTP 서버 '172.16.1.1'로 접근하는 트래픽만 차단한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
tcp	13.13.10.1		 any		172.16.1.1		 20,21

access-list 110 deny tcp host 13.13.10.1 host 172.16.1.1 range 20 21
access-list 110 permit ip any any
!
int fa0/0
 ip access-group 110 in


Ex2) 출발지 '13.13.10.1'인 PC가, 웹-서버 '172.16.1.1'로 접근하는 트래픽만 허용한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
tcp 	13.13.10.1		any		172.16.1.1		80,443

access-list 110 permit tcp host 13.13.10.1 host 172.16.1.1 eq 80
access-list 110 permit tcp host 13.13.10.1 host 172.16.1.1 eq 443
!
int fa0/1
 ip access-group 110 out


Ex3) '172.16.1.1'로 전송하는 ICMP를 차단하고 나머지는 허용한다. 단, 서버는 외부로 Ping이 되어야 한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
icmp	any		-		172.16.1.1		-

access-list 110 deny icmp any host 172.16.1.1 echo
access-list 110 permit ip any any
!
int fa0/1
 ip access-group 110 out


Ex4) 출발지 '13.13.10.1'인 PC가, '172.16.1.0/24'로 접근하는 트래픽을 차단하고 나머지는 허용한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
ip	13.13.10.1		-		172.16.1.0/24	-

access-list 110 deny ip host 13.13.10.1 172.16.1.0 0.0.0.255
access-list 110 permit ip any any
!
int fa0/0
 ip access-group 110 in


Ex5) '13.13.10.1' PC가 웹-서버 '172.16.1.1'로부터 다운로드하는 트래픽을 차단하고 나머지는 허용한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
tcp	172.16.1.1		80		13.13.10.1		any

access-list 110 deny tcp host 172.16.1.1 eq 80 host 13.13.10.1
access-list 110 permit ip any any
!
int fa0/1
 ip access-group 110 in


Ex6) '13.13.10.0/24' 네트워크에서 '172.16.1.1'로 접근하는 것을 차단하고 나머지는 허용한다.
프로토콜	출발지 IP 주소	출발지 포트	목적지 IP 주소	목적지 포트
ip	13.13.10.0/24	-		172.16.1.1		-

access-list 110 deny ip 13.13.10.0 0.0.0.255 host 172.16.1.1
access-list 110 permit ip any any
!
int fa0/0
 ip access-group 110 in



Ex7) Extended ACL

① 출발지 '13.13.10.0/24' 서브넷이 FTP 서버 '172.16.1.1'로 접근하는 것을 허용한다.
② 단, 출발지 '13.13.10.1' 호스트가 FTP 서버 '172.16.1.1'로 접근하는 것을 차단한다.
③ 외부 사용자가 인터넷을 통하여 '172.16.1.1' 서버로 Telnet 접속하는 것을 차단한다.
④ 나머지 패켓들은 접근이 가능하도록 허용한다.

access-list 110 deny tcp host 13.13.10.1 host 172.16.1.1 range 20 21
access-list 110 permit tcp 13.13.10.0 0.0.0.255 host 172.16.1.1 range 20 21
access-list 110 deny tcp any host 172.16.1.1 eq 23
access-list 110 permit ip any any
!
int fa0/1
 ip access-group 110 out

Ex8) Extended ACL

 ① 출발지 '13.13.10.1' 호스트가 웹-서버 '172.16.1.1'로 접근하는 것을 차단한다.
 ② 출발지 '13.13.10.0/24' 서브넷이 웹-서버 '172.16.1.1'로 접근하는 것은 허용한다.
 ③ 외부 사용자가 인터넷을 통하여 '172.16.1.1' 서버로 전송하는 ICMP 패켓을 차단한다.
 ④ 단, '172.16.1.1' 서버는 외부로 Ping이 되어야 한다.
 ⑤ 나머지 패켓들은 접근이 가능하도록 허용한다.

access-list 110 deny tcp host 13.13.10.1 host 172.16.1.1 eq 80
access-list 110 permit tcp 13.13.10.0 0.0.0.255 host 172.16.1.1 eq 80
access-list 110 deny icmp any host 172.16.1.1 echo
access-list 110 permit ip any any
!
int fa0/1
 ip access-group 110 out


Ex9) Extended ACL 예제

- 출발지 '13.13.30.0/24'인 패켓이 내부 로컬 네트워크 '13.13.10.1'로 Telnet 접속되는 것을 차단한다.
- 외부에서 내부 서버 '13.13.10.100'으로 Ping 되는 것을 차단하여라. 단, 서버는 외부로 Ping이 되어야 한다.
- 출발지 '13.13.20.0/24'인 패켓이 내부 웹서버 '13.13.10.100'으로 접근하는 것을 차단하여라.
- 나머지 패켓은 허용한다.
- R1에서 ACL을 최대한 간결하게 구성하며, R1 Serial 1/0 인터페이스에 적용하여라.

@ R1
conf t
access-list 110 deny tcp 13.13.30.0 0.0.0.255 host 13.13.10.1 eq 23
access-list 110 deny icmp any host 13.13.10.100 echo
access-list 110 deny tcp 13.13.20.0 0.0.0.255 host 13.13.10.100 eq 80
access-list 110 deny tcp 13.13.20.0 0.0.0.255 host 13.13.10.100 eq 443
access-list 110 permit ip any any
!
int s1/0
 ip access-group 110 in
 end
!


















