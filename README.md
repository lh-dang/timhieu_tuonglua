# 📛FIREWALL
## ĐỀ TÀI: configuring filtering services
![image](https://github.com/user-attachments/assets/d81b749a-c36e-4424-bf19-d15a1c37b14d)

[CẤU HÌNH MẠNG CƠ BẢN CÓ CHỨA ASA](https://github.com/lh-dang/timhieu_tuonglua/blob/main/tuonglua_asa.md)
### MÔ TẢ: 
- Cấu hình dịch vụ lọc.
### 🎯 Mục tiêu:
- Chúng ta muốn lọc (chặn hoặc cho phép) các dịch vụ như Facebook, VPN, HTTP/HTTPS, v.v. thông qua cấu hình trên ASA.
### 🧠 Thành phần chính trong Filtering Services:
| Thành phần            | Vai trò                                                                       |
| --------------------- | ----------------------------------------------------------------------------- |
| **Access-list (ACL)** | Chặn hoặc cho phép các kết nối dựa trên IP, giao thức, port                   |
| **Class-map**         | Xác định loại traffic cần xử lý (ví dụ: HTTP, HTTPS, VPN...)                  |
| **Policy-map**        | Định nghĩa cách xử lý traffic đó (inspect, drop,...)                          |
| **Service-policy**    | Gắn policy vào interface của ASA                                              |
| **DNS inspection**    | Cho phép ASA kiểm tra DNS query để phát hiện domain bị cấm (như facebook.com) |

### PHẦN MỀM SỬ DỤNG
- vm ware
- gns3
- các thiết bị ảo của cisco(ASA,router,switch...)
# TÀI LIỆU THAM KHẢO
- [LINK ALL PHẦN CỨNG ẢO CẦN CHO CẤU HÌNH](https://github.com/hegdepavankumar/Cisco-Images-for-GNS3-and-EVE-NG)
- [lệnh cisco cơ bản](https://quantrimang.com/cong-nghe/tong-hop-lenh-ccna-cisco-162612)
- [Cisco ISO](https://drive.google.com/drive/folders/1AUD4zwBhoVQW0SOOQr_mM-HNnfDVbdPl)
- [ASAv setup](https://www.gns3.com/community/featured/how-to-configure-any-asav-qcow2-)
- [ISO Hệ điều hành windows](https://docs.google.com/spreadsheets/d/1o5dmOw8jBCVGxFmlMOsKgoIKULMY7tk-TCSz67IJMc4/pubhtml?fbclid=IwAR2na-Puvgad5JfJz60OWF8xFd9loYG5UcC5Of4BlFnAGRXsk4vwA_B2f5w#)
- [1) Cài đặt GNS3 và VMWare, và các phần mềm liên quan (option)](https://github.com/bowlercbtlabs/Ansible-GNS3-Lab-Setup-part-1-GNS3-VMWare-Workstation-Ubuntu-and-Cisco-IOS-Install-/blob/main/Step%20By%20Step%20Guide.md)
- [2) Cài đặt GNS3 (hướng dẫn thuộc trang chủ)](https://docs.gns3.com/docs/getting-started/installation/windows/#introduction)
- [3) Các bài thực hành làm quen với GNS3 (thuộc bản quyền Pacific University):](https://cyberlab.pacific.edu/courses/comp177/labs/lab-1-gns3)
- [4) Các mẫu tham khảo cho xây dựng dịch vụ mạng với GNS3](https://gns3.com/marketplace/labs)
