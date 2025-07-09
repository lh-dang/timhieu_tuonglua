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

### Kích hoạt pfBlockerNG (pfSense-pkg-pfBlockerNG-devel)
- Vào Firewall > pfBlockerNG > Update
- Nhấn Force Update để tải các thành phần cần thiết
- Sau khi tải xong, sang tab General:
> - Enable pfBlockerNG: ✅
> - Keep Settings: ✅
> - Click Save
---
![image](https://github.com/user-attachments/assets/ea3b674d-fee0-40cb-bffa-db234065a9cb)

---
- **DNSBL (DNS Blackhole) giúp chặn domain chứa từ khóa bất kỳ.**
- Vào tab DNSBL
- Bật:
> - Enable DNSBL: ✅
> - Enable TLD: ✅ (Tùy chọn mở rộng)
> - DNSBL Listening Interface: chọn LAN
> - DNSBL IP: chọn 10.10.10.1 (mặc định)
> - Click Save DNSBL settings

---
![image](https://github.com/user-attachments/assets/b5919ec6-76a6-4382-be52-2665e6e0853e)

---
- Vào tab DNSBL > DNSBL Groups
- Nhấn + Add
> - DNSBL Group Name: custom_block
> - Description: Danh sách tự tạo
> - Action: Unbound
> - Click Save
Sau khi tạo xong, bấm vào Custom Domain List để nhập trực tiếp:
```
facebook.com
tiktok.com
casino.com
vpnbook.com
freevpn.org
xvideos.com
```
> - **Nhấn Save, sau đó quay lại tab Update > Run để áp dụng.**
## 🔐 LỌC URLs
### LỌC ĐỊA CHỈ IP

![image](https://github.com/user-attachments/assets/2b3bed65-d482-4179-8953-e259ac1c8def)

---

![image](https://github.com/user-attachments/assets/e3200e06-87ba-4527-8f44-cdbfdc22a1ca)

---

![image](https://github.com/user-attachments/assets/09b1fe45-4221-4498-a5d3-0256da0203af)

---
VD: đã biết địa chỉ ip của ctu.edu.vn hay elearning.ctu.edu.vn và không muốn người dùng truy cập đến đó 

---
### LỌC THEO TÊN MIỀN

![image](https://github.com/user-attachments/assets/cbacc185-73e7-419d-bff4-2f2b6f6e9357)


### LỌC CÁC KÝ TỰ NGHI NGỜ CHỨA MÃ ĐỘC
![image](https://github.com/user-attachments/assets/1dab7e8f-3587-4f9f-8c8d-d43ae9fc92ff)
- **🔹 Gán rule để chặn**
- Tab Common ACL
- Trong Target Rules List:
- block_keywords: chọn deny
- Nhấn Save

- **🔹 Apply cấu hình**
- Tab General
- Nhấn Apply
- Có thể nhấn “Clear Log / Apply” ở trên cùng nếu cần
#### TEST 
- https://casino.com
## 🔐 LỌC THEO NHÓM NGƯỜI DÙNG
## 🔍 GHI LOG, THỐNG KÊ
## 🔐 LỌC THEO CỔNG
![image](https://github.com/user-attachments/assets/a4788c33-bbd1-4126-b83b-7af5abc9fee7)

---
![image](https://github.com/user-attachments/assets/ed379600-6fc4-4bbd-9b4f-75d149368611)

# NOTEs
- **Sử dụng extension**
- squid
- squidGuard
- pfSense-pkg-pfBlockerNG-devel
- **Lỗi**
- Tắt VPN
- Gatewat phải là nhánh LAN của pfsense
