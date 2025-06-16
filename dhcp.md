## ⚙️ III. CẤU HÌNH DHCP TRÊN ROUTER CISCO
```Router> enable
Router# configure terminal
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.99
Router(config)# ip dhcp pool LAN
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# lease 1 0 0
Router(dhcp-config)# exit
```
## 💡 Giải thích:
ip dhcp excluded-address	```Không cấp IP từ 1.1 đến 1.99```
ip dhcp pool LAN	```Tạo pool DHCP tên là LAN```
network	```Chỉ định dải mạng cấp phát```
default-router	```Đặt địa chỉ gateway cho máy nhận DHCP```
dns-server	```Cấp DNS (ở đây là Google DNS)```
lease 1 0 0	```Cấp phát IP trong 1 ngày```
## Xin cap phat dhcp tren pc
```
pc1: dhcp
```
