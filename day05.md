```

tcp : http, https/ssl, telnet, ssh
			ftp..

udp : dns, dhcp s/c ...


TCP/IP 5계층

**상위 계층**

**Layer4      TCP                 UDP**
						통신연결             x
						3-way 핸드쉐이킹     x
						흐름 제어            x
						혼잡 제어            x
						재전송 기능          x
						오류 검사            o

**Layer3               IP**
					로컬 환경에서 리모트 환경으로
					데이터 전송 담당
****				TTL 이용하여 루프방지 및 거리 측정

**Layer2             Ethernet**
							Ethernet  내부 환경에서
							데이터 전송 담당

**Layer1            전기 입출력 담당**
```

## ICMP

- IP 프로토콜을 이용하여 데이터 전송이 가능한지 확인하기 위해서 메세지를 생성하여
- 요청 및 응답을 실시하는 프로토콜이다.

ICMP 메시지 유형

- echo
- echo-reply
-

```
- ping

ICMP Echo                       ICMP Echo-Reply
--------------------- ICMP  --------------------- ICMP
SA 192.168.1.1              SA 192.168.1.200
DA 192.168.1.200            DA 192.168.1.1
--------------------- IP    --------------------- IP

168.126.63.1 // kt dns서버 ip

-tracert
```

## arp

- -d, -a

```
TCP,UDP,IP,Ethernet
ICMP, ARP
```

# 와이어샤크 필터

```
tcp.srcport == 1980
tcp.dstport == 80
tcp.seq == 0
tcp.ack == 1
tcp.flags.syn == 1                          tcp.flags.syn == 0x02
tcp.flags.syn == 1 && tcp.flags.ack == 1    tcp.flags.syn == 0x12
tcp.flags.ack == 1                          tcp.flags.syn == 0x10

udp.srcport ==
udp.dstport ==

ip.src
ip.dst
ip.ttl

eth.src
eth.dst

URG ACK PSH RST SYN FIN
2^5 2^4 2^3 2^2 2^1 2^0

0   0   0   0   1   0    0x02
0   1   0   0   1   0    0x12
0   1   0   0   0   0    0x10

```
