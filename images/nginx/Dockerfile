FROM nginx:1.22-alpine

WORKDIR /var/www/web

ENV NGINX_PORT=8080

COPY ./rootfs/etc/nginx/nginx.conf /etc/nginx/nginx.conf

COPY ./rootfs/etc/nginx/conf.d /etc/nginx/conf.d

COPY ./rootfs/etc/nginx/templates /etc/nginx/templates

COPY ./rootfs/etc/nginx/ssl /etc/nginx/ssl

RUN chown -R nginx:nginx /etc/nginx/conf.d

RUN chmod -R 774 /etc/nginx/conf.d
