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
# CẤU HÌNH:
## NAT overload (PAT) từ inside ra outside
> - Che địa chỉ nội bộ:

<img width="1155" height="605" alt="image" src="https://github.com/user-attachments/assets/e7f89a97-8098-4565-8b53-64ff23350dbf" />

---
<img width="1151" height="454" alt="image" src="https://github.com/user-attachments/assets/d8d84f9b-346a-44c5-bbd7-44fe30bb19b4" />

> - Mặc định pfsense đã chặn truy cập từ ngoài vào inside

## 🔐 LỌC THEO CỔNG
> - Mặc định pfsense sẽ chặn truy cập từ ngoài vào trong lớp mạng
> - Mở cổng từ ngoài vào trong nếu muốn

- **Chặn truy cập web từ trong ra ngoài qua cổng 80(http)**
![image](https://github.com/user-attachments/assets/a4788c33-bbd1-4126-b83b-7af5abc9fee7)

---
![image](https://github.com/user-attachments/assets/ed379600-6fc4-4bbd-9b4f-75d149368611)

## 🔐 LỌC URLs
### 🔐 LỌC ĐỊA CHỈ IP
#### Lọc địa chỉ IP nguồn
#### Lọc địa chỉ IP đíchđích

![image](https://github.com/user-attachments/assets/2b3bed65-d482-4179-8953-e259ac1c8def)

---

![image](https://github.com/user-attachments/assets/e3200e06-87ba-4527-8f44-cdbfdc22a1ca)

---

![image](https://github.com/user-attachments/assets/09b1fe45-4221-4498-a5d3-0256da0203af)

---
VD: đã biết địa chỉ ip của ctu.edu.vn hay elearning.ctu.edu.vn và không muốn người dùng truy cập đến đó 

---
### 🔐 LỌC THEO TÊN MIỀN

![image](https://github.com/user-attachments/assets/cbacc185-73e7-419d-bff4-2f2b6f6e9357)


### 🔐 LỌC TỔ HỢP CÁC KÝ TỰ TRÊN URL:
<img width="1280" height="973" alt="image" src="https://github.com/user-attachments/assets/b166f211-6657-43d2-88dc-9dc4fe4adfa5" />

---
<img width="1161" height="434" alt="image" src="https://github.com/user-attachments/assets/897def8e-fa5e-488b-aa25-309e3e4e1bb6" />

- **ex: http://example.com/casino** 
---

- **Không thể lọc url của https:// bởi vì toàn bộ nội dung trong https:// đã bị mã hóa**
- **Ví Dụ:**
```
https://www.casino.com/vn/xxx.html
```
- **Trình duyệt sẽ:**
- Mã hóa toàn bộ phần /vn/xxx.html và nội dung request
- Proxy (như Squid hoặc pfSense) chỉ thấy hostname www.casino.com, không thấy đường dẫn /vn/xxx.html
- ➡️ Vì vậy, regex như .*/xxx.* sẽ không hoạt động
## 🔐 LỌC THEO NHÓM NGƯỜI DÙNG
![image](https://github.com/user-attachments/assets/658a3336-8406-45d1-b93b-b51536496c20)

## 🔍 GHI LOG, THỐNG KÊ
- ghi log ten mien: 
> - Status > System Logs

# NGOÀI RA:
## LỌC NỘI DUNG TRONG HTTP:
### LỌC ACTIVE X
### LỌC JAVA
### LỌC NỘI DUNG
## CẤU HÌNH AAA NẾU CÓ THỜI GIAN:

# NOTEs
- **Sử dụng extension**
- squid
- squidGuard
- pfSense-pkg-pfBlockerNG-devel
- **Lỗi**
- Tắt VPN
- Gatewat phải là nhánh LAN của pfsense
# Others
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
