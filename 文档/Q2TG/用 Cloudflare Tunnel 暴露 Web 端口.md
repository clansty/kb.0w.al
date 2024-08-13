# 用 Cloudflare Tunnel 暴露 Web 端口

为了实现一些基于 Web UI 的高级功能，比如说在转发的消息中显示 QQ 的头像和头衔之类，我们需要将 Q2TG 的 Web 端口暴露到公网。对于有公网 IP 的机器，可以使用 Nginx、Caddy 之类，对于内网中的机器，可以使用 Cloudflare Tunnel 将 Web 端口暴露到公网。

# 配置 Cloudflare Tunnel

0. 需要拥有一个自己的域名，托管于Cloudflare，托管教程省略

1. 进入到 [tunnel](https://one.dash.cloudflare.com/) 页面，选择测边栏 network 标签下的 tunnels 选项

![image](./image/config_cloudflare_tunnel_01.png)

2. 选择 Cloudflared 作为接入方式

![image](./image/config_cloudflare_tunnel_02.png)

3. 给这个配置起一个名字

![image](./image/config_cloudflare_tunnel_03.png)

4. 选择 docker 作为运行方式，复制命令到运行 q2tg 的机器上运行，等待下方显示出你的机器

![image](./image/config_cloudflare_tunnel_04.png)

5. 配置你的域名前缀，并且填写你 q2tg 的 webui 地址

![image](./image/config_cloudflare_tunnel_05.png)

6. 验证连通性，并且将复制的域名填入你的 q2tg ENV 中

![image](./image/config_cloudflare_tunnel_06.png)
