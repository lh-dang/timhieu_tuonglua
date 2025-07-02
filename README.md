# 📛FIREWALL
## ĐỀ TÀI: configuring filtering services
![image](https://github.com/user-attachments/assets/d81b749a-c36e-4424-bf19-d15a1c37b14d)

[CẤU HÌNH TOPOLOGY TRÊN](https://github.com/lh-dang/timhieu_tuonglua/blob/main/tuonglua_asa.md)
### MÔ TẢ: 
- Cấu hình dịch vụ lọc.
### CHỨC NĂNG
| Loại lọc                                 | Mô tả                                                                    |
| ---------------------------------------- | ------------------------------------------------------------------------ |
| **Lọc theo địa chỉ IP**                  | Chặn hoặc cho phép các IP cụ thể (ví dụ: block IP 8.8.8.8).              |
| **Lọc theo port / protocol**             | Chặn port 80, chỉ cho phép SSH (TCP/22), v.v.                            |
| **Lọc theo nội dung (Layer 7)**          | Nhận diện và lọc nội dung HTTP, chặn từ khóa, chặn Facebook, YouTube,... |
| **Lọc ứng dụng (Application Filtering)** | Chặn các ứng dụng như Skype, Torrent, VPN,…                              |
| **Lọc URL (URL Filtering)**              | Chặn truy cập các website theo tên miền (facebook.com, tiktok.com, v.v). |
| **Lọc gói Deep Packet Inspection (DPI)** | Phân tích sâu nội dung gói để phát hiện các mối đe dọa.                  |

### 🎯 Mục tiêu:
- Chúng ta muốn lọc (chặn hoặc cho phép)
- các dịch vụ như Facebook, VPN, HTTP/HTTPS, v.v. thông qua cấu hình trên ASA.
- Chặn truy cập trang web độc hại / không mong muốn.
- Chống rò rỉ dữ liệu.
- Giới hạn quyền truy cập theo nhóm người dùng / thiết bị.
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
### MỤC TIÊU THÊM
- AAA
- Lưu log lại(ai truy cập, truy cập vào đâu...)
### LÝ DO CHỌN ASA THAY VÌ ROUTER CÓ CHỨC NĂNG FIREWALL
| Lý do                                   | Giải thích                                                                                                                                                                       |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🔒 **Thiết bị chuyên dụng cho bảo mật** | ASA là firewall **hardware-based** (hoặc ảo như ASAv), được Cisco thiết kế để xử lý **kiểm soát truy cập**, **VPN**, **NAT**, **IPS**, **Application Layer Filtering** hiệu quả. |
| 🧠 **Học tập – luyện thi chứng chỉ**    | ASA là nội dung thường gặp trong các chứng chỉ như **CCNP Security**, **CCIE**, hoặc trong các mô hình tấn công/phòng thủ mạng.                                                  |
| 📈 **Hiệu suất và ổn định**             | So với tường lửa tích hợp sẵn trong router hoặc hệ điều hành (như Windows Firewall), ASA xử lý tốt hơn trong môi trường nhiều lưu lượng hoặc yêu cầu nghiêm ngặt.                |
| 🧩 **Modular Policy Framework (MPF)**   | ASA có MPF giúp bạn cấu hình lọc nội dung, inspection protocol, chống tấn công layer 7.                                                                                          |
| 🔧 **Mô phỏng – GNS3 hỗ trợ tốt ASAv**  | Bạn có thể dễ dàng mô phỏng ASA trên GNS3 + VMware để luyện tập thực tế như thiết bị thật.                                                                                       |
- HỖ TRỢ KỸ THUẬT LÂU DÀI
- BẢO MẬT TOÀN DIỆN
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
