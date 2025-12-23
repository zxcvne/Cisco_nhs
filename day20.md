교재 : 21-1.IEEE 802.1d STP.pkt

@SW1
conf t
int range fa0/20, fa0/24
switchport trunk encapsulation dot1q
switchport mode trunk
end
!

@SW2
conf t
int range fa0/22, fa0/24
switchport trunk encapsulation dot1q
switchport mode trunk
end
!

@SW3
conf t
int range fa0/20, fa0/22
switchport trunk encapsulation dot1q
switchport mode trunk
end
!

spanning-tree
포트가 하나라도 up되면 준비