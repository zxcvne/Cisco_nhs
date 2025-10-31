## 1. 네트워크(Network)

- 정보 공유를 목적으로 시스템과 시스템을 연결하여 구성한 망
- 전 세계 적으로 물리적으로 연결 되어 있음 `해저 케이블`
- 장점 : 시간단축, 비용절감, 통합 운영 관리 // 클라우드랑 동일
- 단점 : 보안성 취약

## 2. 프로토콜(Protocol)

- 데이터 전송 규약
- TCP, UDP, IP, Etheret

## 3.Encapsulation

Ethernet | IP | TCP | HTTP

14 20 20

헤더 헤더 헤더

src/dst : 출발지/목적지

헤더의 주소가 다르면 버림

스위치 : Ethernet 헤더 목적지 주소 확인

라우터 : IP 헤더 목적지 주소 확인

```

헤더의 데이터 크기는 거의 고정임

// 2081
Ethernet | IP | TCP | telnet
14         20   20

// 363
Ethenet | IP | TCP | ssl
14         20   20

// 55
Ethernet | IP | UDP | dns
14         20   8

// 1359
Ethernet | IP | icmp
14         20

// 9
Ethernet | arp
32
```

## 4. 네트워크 유형

### **1. LAN**

- 스위치, pc 랜-카드, UTP케이블, 무선 AP `utp,stp`
- 프로토콜 : ethernet
- 구축 방식 : 버스 토폴로지, 스타 토폴로지
- 권장 연결 : 스타 토폴로지 + 이중화 구성
- memo
  pc랜-카드 ←→ utp케이블 ←→ 스위치
  Core 계층 - Distribuiton 계층 - Access 계층
  sub switch, main switch
  네트워크 설계 3요소
  - 확장성, 이중성, 가용성
    보안 3요소
  - 기밀성, 무결성, 가용성
    `커넥터 : RJ45, 전화 커넥터 : RJ11`

### 2. WAN

- memo
  ISP (internet service provide) : 인터넷/네트워크 망을 제공 \\ lg,skt,kt
  SI/NI : 기업, 사용자에게 시스템/네트워크 환경을 구축, 관리, 유지보수 제공
  추가 사업 분야 : 보안, 사물인터넷, 인터넷 전화, 영상회의 시스템,CCTV, 가상화,

                              클라우드 서비스

  벤더 : 장비, 운영체제, 소프트워어 개발, 연구, 판매, 기술지원 \\ cisco

- LAN과 LAN을 연결하는 외부 네트워크
- 장비 : 라우터
- 프로토콜 : Ethernet

### 3. Internet

- 전세계적으로 연결된 네트워크 망
- 프로토콜 : TCP/IP
- 해저케이블

### 4. Intranet

- 기업 내부에서 사용하는 네트워크 망
- 용도 : 회사 게시판, 공지사항, 기록 열람 기타 등등
