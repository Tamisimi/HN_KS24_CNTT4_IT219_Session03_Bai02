# Bài 2 — Custom Error Page 404

## File nộp

- `404.html` — trang lỗi tùy biến
- `my-web.conf` — Server Block có `error_page` + `internal`

## Lệnh trên Droplet

```bash
sudo mkdir -p /var/www/my-web/html
sudo cp 404.html /var/www/my-web/html/
# (có thể thêm index.html nếu chưa có)

sudo cp my-web.conf /etc/nginx/sites-available/my-web.conf
sudo ln -sf /etc/nginx/sites-available/my-web.conf /etc/nginx/sites-enabled/
sudo rm -f /etc/nginx/sites-enabled/default

sudo nginx -t
sudo systemctl reload nginx
```

## Kiểm tra

```bash
curl -I http://<IP>/invalid-path-demo
# → HTTP/1.1 404 + body trang tùy biến khi curl không dùng -I

curl -I http://<IP>/404.html
# → HTTP/1.1 404 (bị chặn bởi internal)
```
