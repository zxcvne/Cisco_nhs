conf t
int s1/0
ip address 13.13.12.1 255.255.255.0
no shutdown
end

show run
show ip int brief
show ip route
ping

Loopback : 가상인터페이스 생성 // 테스트 목적, 관리 목적

기본설정 연습

목요일 : 정적경로
