<img width="793" height="610" alt="image" src="https://github.com/user-attachments/assets/3e2e9323-d359-4088-a6dd-e26373fc2794" />



## CẤU HÌNH ROUTER 1
```
conf t
hostname R1

interface f0/1
  ip address 192.168.60.1 255.255.255.0
  no shutdown

interface s0/0
  ip address 10.0.0.1 255.255.255.252
  no shutdown

interface f1/0
   ip address dhcp
   no shutdown


router ospf 1
 network 192.168.60.0 0.0.0.255 area 0
 network 192.168.11.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
exit
ip route 0.0.0.0 0.0.0.0 192.168.11.2
end
```
- **Cấu hình thêm ospf để có thể ping từ máy bên trong ra ngoài**
```
conf t
router ospf 1
! redistribute static subnets
default-information originate
end
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
end
```
