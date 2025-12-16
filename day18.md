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
