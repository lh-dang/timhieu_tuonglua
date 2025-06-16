# TÌM HIỂU - CẤU HÌNH CƠ BẢN TƯỜNG LỬA
![image](https://github.com/user-attachments/assets/2a114cab-4b04-499f-b1cf-747b9427b2df)
---
## 1. Cấu hình ip cho router
### Router R1
```
enable
conf t
hostname R1

interface s0/0
ip address 10.1.1.1 255.255.255.252
no shutdown

interface f0/0
ip address 192.168.2.1 255.255.255.0
no shutdown

exit
```
### Router R2
```
enable
conf t
hostname R2

interface s0/0
ip address 10.1.1.2 255.255.255.252
no shutdown

interface s0/1
ip address 10.10.2.2 255.255.255.252
no shutdown

exit
```
### Router R3
```
enable
conf t
hostname R3

interface s0/0
ip address 10.10.2.1 255.255.255.252
no shutdown

interface f0/0
ip address 172.16.3.1 255.255.255.0
no shutdown

exit

```
## Cấu hình định tuyến tĩnh (Static routing)
### Router R1
```
ip route 172.16.3.0 255.255.255.0 10.1.1.2
```
### Router R2
```
ip route 192.168.2.0 255.255.255.0 10.1.1.1
ip route 172.16.3.0 255.255.255.0 10.10.2.1
```
### Router R3
```
ip route 192.168.2.0 255.255.255.0 10.10.2.2
```
## Cấu hình ip cho pc (kết nối đến gateway)
### PC1
```
ip 192.168.2.2 255.255.255.0 192.168.2.1
```
### PC2
```
ip 192.168.2.3 255.255.255.0 192.168.2.1
```
### PC3
```
ip 172.16.3.2 255.255.255.0 172.16.3.1
```
## show ip route
```
show ip int brief
```
## show ip pc
```
show ip
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
- [Hệ điều hành windows ISO](https://docs.google.com/spreadsheets/d/1o5dmOw8jBCVGxFmlMOsKgoIKULMY7tk-TCSz67IJMc4/pubhtml?fbclid=IwAR2na-Puvgad5JfJz60OWF8xFd9loYG5UcC5Of4BlFnAGRXsk4vwA_B2f5w#)
1) Cài đặt GNS3 và VMWare, và các phần mềm liên quan (option): https://github.com/bowlercbtlabs/Ansible-GNS3-Lab-Setup-part-1-GNS3-VMWare-Workstation-Ubuntu-and-Cisco-IOS-Install-/blob/main/Step%20By%20Step%20Guide.md

2) Cài đặt GNS3 (hướng dẫn thuộc trang chủ): https://docs.gns3.com/docs/getting-started/installation/windows/#introduction

3) Các bài thực hành làm quen với GNS3 (thuộc bản quyền Pacific University): https://cyberlab.pacific.edu/courses/comp177/labs/lab-1-gns3

4) Các mẫu tham khảo cho xây dựng dịch vụ mạng với GNS3: https://gns3.com/marketplace/labs
