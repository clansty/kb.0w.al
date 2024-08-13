# 使用 NapCat 作为 QQ 客户端的场合

使用无头 NTQQ NapCat 接入。并非所有功能都支持，只有在 icqq 不可用的时候才使用 NapCat 接入

https://napneko.github.io/zh-CN

请在 napcat 容器的 ACCOUNT 变量中填写你要登录的 QQ 号，并且将 mac 改成一个唯一的虚拟 mac 地址（方便 QQ 保存你的登录信息）

然后通过访问主机 IP:6099/webui 登录 QQ，登录的 token 在 docker compose logs 里会显示。完成之后再开始 Q2TG 的配置。会自动使用设置好的 NapCat WebSocket 连接

## 将原先使用 icqq 的实例转换为 NapCat

首先删除 docker compose 里面的 sign 容器（如果有）同时清理 depends_on。然后参考这里的 docker compose yaml，添加 NapCat 容器，并且将 volume 挂载好

登录好 NapCat 后，进入 Q2TG 的数据库，在 QqBot 表中将对应的 bot 的 type 改为 napcat，并且在 wsUrl 里填写 `ws://napcat:3001` 这样的 url

## 为第二个实例使用 NapCat

首先参考 docker compose 的 yaml，创建一份新的 NapCat 容器

```yaml
volumes:
  napcat-data2:
  napcat-config2:

services:
  napcat2:
    image: mlikiowa/napcat-docker:latest
    environment:
      - ACCOUNT=要登录的 QQ 号
      - WS_ENABLE=true
    ports:
      - 6098:6099
    mac_address: 02:42:12:34:56:78 # 请修改为一个固定的 MAC 地址，但是不要和其他容器或你的主机重复
    restart: unless-stopped
    volumes:
      - napcat-data2:/root/.config/QQ
      - napcat-config2:/usr/src/app/napcat/config
      - cache:/root/.config/QQ/NapCat/temp

  q2tg:
    depends_on:
      - napcat2
```

需要注意，cache 这个 volume（路径为 /root/.config/QQ/NapCat/temp）应该是所有容器共享的，因为发送和接受文件 / 图片之类的会用到。如果你自己用其他的方法启动 NapCat 的话，也要让这个目录保持共享

然后，在初始化让你输入 QQ 号的时候，输入 `ws://napcat2:3001` 这样的 url
