# Webpress Local Server

- [Webpress Local Server](#webpress-local-server)
  - [Cài đặt](#cài-đặt)


## Cài đặt

**Cài đặt Docker**

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

**Clone repository**

```
git clone https://github.com/webpress-infra/webpress-local-server
```

**Tạo file .env**

```
cp .env.example .env
```

Mở terminal / CMD chạy lệnh `docker compose up -d`

**Khởi chạy website**

- Tạo thư mục `www/website.local`
- Đưa code của project vào thư mục `website.local`
- Trỏ tên miền `website.local` về IP `127.0.0.1`
- Truy cập `http://website.local:8080`

> Có thể sử dụng tên thư mục tuỳ ý, nhưng nếu sử dụng tên thư mục dạng `*.local` thì dùng đc SSL có sẵn

> Cổng mặc định là `NGINX_PUBLIC_PORT=8080` có thể tuy ý đổi cổng này trong file `.env` và chạy lệnh `docker compose up -d --build nginx` để update