# 📛FIREWALL
## ĐỀ TÀI: CONFIGURING FILTERING SERVICES
![image](https://github.com/user-attachments/assets/d81b749a-c36e-4424-bf19-d15a1c37b14d)

- [CẤU HÌNH TOPOLOGY TRÊN](https://github.com/lh-dang/timhieu_tuonglua/blob/main/tuonglua_asa.md)
- [CONFIGURING FILTERING SERVICES](https://github.com/lh-dang/timhieu_tuonglua/blob/main/configuring_filtering_services.md)
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

### CÁC LOẠI DỊCH VỤ LỌC
#### 🔍 1. HTTP (Web thông thường - Port 80)
- Lọc nội dung web như:
  - ActiveX (filter activex)
  - Java Applet (filter java)
  - URL cụ thể, long URLs (filter url)
- Có thể lọc theo IP nguồn, đích, subnet, port.
#### 🔒 2. HTTPS (Web bảo mật - Port 443)
- Lọc URL HTTPS bằng cách kiểm tra phần domain (vì nội dung bị mã hóa).
- ASA không xem được nội dung mã hóa, nhưng vẫn có thể chặn domain theo chính sách.
#### 📁 3. FTP (Truyền tệp - Port 21)
- Lọc truy cập đến server FTP dựa vào địa chỉ và tên tệp.
- Có thể chặn tương tác FTP không rõ ràng (dùng interact-block).
#### 🧱 4. ActiveX Filtering
- Lọc đối tượng <OBJECT> hoặc <APPLET> trong trang HTML.
- Chặn hoặc xóa khỏi mã HTML để trình duyệt không thực thi.
#### ☕ 5. Java Applet Filtering
- Chặn Java applet trong trang web — ngăn mã chạy trên máy client.
- ASA sẽ chuyển mã applet thành comment để không chạy.
#### 🖥️ 6. Lọc bằng máy chủ bên ngoài (Websense / SmartFilter)
- Dịch vụ lọc cao cấp hơn:
  - HTTP / HTTPS / FTP
  - Lọc theo chuyên mục trang web (ví dụ: game, mạng xã hội, khiêu dâm…)
  - Hỗ trợ cache, logging, thống kê.

### MỤC TIÊU THÊM
- AAA :  quản lý theo user
- Lưu log lại(ai truy cập, truy cập vào đâu...)
- Hỗ trợ cache(tăng tốc)
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
- [Tài liệu của Cisco (CONFIGURING FILTERING SERVICES)](extension://bfdogplmndidlpjfhoijckpakkdjkkil/pdf/viewer.html?file=https%3A%2F%2Fwww.cisco.com%2Fc%2Fen%2Fus%2Ftd%2Fdocs%2Fsecurity%2Fasa%2Fasa91%2Fconfiguration%2Ffirewall%2Fasa_91_firewall_config%2Fprotect_filter.pdf)
- [LINK ALL PHẦN CỨNG ẢO CẦN CHO CẤU HÌNH](https://github.com/hegdepavankumar/Cisco-Images-for-GNS3-and-EVE-NG)
- [lệnh cisco cơ bản](https://quantrimang.com/cong-nghe/tong-hop-lenh-ccna-cisco-162612)
- [Cisco ISO](https://drive.google.com/drive/folders/1AUD4zwBhoVQW0SOOQr_mM-HNnfDVbdPl)
- [ASAv setup](https://www.gns3.com/community/featured/how-to-configure-any-asav-qcow2-)
- [ISO Hệ điều hành windows](https://docs.google.com/spreadsheets/d/1o5dmOw8jBCVGxFmlMOsKgoIKULMY7tk-TCSz67IJMc4/pubhtml?fbclid=IwAR2na-Puvgad5JfJz60OWF8xFd9loYG5UcC5Of4BlFnAGRXsk4vwA_B2f5w#)
- [1) Cài đặt GNS3 và VMWare, và các phần mềm liên quan (option)](https://github.com/bowlercbtlabs/Ansible-GNS3-Lab-Setup-part-1-GNS3-VMWare-Workstation-Ubuntu-and-Cisco-IOS-Install-/blob/main/Step%20By%20Step%20Guide.md)
- [2) Cài đặt GNS3 (hướng dẫn thuộc trang chủ)](https://docs.gns3.com/docs/getting-started/installation/windows/#introduction)
- [3) Các bài thực hành làm quen với GNS3 (thuộc bản quyền Pacific University):](https://cyberlab.pacific.edu/courses/comp177/labs/lab-1-gns3)
- [4) Các mẫu tham khảo cho xây dựng dịch vụ mạng với GNS3](https://gns3.com/marketplace/labs)
