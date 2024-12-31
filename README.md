# Webpress Local Server

- [Webpress Local Server](#webpress-local-server)
  - [Cài đặt](#cài-đặt)
    - [Cài đặt Docker](#cài-đặt-docker)
    - [Clone repository](#clone-repository)
    - [Tạo file .env](#tạo-file-env)
    - [Khởi chạy website](#khởi-chạy-website)
  - [Sử dụng SSL](#sử-dụng-ssl)


## Cài đặt

### Cài đặt Docker

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

### Clone repository

```
git clone https://github.com/webpress-infra/webpress-local-server
```

### Tạo file .env

```
cp .env.example .env
```

Mở terminal / CMD chạy lệnh `docker compose up -d`

### Khởi chạy website

- Tạo thư mục `www/website.local`
- Đưa code của project vào thư mục `website.local`
- Trỏ tên miền `website.local` về IP `127.0.0.1`
- Truy cập `http://website.local:8080`
- Truy cập link https `https://website.local:4443`

> Có thể sử dụng tên thư mục tuỳ ý, nhưng nếu sử dụng tên thư mục dạng `*.local` thì dùng đc SSL có sẵn

> Cổng mặc định là `NGINX_PUBLIC_PORT=8080` có thể tuy ý đổi cổng này trong file `.env` và chạy lệnh `docker compose up -d --build nginx` để update

> Cổng mặc định https là `NGINX_SSL_PUBLIC_PORT=4443`


## Sử dụng SSL

[https://github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert)

Cài đặt makecert theo hướng dẫn ở trên.

Nếu muốn tạo certificate theo domain tuỳ chỉnh thì làm lần lượt các bước sau

Cài đặt local CA
```
mkcert -install
```

Tạo certificate

> mở thư mục `images/nginx/rootfs/etc/nginx/ssl` và gõ lệnh

```
mkcert example.com "*.example.com" localhost 127.0.0.1 ::1

```
> Thay thế `example.com` bằng tên miền muốn dùng certificate

Update file `images/nginx/rootfs/etc/nginx/templates/default.conf.template`

```
ssl_certificate /etc/nginx/ssl/website.local+5.pem;
ssl_certificate_key /etc/nginx/ssl/website.local+5-key.pem;
```
Thay thế tên 2 file `.pem` bằng 2 file mà makecert vừa tạo ra

Update lại nginx bằng lệnh `docker compose up -d --build nginx`