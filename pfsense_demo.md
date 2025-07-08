# CẤU HÌNH DỊCH VỤ LỌC VỚI PFSENSE
## 🔐 Bảo mật mạng
> pfSense hoạt động như một tường lửa (firewall) kiểm soát và bảo vệ lưu lượng mạng ra vào.
## 🌐 Ưu Điểm:
- Nhẹ
- Có giao diện(GUI)
- pfSense có thể thay thế router
  - NAT (Network Address Translation)
  - DHCP (Phân phối IP)
  - DNS (Tên miền)
  - Routing (Định tuyến)
- Các tính năng nổi bật
  - 🔥 Firewall
  - 🌐 VPN
  - 🚫 Lọc nội dung
  - 📊 Giám sát mạng
  - 🧩 Plugin
## Cấu Hình
### Kích hoạt Squid Proxy
- Vào Services > Squid Proxy Server.
- Tab General:
> - Enable Squid: ✅
> - Proxy Interface: chọn LAN
> - Allow users on interface: ✅
> - Transparent HTTP proxy: ✅ (để không cần cấu hình proxy thủ công trên máy client)
> - Nhấn Save.
---
![image](https://github.com/user-attachments/assets/d0da2e3c-deee-425f-9426-b244e4ebfa8b)

---
![image](https://github.com/user-attachments/assets/7caecafd-9121-4ab6-a082-a5f82158a0d9)

--- 
### Kích hoạt SquidGuard
- Vào Services > SquidGuard Proxy Filter.
- Tab General:
> - Enable: ✅
> - Target rules: chọn action mặc định là deny nếu không khớp.
> - Nhấn Save.
---
![image](https://github.com/user-attachments/assets/667000b6-58f7-4073-b99e-8a7a0901b2f7)

---
![image](https://github.com/user-attachments/assets/a383f988-5901-4527-b89e-a0a4fdf5b69a)

## 🔐 LỌC URLs
### LỌC THEO TÊN MIỀN
![image](https://github.com/user-attachments/assets/2b3bed65-d482-4179-8953-e259ac1c8def)

---

![image](https://github.com/user-attachments/assets/e3200e06-87ba-4527-8f44-cdbfdc22a1ca)

---
### LỌC ĐỊA CHỈ IP
### LỌC CÁC KÝ TỰ NGHI NGỜ CHỨA MÃ ĐỘC
## 🔐 LỌC THEO NHÓM NGƯỜI DÙNG
## 🔍 GHI LOG, THỐNG KÊ
## 🔐 LỌC THEO CỔNG
# NOTEs
- **Sử dụng extension**
- squid
- squidGuard
