![image](https://github.com/user-attachments/assets/da71e39f-502c-484f-a0e6-66dd95da8201)
## CẤU HÌNH ROUTER 1
```
conf t
hostname R1

interface f0/0
  ip address 192.168.50.1 255.255.255.0
  no shutdown

interface f0/1
  ip address 192.168.60.1 255.255.255.0
  no shutdown

interface s0/0
  ip address 10.0.0.1 255.255.255.252
  clock rate 64000
  no shutdown

interface f1/0
   ip address dhcp
   no shutdown


router ospf 1
 network 192.168.50.0 0.0.0.255 area 0
 network 192.168.60.0 0.0.0.255 area 0
 network 192.168.11.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
ip route 0.0.0.0 0.0.0.0 192.168.11.2
ip access-list standard LAN
  permit 192.168.50.0 0.0.0.255
  permit 192.168.60.0 0.0.0.255
  permit 10.0.0.0 0.0.0.3
  permit 192.168.30.0 0.0.0.255

ip nat inside source list LAN interface f1/0 overload
conf t
interface f0/0
  ip nat inside
interface f0/1
  ip nat inside
interface s0/0
  ip nat inside
interface f1/0
  ip nat outside


```
## CẤU HÌNH ROUTER 2
```
conf t
hostname R2

interface s0/0
  ip address 10.0.0.2 255.255.255.252
  no shutdown

interface f0/0
  ip address 192.168.30.1 255.255.255.0
  no shutdown

conf t
router ospf 1
 network 10.0.0.0 0.0.0.3 area 0
 network 192.168.30.0 0.0.0.255 area 0

```
## CẤU HÌNH ASA
```
conf t
hostname ASA-1

interface g0/0
  nameif outside
  security-level 0
  ip address 192.168.50.2 255.255.255.0
  no shutdown

interface g0/1
  nameif inside
  security-level 100
  ip address 192.168.10.1 255.255.255.0
  no shutdown

interface g0/2
  nameif dmz
  security-level 50
  ip address 192.168.20.1 255.255.255.0
  no shutdown

 route outside 0.0.0.0 0.0.0.0 192.168.50.1

object network obj-inside
  subnet 192.168.10.0 255.255.255.0
  nat (inside,outside) dynamic interface

object network obj-dmz
  subnet 192.168.20.0 255.255.255.0
  nat (dmz,outside) dynamic interface


 access-list outside_access extended permit ip any any
 access-group outside_access in interface outside
```
