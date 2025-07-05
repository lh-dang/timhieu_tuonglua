![image](https://github.com/user-attachments/assets/6f8b9842-399d-46d8-9e4e-b5e55005134e)

---
| Thiết bị | Interface | IP                 | Ghi chú           |
| -------- | --------- | ------------------ | ----------------- |
| **R1**   | s0/0      | 10.1.1.1/30        | Kết nối R2        |
|          | s0/1      | 10.2.2.1/30        | Kết nối R3        |
| **R2**   | s0/0      | 10.1.1.2/30        | Kết nối R1        |
|          | f0/0      | 209.165.200.225/29 | Nối vào ASA       |
| **R3**   | s0/0      | 10.2.2.2/30        | Kết nối R1        |
|          | f0/0      | 172.16.3.1/24      | LAN 172.16.3.0/24 |
| **ASA**  | G0/0      | 209.165.200.226/29 | Outside           |
|          | G0/1      | 192.168.1.1/24     | Inside            |
|          | G0/1.1    | 192.168.2.1/24     | DMZ               |

# CAU HINH DIA CHI IP
### R1
```
ena
conf ter
int s0/0
ip address 10.1.1.1 255.255.255.252
no shut
int s0/1
ip address 10.2.2.2 255.255.255.252
no shut
exit
```
### R2
```
ena
conf ter
int s0/0
ip address 10.1.1.2 255.255.255.252
no shut
int f0/0
ip address 209.165.200.225 255.255.255.248
no shut
exit
```
### R3
```
ena
conf ter
int s0/0
ip address 10.2.2.1 255.255.255.252
no shut
int f0/0
ip address 172.16.3.1 255.255.255.0
no shut
exit
```
### ASAv992-32
```
enable
configure terminal
hostname ASA

! Cấu hình các interface
interface GigabitEthernet0/0
 nameif outside
 security-level 0
 ip address 209.165.200.226 255.255.255.248
 no shutdown

interface GigabitEthernet0/2
 nameif inside
 security-level 100
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 nameif dmz
 security-level 50
 ip address 192.168.2.1 255.255.255.0
 no shutdown

! Bật định tuyến
route outside 0.0.0.0 0.0.0.0 209.165.200.225

! NAT cho inside và DMZ ra outside
! object network obj_any
!  subnet 0.0.0.0 0.0.0.0
!  nat (inside,outside) dynamic interface
!  nat (dmz,outside) dynamic interface

object network INSIDE-NET
 subnet 192.168.1.0 255.255.255.0
 nat (inside,outside) dynamic interface

object network DMZ-NET
 subnet 192.168.2.0 255.255.255.0
 nat (dmz,outside) dynamic interface




! Cho phép truy cập từ inside và dmz ra ngoài
access-list outside_access_in extended permit ip any any
access-group outside_access_in in interface outside

! Cho phép ICMP (ping)
policy-map global_policy
 class inspection_default
  inspect icmp

```
# CAU HINH DINH TUYEN DONG OSPF
### R1
```
conf t
router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0
end
```
### R2
```
conf t
router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 209.165.200.224 0.0.0.7 area 0
end
```
### R3
```
conf t
router ospf 1
network 10.2.2.0 0.0.0.3 area 0
network 172.16.3.0 0.0.0.255 area 0
end
```
### ASAv992-32
```

```
******************************************************
## Nâng cấp cloud để ping ra ngoài
![image](https://github.com/user-attachments/assets/66ab6196-b6d9-450e-8d91-6dc6e7d39276)
- sử dụng card vmnet8 mặc định nat
 - cấu hình gateway của vmnet8 là:192.168.10.1
### R1
```
ena
conf t
int fa0/0
ip address 192.168.242.252 255.255.255.0
no shut
end
conf t
router ospf 1
network 192.168.242.252 0.0.0.255 area 0
end
conf t
ip route 0.0.0.0 0.0.0.0 192.168.242.2
end
```
- Cấu hình thêm ospf để có thể ping từ máy bên trong ra ngoài
```
conf t
router ospf 1
! redistribute static subnets
default-information originate
end
```
### ✅ default-information originate

- Lệnh này yêu cầu router quảng bá route mặc định (0.0.0.0/0) vào OSPF.

- Điều này có nghĩa là: “Muốn ra ngoài Internet à? Cứ gửi cho tao!”

## ⚡ Kiểm tra NAT Service của VMware
- Vào Services.msc trên Windows.
- Tìm và khởi động lại dịch vụ:

> - VMware NAT Service
> - VMware DHCP Service
## KIEM TRA LAI OSPF
```
show ip ospf neighbor
show ip route ospf
```
## LƯU CẤU HÌNH

```
copy running-config startup-config
```
## XÓA CẤU HÌNH
```
write erase
```
hoặc
```
erase startup-config
```
```
reload
```
