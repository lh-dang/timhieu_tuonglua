![image](https://github.com/user-attachments/assets/ef7eedac-8aff-476f-9a52-a5f723de2ec3)

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

interface GigabitEthernet0/1
 nameif inside
 security-level 100
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/2
 nameif dmz
 security-level 50
 ip address 192.168.2.1 255.255.255.0
 no shutdown

! Bật định tuyến
route outside 0.0.0.0 0.0.0.0 209.165.200.225

! NAT cho inside và DMZ ra outside
object network obj_any
 subnet 0.0.0.0 0.0.0.0
 nat (inside,outside) dynamic interface
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
## KIEM TRA LAI OSPF
```
show ip ospf neighbor
show ip route ospf
```
## LƯU CẤU HÌNH

```
copy running-config startup-config
```

# TÀI LIỆU THAM KHẢO
---
- [link route img,hdh...](https://github.com/hegdepavankumar/Cisco-Images-for-GNS3-and-EVE-NG)
- [lệnh cisco cơ bản:](https://quantrimang.com/cong-nghe/tong-hop-lenh-ccna-cisco-162612)
- [Cisco ISO](https://drive.google.com/drive/folders/1AUD4zwBhoVQW0SOOQr_mM-HNnfDVbdPl)
- [ASAv setup](https://www.gns3.com/community/featured/how-to-configure-any-asav-qcow2-)
- [Hệ điều hành windows ISO](https://docs.google.com/spreadsheets/d/1o5dmOw8jBCVGxFmlMOsKgoIKULMY7tk-TCSz67IJMc4/pubhtml?fbclid=IwAR2na-Puvgad5JfJz60OWF8xFd9loYG5UcC5Of4BlFnAGRXsk4vwA_B2f5w#)
1) Cài đặt GNS3 và VMWare, và các phần mềm liên quan (option): https://github.com/bowlercbtlabs/Ansible-GNS3-Lab-Setup-part-1-GNS3-VMWare-Workstation-Ubuntu-and-Cisco-IOS-Install-/blob/main/Step%20By%20Step%20Guide.md

2) Cài đặt GNS3 (hướng dẫn thuộc trang chủ): https://docs.gns3.com/docs/getting-started/installation/windows/#introduction

3) Các bài thực hành làm quen với GNS3 (thuộc bản quyền Pacific University): https://cyberlab.pacific.edu/courses/comp177/labs/lab-1-gns3

4) Các mẫu tham khảo cho xây dựng dịch vụ mạng với GNS3: https://gns3.com/marketplace/labs
