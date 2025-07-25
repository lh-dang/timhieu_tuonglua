🔧 BƯỚC 1: Cài đặt OpenVPN
Mở Terminal và chạy lệnh sau:
```
sudo apt update
sudo apt install openvpn -y
```

### 🔍 BƯỚC 2: Kiểm tra đã cài đặt chưa

```
openvpn --version
```

### Bước 3

```
[Tải file từ dịch vụ VPN miễn phí (như VPNGate):](https://www.vpngate.net/en/)
```

```
🧭 BƯỚC 2: Tìm máy chủ có hỗ trợ OpenVPN
Kéo xuống phần “Public VPN Relay Servers”

Tìm dòng nào có cột "OpenVPN" hiện chữ "Config file"

Bấm vào dòng “OpenVPN Config file” tương ứng

🧾 BƯỚC 3: Tải file .ovpn
Sau khi nhấn vào "OpenVPN Config file", trang mới sẽ hiện ra:

Nhấn chuột phải vào liên kết "Download .ovpn file"

Chọn “Save Link As…” hoặc “Lưu liên kết thành…”

Lưu file về thư mục Downloads

📌 Tên file thường là kiểu: vpnXXXXXX.ovpn
```


### 📦 BƯỚC 4: Cấu hình VPN (sử dụng file .ovpn)

```
mkdir ~/vpn
cp /path/to/myvpn.ovpn ~/vpn/
```

### ▶️ BƯỚC 5: Kết nối VPN
Chạy lệnh sau để kết nối VPN:

```
sudo openvpn --config ~/vpn/myvpn.ovpn
```

❗ Nếu file cấu hình yêu cầu username/password, OpenVPN sẽ yêu cầu nhập lúc kết nối.

### 🧪 Kiểm tra sau khi kết nối thành công:
Mở terminal mới:

```
curl ifconfig.me
```
