## day18

standard VLAN 1~1005
entended VLAN 1006 ~ 4094

vlan 11 fa0/1 - 5, fa0/7 - 10, fa0/15 -19

int range fa0/1 - 5, fa0/7 - 10, fa0/15 -19
switchport mode access
switchport access vlan 11
!

int fa0/1
switchport mode access
switchport access vlan 11
!

int fa0/2
switchport mode access
switchport access vlan 12
!

int fa0/3
switchport mode access
switchport access vlan 11
!

int fa0/4
switchport mode access
switchport access vlan 12
!

int fa0/5
switchport mode access
switchport access vlan 13
!

IEEE 802.1q

conf t
int fa0/24
switchport trunk encapsulation dot1q
switchport mode trunk
end
!

show run
show int trunk

conf t
int fa0/0
switchport trunk encapsulation dot1q
switchport mode trunk
end
!

conf t
int fa0/0
no shotdown
!
int fa0/0.1
encapsulation dot1q 1
ip address 192.168.100.254 255.255.255.0
!
int fa0/0.11
encapsulation dot1q 11
ip address 192.168.11.254
!
int fa0/0.12
encapsulation dot1q 12
ip address 192.168.12.254
!
int fa0/0.13
encapsulation dot1q 13
ip address 192.168.13.254
end
!

trunk -> IP

switchport mode access
switchport access vlan 14
!
