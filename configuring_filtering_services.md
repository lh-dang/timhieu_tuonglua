# 📛 CẤU HÌNH CONFIGURING FILTERING SERVICES
## 🔍 1. HTTP (Web thông thường - Port 80)
### tính năng lọc ActiveX và Java Applet 
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
## 🔒 2. HTTPS (Web bảo mật - Port 443)






## 📁 3. FTP (Truyền tệp - Port 21)
## 🧱 4. ActiveX Filtering
## ☕ 5. Java Applet Filtering
## 🖥️ 6. Lọc bằng máy chủ bên ngoài (Websense / SmartFilter)
