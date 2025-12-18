## vtp

vlan 동기화

conf t
int vlan 1
ip address 192.168.100.1 255.255.255.0
no shutdown
end
!

conf t
int vlan 1
ip address 192.168.100.2 255.255.255.0
no shutdown
end
!

conf t
int vlan 1
ip address 192.168.100.3 255.255.255.0
no shutdown
end
!

conf t
vtp domain CCNA
vtp password cisco
end

show vtp status
show vtp password
