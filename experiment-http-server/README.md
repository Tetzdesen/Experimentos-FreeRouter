# Experiment HTTP Server freeRtr

## Topology

### rtr-sw.txt
```
hostname freertr
buggy
…
!
access-list nat4
 sequence 10 deny all obj lloc4 all any all
 sequence 20 deny all any all obj mcast4 all
 sequence 30 deny all obj host4 all obj host4 all
 sequence 40 permit all obj host4 all any all
 exit
!
access-list nat6
 sequence 10 deny all obj lloc6 all any all
 sequence 20 deny all any all obj mcast6 all
 sequence 30 deny all obj host6 all obj host6 all
 sequence 40 permit all obj host6 all any all
 exit
!
prefix-list all4
 sequence 10 permit 0.0.0.0/0 ge 0 le 0
 exit
!
prefix-list all6
 sequence 10 permit ::/0 ge 0 le 0
 exit
!
…
!
vrf definition inet
 exit
!
…
interface ethernet2
 vrf forwarding inet
 ipv4 address 192.168.0.1 255.255.255.0
 ipv6 address 1112::1 ffff:ffff:ffff:ffff::
 no shutdown
 no log-link-change
 exit
!
…
server dhcp4 dhcp-server
 pool 192.168.0.2 192.168.0.100
 gateway 192.168.0.1
 netmask 255.255.255.0
 no dns-server
 domain-name 
 interface ethernet2
 vrf inet
 exit
!
```