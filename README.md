# 📛FIREWALL
## ĐỀ TÀI: CONFIGURING FILTERING SERVICES
<img width="804" height="601" alt="image" src="https://github.com/user-attachments/assets/320fc6ab-881c-479f-8648-e7b0a6db76cc" />


- [CẤU HÌNH TOPOLOGY TRÊN](https://github.com/lh-dang/timhieu_tuonglua/blob/main/config_topology_tuonglua_bcnhom.md)
### MÔ TẢ: 
- **Cấu hình dịch vụ lọc**
- Lọc gói tin.
- Chặn hoặc cho phép.
- Chặn truy cập trang web độc hại / không mong muốn.
- Giới hạn quyền truy cập theo nhóm người dùng / thiết bị.
### PHẦN MỀM SỬ DỤNG
- vm ware
- gns3
- các thiết bị ảo của cisco(ASA,pfsense,router,switch...)

### CÁC LOẠI DỊCH VỤ LỌC
#### 1. Xác định phạm vi lọc
- **Lọc gói tin (Packet Filtering): Kiểm tra từng gói tin (packet) dựa trên:**
- Địa chỉ IP nguồn/đích
- Port (cổng) (VD: Chỉ mở port 80 cho HTTP, 443 cho HTTPS).
  - `ActiveX (filter activex)`
  - `Java Applet (filter java)`
- Giao thức mạng (TCP, UDP, ICMP, etc.).
- **Lọc ứng dụng (Application Filtering)**
- VD: game, mạng xã hội, khiêu dâm…
#### 2. Thiết lập quy tắc (Rules)
- **Quy tắc cho phép (Allow):**
- VD: Cho vào vùng DMZ với cổng 443
- **Quy tắc chặn (Deny/Block)**
- VD: Chặn tất cả truy cập từ IP độc hại đã biết, Chặn port 21 (FTP) nếu không sử dụng.
- **Lọc Theo nhóm người dùng**
- **Quy tắc NAT (Network Address Translation):**
- VD: Chuyển hướng port hoặc ẩn IP nội bộ.
- **Lọc theo thời gian (Time-based Rules):**
- **VPN Filtering:**
#### 3. Ghi logging, thống kê.

## CẤU HÌNH CONFIGURING FILTERING SERVICES CHI TIẾT

[DEMO PFSENSE](https://github.com/lh-dang/timhieu_tuonglua/blob/main/pfsense_demo.md)
### MỤC TIÊU THÊM
- AAA :  quản lý theo user
- Lưu log lại(ai truy cập, truy cập vào đâu...)
- Hỗ trợ cache(tăng tốc)

### ⚔️ Lý do không chọn Router
- 🔥 Lọc cơ bản lọc theo IP/Port.
- 🧨 Zone-Based Firewall: giới hạn tường lửa lớp 3/4
- 📦 Khả năng lọc ứng dụng (không nhận diện URL, Java, ActiveX): ❌ Không hỗ trợ
- 🌐 Lọc URL theo nội dung: ⚠️ Không có sẵn
- 🧠 Chức năng IPS/IDS: ⚠️ Yếu (cần cài riêng hoặc ISR cao cấp)
- 📶 Hiệu suất xử lý gói tin: 	Tốt nhưng không tối ưu cho security
- 🔌 Mở rộng:	Không
- 📚 Khó học –  cấu hình
- 💡 Ghi log chi tiết, thống kê, báo cáo như firewall chuyên dụng
  
### LÝ DO CHỌN PFSENSE THAY VÌ ASA
| Tiêu chí                    | pfSense (Nguồn mở)                          | Cisco ASA (Thiết bị chuyên dụng)             |
| --------------------------- | ------------------------------------------- | -------------------------------------------- |
| 💰 **Chi phí**              | **Miễn phí** hoàn toàn                      | Cần license, file image khó tìm/giới hạn     |
| 🧠 **Dễ học, dễ dùng**      | Giao diện web GUI trực quan, đơn giản       | Chủ yếu dùng **CLI**, khó với người mới      |
| 📦 **Tính năng mặc định**   | Firewall, NAT, VPN, Captive Portal, IDS/IPS | Firewall mạnh, NAT, VPN, lọc mức ứng dụng    |
| 🔌 **Mở rộng**              | Cài thêm gói: Squid, Snort, pfBlockerNG...  | Khó mở rộng, giới hạn theo bản firmware      |
| 🔧 **Tùy chỉnh & kiểm thử** | Rất linh hoạt, chỉnh sửa theo ý muốn        | Cứng nhắc, phụ thuộc vào chính sách Cisco    |
| 🧪 **Thí nghiệm, lab**      | Lý tưởng cho lab linh hoạt, mô phỏng mạng   | Khó tích hợp nếu thiếu license hoặc ASAv lỗi |
| 📚 **Tài liệu cộng đồng**   | Cộng đồng mạnh, nhiều hướng dẫn chi tiết    | Tài liệu chính quy từ Cisco, ít cộng đồng mở |
| 🌐 **Lọc nội dung web**     | Dùng Squid + squidGuard, mạnh mẽ, tùy chỉnh | Cần license + máy chủ Websense hoặc SFR      |
| 💻 **Tài nguyên hệ thống**  | Nhẹ, chạy mượt trên QEMU hoặc VirtualBox    | ASAv nặng, yêu cầu nhiều RAM/CPU             |

---
# TÀI LIỆU THAM KHẢO
- [Tài liệu của Cisco (CONFIGURING FILTERING SERVICES)](extension://bfdogplmndidlpjfhoijckpakkdjkkil/pdf/viewer.htmlfile=https%3A%2F%2Fwww.cisco.com%2Fc%2Fen%2Fus%2Ftd%2Fdocs%2Fsecurity%2Fasa%2Fasa91%2Fconfiguration%2Ffirewall%2Fasa_91_firewall_config%2Fprotect_filter.pdf)
- [LINK ALL PHẦN CỨNG ẢO CẦN CHO CẤU HÌNH](https://github.com/hegdepavankumar/Cisco-Images-for-GNS3-and-EVE-NG)
- [lệnh cisco cơ bản](https://quantrimang.com/cong-nghe/tong-hop-lenh-ccna-cisco-162612)
- [Cisco ISO](https://drive.google.com/drive/folders/1AUD4zwBhoVQW0SOOQr_mM-HNnfDVbdPl)
- [ASAv setup](https://www.gns3.com/community/featured/how-to-configure-any-asav-qcow2-)
- [ISO Hệ điều hành windows](https://docs.google.com/spreadsheets/d/1o5dmOw8jBCVGxFmlMOsKgoIKULMY7tk-TCSz67IJMc4/pubhtml?fbclid=IwAR2na-Puvgad5JfJz60OWF8xFd9loYG5UcC5Of4BlFnAGRXsk4vwA_B2f5w#)
- [Cài đặt GNS3 và VMWare, và các phần mềm liên quan (option)](https://github.com/bowlercbtlabs/Ansible-GNS3-Lab-Setup-part-1-GNS3-VMWare-Workstation-Ubuntu-and-Cisco-IOS-Install-/blob/main/Step%20By%20Step%20Guide.md)
- [Cài đặt GNS3 (hướng dẫn thuộc trang chủ)](https://docs.gns3.com/docs/getting-started/installation/windows/#introduction)
- [Các bài thực hành làm quen với GNS3 (thuộc bản quyền Pacific University):](https://cyberlab.pacific.edu/courses/comp177/labs/lab-1-gns3)
- [Các mẫu tham khảo cho xây dựng dịch vụ mạng với GNS3](https://gns3.com/marketplace/labs)
