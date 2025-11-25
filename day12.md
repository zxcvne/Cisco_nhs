## 동적 경로

@ 라우팅 프로토콜

- RIPv1, RIPv2, IGRP, EIGRP, OSPF, ISIS, BGPv4

- RIPv1, RIPv2, IGRP, EIGRP : 요즘 안씀
- OSPF, BGPv4 : 현재 많이 씀

`kt : ISIS, BGPv4`

---

### 1. 라우팅 업데이트 동작 및 관리

#### 1) Distance Vector

- RIPv1, RIPv2, IGRP, EIGRP

#### 2) Link-State

- OSPF, ISIS

라우팅 업데이트

---

### 2. 서브넷 처리 방식

#### 1) Classful Routing Protocol

- RIPv1, IGRP
- Ex) 13.13.10.0/24 <- 13.0.0.0/8

#### 2) Classless Routing Protocol

- Ex) 13.13.10.0/24 <- 13.13.10.0/24

---

### 3. 자동 클래스풀 요약을 실시하는 라우팅 프로토콜

- RIPv2, EIGRP, BGPv4
- 설정할 때 'no auto-summary' 명령을 이용하여 자동 요약 해지

### 4. 사용하는 지역

#### 1) IGP

- RIPv1, RIPv2, IGRP, EIGRP, OSPF, ISIS
- AS 안에 네트워크 망을 구축하기 위해서 라우팅 업데이트 할때 사용한다.
- 라우팅 업데이트 속도가 빠르며, 변경된 사항을 빠르게 적용한다.
- 대신, 많은 양의 라우팅 업데이트를 실시하면 장비 부하가 발생되는 문재가 있다.

#### 2) EGP

- BGPv4
- AS와 AS간(ISP와 ISP간)에 라우팅 업데이트할 때 사용한다.
- 많은 양의 라우팅 업데이트를 실시해도 장비 부하가 발생되지 않는다.
- 대신, 라우팅 업데이트 속도가 느리며, 변경된 사항이 느리게 적용되거나 명령어를 이용하여
  직접 적용해야 한다.

---

<pre>
@R1
conf t 
router rip
network 13.0.0.0
end
!

show run
show ip route
</pre>
