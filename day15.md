## day15

ACL(Access Control List) 접근 제어 항목

ACL 설정 순서

1. 출발지 목적지
2. 허용(permit)/차단(deny)
3. 인바운드(선불), 아웃바운드(후불)

\*rule number `cisco에서는 시퀀스넘버`

acl은 순서 중요함

- EX3) '172.16.11' 서버는 인터넷과 연결된 외부 사용자들에게 서비스가 되지 않도록 하며, 오직 '13.13.10.0/24'
  사용자들에게만 서비스가 가능하도록 한다.

  access-list 10 deny host 172.16.1.1
  access-list 10 permit any
  !
  int s1/0
  ip access-group 10 out
  !

- EX4) 출발지 '13.13.30.0/24'인 패켓만 '13.13.10.0/24' 서브넷으로 접근하는 것을 차단한다.
  나머지 패켓들은 허용한다. R1에서 ACL을 구성하도록 한다.

access-list 10 deny 13.13.30.0 0.0.0.255
access-list 10 permit any 
! 
int s1/0
 ip access-group 10 in
 end
!

```

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
```
