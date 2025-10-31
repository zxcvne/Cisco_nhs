HTTP ⇒ HyperText Transfer Protocol `80`

HTTPS ⇒ Security `443`

telnet `23`

ssh `22`

ftp `21`

ftp-data `20`

smtp ⇒ Simple Mail Transfer protocol `25`

pop3 `110`

www ⇒ 호스트 / [naver.com](http://naver.com) ⇒ 도메인

domain(dns) : 도메인을 받으면 ip번호를 알려줌 `53`

bootps(dhcp server) : 컴퓨터가 여러대 있으면 ip 할당/임대 해줌 `68`

bootpc(dhcp client) : 네트워크 장치에 설정

---

```
PC1(192.168.1.1) -> PC1(192.168.1.11)

SA 192.168.1.1
DA 192.168.1.11
----------------------- IP
SA 0060.7030.6E19
DA 00e0.f954.b5a1
----------------------- ETH

PC1(192.168.1.1) <- PC1(192.168.1.11)

SA 192.168.1.11
DA 192.168.1.1
----------------------- IP
SA 00e0.f954.b5a1
DA 0060.7030.6E19
----------------------- ETH

PC1(192.168.1.1) -> PC2(10.1.1.1)

SA 192.168.1.1
DA 10.1.1.1
----------------------- IP
SA 0060.7030.6E19
DA 0090.2b01.7e2e // 기본 게이트웨이
----------------------- ETH
```
