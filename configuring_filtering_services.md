# 📛 CẤU HÌNH CONFIGURING FILTERING SERVICES
## 🔍 1. HTTP (Web thông thường - Port 80)
### Tính năng lọc ActiveX và Java Applet
#### Hướng Dẫn:
-  Cấu hình Lọc ActiveX
```
filter activex <port> <local_IP> <local_mask> <foreign_IP> <foreign_mask>
```
-  Cấu hình Lọc Java Applet
```
filter java <port> <local_IP> <local_mask> <foreign_IP> <foreign_mask>
```
Giải thích tham số:
> - port: Cổng HTTP (thường là 80 hoặc http).
> - local_IP/local_mask: IP/mask của máy nội bộ (nguồn).
> - foreign_IP/foreign_mask: IP/mask của máy bên ngoài (đích).
> - 0 0 0 0: Áp dụng cho mọi IP.
VD:
- Chặn ActiveX trên port 80 cho tất cả lưu lượng:
```
filter activex 80 0 0 0 0
```
- Chặn ActiveX chỉ cho mạng nội bộ 192.168.1.0/24:
```
filter activex http 192.168.1.0 255.255.255.0 0 0
```
KIỂM TRA CẤU HÌNH:
```
show running-config | include filter
```
#### NOTE:
> Bị xóa dần, lý do không còn hợp thời
- Người dùng chuyển sang dùng HTTPS không còn có thể đọc và lọc thông tin
- **Nếu muốn test, sử dụng ASA 8.4.2 hoặc thấp hơn**
- Hướng dẫn test:
  - sử dụng trình duyệt mở một trang web có chứa ActiveX và Java Applet
  - Ctrol + U -> sẽ thấy
```
<!-- <object ...> -->
<!-- <applet ...> -->
```
### Theo doi hieu xuat:
```
ciscoasa# show perfmon
```
## 🔒 2. HTTPS (Web bảo mật - Port 443)






## 📁 3. FTP (Truyền tệp - Port 21)
## 🧱 4. ActiveX Filtering
- Mục đích: Chặn các thẻ <OBJECT> hoặc <APPLET> có thể chứa mã độc.
- Cảnh báo: Có thể chặn cả Java applets hoặc hình ảnh/multimedia nhúng trong <object>.
Cấu hình mẫu:
```
ciscoasa(config)# filter activex 80 0 0 0 0
```
## ☕ 5. Java Applet Filtering
## 🖥️ 6. Lọc bằng máy chủ bên ngoài (Websense / SmartFilter)
- Hỗ trợ: Websense, SmartFilter (N2H2).
- Cách hoạt động:
- ASA gửi truy vấn song song đến máy chủ lọc và server gốc.

- Nếu bị từ chối, ASA chặn phản hồi.
- Tùy chọn cấu hình:
- Caching URL
- Lọc long URL (HTTP dài)
- Lọc HTTPS (dựa trên hostname vì mã hóa)
- Lọc FTP
## 📊 7. Giám sát Filtering
- URL đã cho phép/bị từ chối
- Số lượng yêu cầu HTTPS/FTP
- Gói bị chặn do vượt bộ đệm
- Sử dụng cache
