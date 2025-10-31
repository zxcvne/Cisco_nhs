TCP, UDP

IP

ETH

ICMP

ARP

### TCP (Transmission Control protocol)

해더 : 20byte `옵션없을때`

Layer 4계층 프로토콜

다른 시스템과 **통신 수립 연결**을 실시한 후 데이터 **요청** 및 **응답 `연결 지향성`**

3-Way 핸드 쉐이킹

1. 클라이언트 Syn →
2. ← Syn + Ack 서버
3. 클라이언트 Ack →

TCP 연결 성립 : ESTABLISHED

@Control Flag 6bit

- URG : 2^5 32
- ACK : 2^4 16
- PSH : 2^3 8
- RST : 2^2 4
- SYN : 2^1 2
- FIN : 2^0 1

FIN

통신을 종료할 때 사용

4-Way

1. fin →
2. ←ack
3. ← fin
4. ack →

RST : reset

tcp 연결이 해제되거나 포트가 닫혀있음

URG : 긴급 데이터 `우선적`

PSH : push

데이터를 큐에 담아놨다가 한번에 넣음 `버퍼링, 큐잉`

1이면 버퍼링X 큐잉 X

### TCP는 데이터가 크면 분할 해서 보냄 `세그먼트`

```
**흐름 제어 기능

Stop & Wait**

서버            클라이언트
                0
ACK 0
								1
ACK 1
								2
ACK 2

단점 : 세그먼트 딜레이	, ack 양이 많음

**Sliding Window**

서버            클라이언트
                0
ACK 1
								1,2
ACK 3

윈도우 : 자신이 처리할 수 있는 세그먼트 양

	윈도우 : 100                 윈도우 : 80
	서버                         클라이언트

sender             receiver

1
6
11
16
21                <- ack 26

26
31
36
41
46                <- ack 51
```

### 혼잡 제어 기능

Congestion 데이터 정체

ECN

라우터 QoS 정책을 별도로 구성 데이터 품질 저하 방지 `혼잡 회피`

### 오류 검사

수신한 세그먼트에 대한 손성 여부 판단하여, 세그먼트를 드랍하는 기능

### 재전송 기능

시간초과 타이머(RTO) RST

### Window Size

세그먼트 양 // 가변

### TCP를 사용하는 서비스

- HTTP, HTTPS, TELNET, SSH,FTP, FTP-DATA, SMTP, POP3, MYSQL

# UDP (User Data Protocol)

- Layer 4계층
- 8byte
- 비연결 지향성
- 요청,응답 x

```
**Layer4        TCP           UDP**
							통신 연결      X
							흐름 제어      X
							혼잡 제어      X
							재전송 기능    X
							오류 검사      o

****DNS -> TCP연결 -> HTTP 요청

****
```

# IP

- Layer 3계층
- 20byte
- 비연결 지향성
- TTL (Time to live (생존시간))

- IP Precedence : `ip 우선순위`

000

001

010

011

100

101

111

- DSCP : `000000` 2^5
- MTU : default 1500 byte

# Ehternet

- Layer 2계층
- 14byte

```

**TCP/IP 5 LAYER

상위계층       http,dns...

Layer4        TCP           UDP**
							통신 연결      X
							흐름 제어      X
							혼잡 제어      X
							재전송 기능    X
							오류 검사      o
**Layer3                Ip**
					로컬 환경에서 리모트 환경으로
					데이터 전송 담당
**Layer2             Ehternet**
					Ethernet 내부 환경에서 데이터 전송 담당

**Layer1         전기 신호 입출력 담당**

						id   More Fragments  Fragment offset
1500        17   1               0
1500        17   1               1500
1000        17   0               3000

** time to live
ttl이 0이면 패킷 drop `루프 방지 목적`
중간의 라우터 개수를 알 수 있음

윈도우 --------- R1 ------------- R2 ------------- R3 ----------- 리눅스
ttl = 128   ->   ttl = 127    ->  ttl = 126 ->     ttl = 125   -> ttl = 64

윈도우 --------- R1 ------------- R2 ------------- R3 ----------- 리눅스
ttl = 128   <-   ttl = 61    <-  ttl = 62  <-   ttl = 63   <- ttl = 64

윈도우 128
리눅스 64
시스코 255

ping 8.8.8.8
ping www.google.com

디캡 -> 전기신호 ~~~>   ETH | IP | UDP | DNS요청

<~~~ 전기신호 <- 인캡   ETH | IP | UDP | DNS응답

```

ICMP, ARP

와이어샤크 필터
