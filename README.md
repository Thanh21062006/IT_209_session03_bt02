# Bài 2: Cấu hình trang lỗi tùy chỉnh (Custom Error Page 404)

### 1. Tạo tệp HTML báo lỗi
Tạo thư mục gốc và file 404:
```bash
sudo mkdir -p /var/www/my-web/html/
sudo nano /var/www/my-web/html/404.html
```
*(Nội dung file `404.html` đã được đính kèm trong repository này).*

### 2. Cấu hình Server Block
Cấu hình Nginx để sử dụng trang lỗi này và chặn truy cập trực tiếp bằng chỉ thị `internal`:
```bash
sudo nano /etc/nginx/sites-available/my-web.conf
```
*(Nội dung cấu hình `my-web.conf` đã được đính kèm trong repository).*

### 3. Kích hoạt và Reload
```bash
sudo ln -s /etc/nginx/sites-available/my-web.conf /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 4. Kiểm tra 
*Lưu ý: Vì thẻ visa của em bị khoá nên không thể tạo droplet để chạy thử nghiệm các lệnh này.*

Lệnh kiểm tra truy cập đường dẫn sai (sẽ trả về 404 kèm nội dung tùy biến):
```bash
curl -I http://<IP_ADDRESS_DROPLET>/invalid-path-demo
```

Lệnh kiểm tra truy cập trực tiếp file lỗi (sẽ bị Nginx chặn vì có `internal`):
```bash
curl -I http://<IP_ADDRESS_DROPLET>/404.html
```
