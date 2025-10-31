네트워크 : 정보 공유 목적

프로토콜 : 통신 규약

전송하는 데이터가 어떤 데이터인지에 따라 프로토콜이 정해져 있다.

src port → dst port

Eth | IP | TCP | HTTP

Eth | IP | TCP | ssl

## 5. 데이터 전송 관계

- 요청에 의한 응답 관계

Client -(요청)→ Server

Client ←(응답)- Server

## 6. 데이터 전송 방식

- 유니캐스트(Unicast)
  1:1
- 브로드캐스트(Boardcast)
  1:N
  // 라우터는 브로드캐스트를 받아도 넘기지 않음
  // 스위치는 브로드캐스트를 받으면 전부 넘김
- 멀티캐스트 (Multicast)
  1:특정그룹
  실시간 다수 : 브로드 캐스트, 멀티 캐스트
  특정 사용자 : 유니캐스트

# 네트워크 주소체계

## 포트 번호

tcp,udp 헤더 안에 포함된 주소

주소크기 2^16

System Ports (0-1023),

User Ports (1024-49151),

Dynamic and/or Private Ports (49152-65535);

```
http 80
https 443
telnet 23
ssh 22
ftp 21
ftp-data 20
smtp 25
pop3 110
mysql 3306

domain(dns) 53
bootps(dhcp server) 67
bootpc(dhcp client) 68
syslog 514
ntp 123
snmp 161
tftp 69

SA(출발포트)
DA(목적포트)

클라이언트          서버
SA 50001            SA 80
DA 80               DA 50001
요청 ------>  <--------응답
```

```
netstat -n

```

## IP 주소

IPv4 주소 크기 32bit 2^32 = 대략 43억개 정도

IPv6 주소 크기 128bit 2^128 = 무한대 주소 (340간)

- 로컬 환경에서 리모트 환경으로 데이터 전송 담당
  // 내부 네트워크에서는 필요 없음
- 변경이 가능한 논리적인 주소(만들어서/설정해서 사용하는 주소)
- IP 주소 조회 사이트: [https://후이즈검색.한국/main.do](https://xn--c79as89aj0e29b77z.xn--3e0b707e/main.do)
- IP 주소 조회 사이트: [https://mylocation.co.kr](https://mylocation.co.kr/)
- IP 주소 조회 사이트: [http://www.ipconfig.kr](http://www.ipconfig.kr/)
- https://checkip.amazonaws.com/

- ipconfig /all
- ip address // linux

## MAC 주소

- 같은 내부 네트워크 주소에 데이터 전송시 사용
- 변경이 불가능한 물리적인 주소
- 앞에서 부터 24bit OUI-24 // IEEE

**Cisco ⇒ 00:00:0C**

**RElteak ⇒ 00:E0:4C**

A → B

switch router

내부 통신 : ETH

외부 통신 : IP

기본 게이트 웨이 : 첫번째 관문

# TCP

- http 80
- https(ssl) 443
- telnet 23
- ssh 22
- ftp 21
- ftp-data 20
- smtp 25
- pop3 110
- mysql 3306

# UDP

- domain(dns) 53
- bootps(dhcp server) 67
- bootpc(dhcp client) 68
- syslog 514
- ntp 123
- snmp 161
- tftp 69
