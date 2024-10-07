# 使用 Nginx 做反向代理

为了实现一些基于 Web UI 的高级功能，比如说在转发的消息中显示 QQ 的头像和头衔之类，我们需要将 Q2TG 的 Web 端口暴露到公网。对于有公网 IP 的机器，可以使用 Nginx、Caddy 之类。本文主要讲述如何用 Nginx 做反向代理。

## 配置 Certbot 邮箱和域名

在此之前，你需要确保接下来填写的域名正确解析到当前服务器的 IP。

在 Docker Compose 文件中的 certbot 小节填写你自己的邮箱和域名：

```yaml
    command: certonly --webroot -w /var/www/certbot --force-renewal --email 你的邮箱 -d 你的域名 --agree-tos
```

然后使用以下命令开始启动 Q2TG

```bash
docker compose up -d
```

使用以下命令检查是否成功获取 SSL 证书

```bash
docker compose logs certbot
```

## 配置 Nginx SSL

在确认 Certbot 成功获取 SSL 证书后，取消注释 `nginx.conf` 中的以下代码（即删掉行首的注释符号 `#`），并将`你的域名`替换为你自己的域名。

```nginx
    # server {
    #     listen 443 ssl;
    #     listen [::]:443 ssl;
    #     server_name 你的域名;
    #     ssl_certificate /etc/letsencrypt/live/你的域名/fullchain.pem;
    #     ssl_certificate_key /etc/letsencrypt/live/你的域名/privkey.pem;

    #     location / {
    #         proxy_pass http://q2tg:8080;
    #     }
    # }
```

使用以下命令重启 Nginx 容器

```bash
docker compose restart nginx
```

使用以下命令查看 Nginx 日志

```bash
docker compose logs nginx
```
