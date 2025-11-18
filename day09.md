Cisco Router 2600
Cisco Router 2601
Cisco Router 2602
Cisco Router 2603
...

console : 라우터 접속용 관리 포트

모듈/슬롯/포트
0/0/0

시스코 권한 0~15 0~14 : 일반 사용자 권한 / 15 : 모든 권한
Router> : User Mode // 라우터 초기 접속 프롬프트
Router# : privilge Exec Mode

명령어 축약 가능
enable => en 가능
안되면 : ?

```
Router>e?
enable  exit
```

? : manual

캐리지리턴 라인피드

% : 오류 메시지
Router#show i
% Ambiguous command: "show i" => 축약이 너무 심하다
% Incomplete command. : 명령어 완성 X

커서 가장 앞 뒤 삭제
ctrl + a // 앞
ctrl + e // 뒤
ctrl + x // 삭제

enable : root

running-config 파일 -> RAM 메모리
startup-config 파일 -> NVRAM 메모리 (비휘발성 메모리) 메인보드에서 제공하는 작은 저장공간 // 부팅 마지막에 확인
copy running-config startup-config
erase startup-config
show run

console idle timeout : 자동 로그아웃

conf t => running-config

show startup-config
copy running-config startup-config
erase startup-config : running-config파일은 삭제가 안되지만 startup-confing 파일은 삭제가 가능함

=>

```
Restricted Rights Legend

Use, duplication, or disclosure by the Government is
subject to restrictions as set forth in subparagraph
(c) of the Commercial Computer Software - Restricted
Rights clause at FAR sec. 52.227-19 and subparagraph
(c) (1) (ii) of the Rights in Technical Data and Computer
Software clause at DFARS sec. 252.227-7013.

           cisco Systems, Inc.
           170 West Tasman Drive
           San Jose, California 95134-1706

Cisco Internetwork Operating System Software
IOS (tm) C2600 Software (C2600-I-M), Version 12.2(28), RELEASE SOFTWARE (fc5)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2005 by cisco Systems, Inc.
Compiled Wed 27-Apr-04 19:01 by miwang

Cisco 2621 (MPC860) processor (revision 0x200) with 253952K/8192K bytes of memory
.
Processor board ID JAD05190MTZ (4292891495)
M860 processor: part number 0, mask 49
Bridging software.
X.25 software, Version 3.0.0.
2 FastEthernet/IEEE 802.3 interface(s)
4 Low-speed serial(sync/async) network interface(s)
32K bytes of non-volatile configuration memory.
63488K bytes of ATA CompactFlash (Read/Write)

         --- System Configuration Dialog ---

Continue with configuration dialog? [yes/no]: no
```

no ip domain-lookup

- console idle timeout 수업 실습 환경에서 번거롭기 때문에 제거 실제 환경에서는 보안상 반드시 있어야 함
  exec-timeout 30 30 // 30분 30초
  exec-timeout 0 30 // 30초
  exec-timeout 0 0

logg syn : 라인 동기 // 순서대로 밀림없이

R1(config)#enable secret cisco

해시함수 : 믹서기 => 솔트키 + 해시값 => 사과 + 고추장

```
banner motd ^
### 내용 ###
^
```

```
Router>enable
Router#conf t
Router(config)# hostname R1
R1(config)# no ip domain-lookup : dns요청 X
R1(config)# enable secret cisco : 관리자 비번
R1(config)#
R1(config)#line con 0
R1(config-line)#exec-timeout 0 0 : 자동 로그아웃
R1(config-line)#logg syn : 출력 동기화
R1(config-line)#password ciscocon : 맨 처음 비빌번호
R1(config-line)#login
R1(config-line)#
R1(config-line)#line vty 0 4 // telnet, ssh등 가상포트 [0,1,2,3,4]
R1(config-line)#password ciscovty : vty 비밀번호
R1(config-line)#login
R1(config-line)#end
R1#show run

```

```
R1#conf t
R1(config)#int fa0/0
R1(config-if)#ip address 13.13.10.1 255.255.255.0
R1(config-if)#no shutdown
R1(config-if)#end
R1#show run

R1#show ip int brief
R1#show ip route
R1#ping 13.13.10.2
R1#ping 13.13.10.3
R1#show arp

A,B>ping 13.13.10.1
A>telnet 13.13.10.1	 	->	exit
```


```
en
conf t
hostname R1
enable secret cisco
no ip domain-lookup
line con 0
password ciscocon
login
line vty 0 4
password ciscovty
login
end
show run
```



```
-- memo --
howpassword
```
