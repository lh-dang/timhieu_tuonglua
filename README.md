# 📛FIREWALL
## ĐỀ TÀI: CONFIGURING FILTERING SERVICES
![image](https://github.com/user-attachments/assets/079c3a34-434a-4672-920c-a2ee832fc612)

- [CẤU HÌNH TOPOLOGY TRÊN](https://github.com/lh-dang/timhieu_tuonglua/blob/main/config_topology_tuonglua_bcnhom.md)
- [CONFIGURING FILTERING SERVICES](https://github.com/lh-dang/timhieu_tuonglua/blob/main/configuring_filtering_services.md)
### MÔ TẢ: 
- Cấu hình dịch vụ lọc.

### 🎯 Mục tiêu:
- Lọc (chặn hoặc cho phép)
- Các dịch vụ như Facebook, VPN, HTTP/HTTPS, v.v. thông qua cấu hình trên ASA, pfsense.
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
- các thiết bị ảo của cisco(ASA,pfsense,router,switch...)

### CÁC LOẠI DỊCH VỤ LỌC
#### 🔍 1. HTTP (Web thông thường - Port 80)
- Lọc nội dung web như:
  - ActiveX (filter activex)
    > - Lọc các thẻ được nhúng vào trang web
    > - Lọc đối tượng `<OBJECT>` hoặc `<APPLET>` trong trang HTML.
  - Java Applet (filter java)
    > - Chặn Java applet trong trang web — ngăn mã chạy trên máy client.
    > - ASA sẽ chuyển mã applet thành comment để không chạy.
- URL cụ thể, long URLs (filter url)
- Có thể lọc theo IP nguồn, đích, port.

#### 🔒 2. HTTPS (Web bảo mật - Port 443)
- Lọc URL HTTPS bằng cách kiểm tra phần domain (vì nội dung bị mã hóa).
- ASA không xem được nội dung mã hóa, nhưng vẫn có thể chặn domain theo chính sách.

#### 📁 3. FTP (Truyền tệp - Port 21)
#### 📁 4. Lọc theo chuyên mục trang web (ví dụ: game, mạng xã hội, khiêu dâm…)
#### 📁 5. Lọc Theo nhóm người dùng.
#### 📁 6. Ghi logging, thống kê.
[DEMO PFSENSE](https://github.com/lh-dang/timhieu_tuonglua/blob/main/pfsense_demo.md)
### MỤC TIÊU THÊM
- AAA :  quản lý theo user
- Lưu log lại(ai truy cập, truy cập vào đâu...)
- Hỗ trợ cache(tăng tốc)
### LÝ DO CHỌN ASA THAY VÌ ROUTER CÓ CHỨC NĂNG FIREWALL
- 🔒 **Thiết bị chuyên dụng cho bảo mật** 
- 🧠 **Học tập – luyện thi chứng chỉ**    
- 📈 **Hiệu suất và ổn định**             
- 🧩 **Modular Policy Framework (MPF)**   
- 🔧 **Mô phỏng – GNS3 hỗ trợ tốt ASAv**  
- **Hỗ trợ kỹ thuật lâu dài**                 
- **Bảo mật toàn diện**
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
