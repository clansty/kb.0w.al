# 使用 icqq 作为 QQ 客户端的场合

这是和 v2、v3 相同的登录方式。如果 icqq 可以用的话，就不要切换到 NapCat

## 更换签名版本

yaml 里面以下两行定义了签名服务器版本

```yaml
    environment:
      # 需要与下方的 SIGN_VER 同步
      # 配置请参考 https://hub.docker.com/r/xzhouqd/qsign
      - BASE_PATH=/srv/qsign/qsign/txlib/8.9.71
```

```yaml
      - SIGN_VER=8.9.71 # 与上方 sign 容器的配置同步
```

如果旧版本的签名还能用，就不要切换到新版本。这两个地方的版本要同步。关于这个签名服务器支持的版本，请参考 https://hub.docker.com/r/xzhouqd/qsign

## 使用其他的签名服务器

如果你有其他可以用的、icqq 兼容的签名服务器，你可以删除 sign 容器，并且把 q2tg 的环境变量里面的 SIGN_API 和 SIGN_VER 改成你的签名服务器地址和版本

```diff
- sign:
-   image: xzhouqd/qsign:core-1.1.9
-   restart: unless-stopped
-   environment:
-     # 需要与下方的 SIGN_VER 同步
-     # 配置请参考 https://hub.docker.com/r/xzhouqd/qsign
-     - BASE_PATH=/srv/qsign/qsign/txlib/8.9.71

  q2tg:
    image: ghcr.io/clansty/q2tg:rainbowcat
    restart: unless-stopped
    depends_on:
      - postgres
-     - sign
```

```yaml
      - SIGN_API=http://sign:8080/sign?key=114514
      - SIGN_VER=8.9.71 # 与上方 sign 容器的配置同步
```

如果你需要使用多实例功能，请确保你的签名服务器可以支持多个用户同时使用。如果不支持，请删除这两个变量，这样每次设置的时候会让你自己填写签名服务器的地址和版本
