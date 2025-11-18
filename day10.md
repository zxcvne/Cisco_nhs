conf t
int s1/0
ip address 13.13.12.1 255.255.255.0
no shutdown
end

show run
show ip int brief
show ip route
ping
