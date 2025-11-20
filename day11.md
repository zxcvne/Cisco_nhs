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
 shutdown
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

ICMP 요청 : 8
포트 닫힘 : 3
게이트웨이 reply => 못감 : 1

경로 추가
no ip route 명령어로 가는 경로와 오는 경로를 설정

next hop == 게이트 웨이

- linux
  route add -net 13.13.30.0 netmask 255.255.255.0 gw 13.13.12.2

- window
  route add 13.13.30.0 mask 255.255.255.0 13.13.12.2

- cisco
  ip route 13.13.30.0 255.255.255.0 13.13.12.2

ICMP Echo, Echo-Reply

show no ip route 13.13.30.0

tracert => ttl 1로 요청

<pre>
conf t
no ip route 13.13.30.0 255.255.255.0 13.13.12.2 
no ip route 13.13.20.0 255.255.255.0 13.13.12.2 
no ip route 13.13.23.0 255.255.255.0 13.13.12.2 
end
!
</pre>

conf t
no ip route 13.13.30.0 255.255.255.0 13.13.23.3
no ip route 13.13.10.0 255.255.255.0 13.13.12.1
end
!

<pre>
</pre>

<pre>
conf t
no ip route 13.13.10.0 255.255.255.0 13.13.23.2 
no ip route 13.13.20.0 255.255.255.0 12.12.23.2 
no ip route 13.13.20.0 255.255.255.0 13.13.23.2 
no ip route 13.13.12.0 255.255.255.0 13.13.23.2 
end
!
</pre>

<pre>
@ R1
conf t
ip route 13.13.20.0 255.255.255.0 13.13.12.2
ip route 13.13.23.0 255.255.255.0 13.13.12.2
ip route 13.13.30.0 255.255.255.0 13.13.12.2
end
!
</pre>

<pre>
@ R2
conf t
ip route 13.13.10.0 255.255.255.0 13.13.12.2
ip route 13.13.30.0 255.255.255.0 13.13.23.3
end
!
</pre>

<pre>
@ R3
conf t
ip route 13.13.10.0 255.255.255.0 13.13.12.2
ip route 13.13.12.0 255.255.255.0 13.13.23.2
ip route 13.13.20.0 255.255.255.0 13.13.23.2
end
!
</pre>

show run

show ip route

## 정적 경로란?
관리자가 목적지 네트워크 정보와 넥스트-홉 정보를 파악하여 직접 설정하는 방식.

```
Gateway of last resort is not set
13.0.0.0/24 is subnetted, 5 subnets
C 13.13.10.0 is directly connected, FastEthernet0/0
C 13.13.12.0 is directly connected, Serial1/0
S 13.13.20.0 [1/0] via 13.13.12.2
S 13.13.23.0 [1/0] via 13.13.12.2
S 13.13.30.0 [1/0] via 13.13.12.2
S : Static 경로
13.13.30.0 : 목적지 네트워크
[1/ : 정적 경로의 신뢰도(0~255) //(distance)
/0] : 메트릭 // (metric : 비용)
via : 넥스트-홉 라우터 표시
13.13.12.2 : 넥스트-홉 IP 주소
```

```
@R3
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
```

```
@ R2
conf t
ip route 168.126.63.0 255.255.255.0 13.13.23.3
ip route 198.133.219.0 255.255.255.0 13.13.23.3
ip route 211.241.228.0 255.255.255.0 13.13.23.3
ip route 8.8.8.0 255.255.255.0 13.13.23.3
end
!

R2# show ip route
R2# ping 168.126.63.1
R2# ping 198.133.219.1
R2# ping 211.241.228.1
R2# ping 8.8.8.8
```

```
@ R!
// 모든 IP => default route
ip route 0.0.0.0 0.0.0.0 13.13.12.2
```

## 기본경로

Core 라우터 > Distribution 라우터 > Access 라우터
100 만개 <- 0.0.0.0/0 <- 0.0.0.0/0
0.0.0.0/0 -> Access 라우터

### 롱기스트 매치룰

라우팅 테이블에 경로를 검색할때 가장 먼저 검사하며 패켓의 목적지 IP 주소에 대한 상세 경로를 먼저
사용하는 규칙이다.

### 신뢰도

라우팅 테이블에 등록한 경로의 신뢰도를 의미한다. 범위는 '0~255'까지이며 신뢰도 값이 작은 경로가 라우팅
테이블에 우선적으로 등록된다. 다음은 경로에 대한 신뢰도 기본값이다.

### 메트릭

라우팅 테이블에 등록한 경로의 싞뢰도를 의미한다. 범위는 '0~255'까지이며 신뢰도 값이 작은 경로가 라우팅
테이블에 우선적으로 등록된다. 다음은 경로에 대한 신뢰도 기본값이다.

> 메트릭이 같으면 ?
> 경로가 같으면 둘 다 등록됨(로드 분산)
