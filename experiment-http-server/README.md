# Experiment HTTP Server freeRtr

## Topology

### rtr-hw.txt
```
hwid xxx
proc ifc1.sh /rtr/rawInt.bin eth0 20002 127.0.0.1 20001 127.0.0.1
int eth1 stat eth 08:00:27:8d:c0:4d 127.0.0.1 20001 127.0.0.1 20002
proc ifc2.sh /rtr/rawInt.bin eth1 20012 127.0.0.1 20011 127.0.0.1
int eth2 stat eth 08:00:27:5d:e6:12 127.0.0.1 20011 127.0.0.1 20012
proc tap20001.sh /rtr/tapInt.bin tap20001 20022 127.0.0.1 20021 127.0.0.1 10.255.255.1/24 10.255.255.254
int eth20001 eth - 127.0.0.1 20021 127.0.0.1 20022
tcp2vrf 8082 inet 8087
```
### rtr-sw.txt
```
!
server http webserver
 port 8087
 interface ethernet1
 vrf inet
 exit
!
```