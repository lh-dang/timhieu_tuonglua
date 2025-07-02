# 📛 CẤU HÌNH CONFIGURING FILTERING SERVICES
🔒 2. HTTPS (Web bảo mật - Port 443)
Lọc URL HTTPS bằng cách kiểm tra phần domain (vì nội dung bị mã hóa).
ASA không xem được nội dung mã hóa, nhưng vẫn có thể chặn domain theo chính sách.
📁 3. FTP (Truyền tệp - Port 21)
Lọc truy cập đến server FTP dựa vào địa chỉ và tên tệp.
Có thể chặn tương tác FTP không rõ ràng (dùng interact-block).
🧱 4. ActiveX Filtering
Lọc đối tượng hoặc trong trang HTML.
Chặn hoặc xóa khỏi mã HTML để trình duyệt không thực thi.
☕ 5. Java Applet Filtering
Chặn Java applet trong trang web — ngăn mã chạy trên máy client.
ASA sẽ chuyển mã applet thành comment để không chạy.
🖥️ 6. Lọc bằng máy chủ bên ngoài (Websense / SmartFilter)
Dịch vụ lọc cao cấp hơn:
HTTP / HTTPS / FTP
Lọc theo chuyên mục trang web (ví dụ: game, mạng xã hội, khiêu dâm…)
Hỗ trợ cache, logging, thống kê.
