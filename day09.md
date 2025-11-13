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

커서 가장 앞 뒤 삭제
ctrl + a // 앞
ctrl + e // 뒤
ctrl + x // 삭제

enable : root
running-config 파일 -> RAM 메모리
startup-config 파일 -> NVRAM 메모리 (비휘발성 메모리) 메인보드에서 제공하는 작은 저장공간
copy running-config startup-config
erase startup-config
show run

console idle timeout : 자동 로그아웃

conf t

no ip domain-lookup

- console idle time 수업 실습 환경에서 번거롭기 때문에 제거 실제 환경에서는 보안상 반드시 있어야 함
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
R1(config)# no ip domain-lookup
R1(config)# enable secret cisco
R1(config)#
R1(config)#line con 0
R1(config-line)#exec-timeout 0 0
R1(config-line)#logg syn
R1(config-line)#password ciscocon
R1(config-line)#login
R1(config-line)#
R1(config-line)#line vty 0 4
R1(config-line)#password ciscovty
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