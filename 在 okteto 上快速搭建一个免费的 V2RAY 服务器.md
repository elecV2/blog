## 在 okteto 上快速搭建一个免费的 V2RAY 服务器

1、使用 Github 授权登录 https://cloud.okteto.com
2、Deploy，选择Deploy from Github，填写 URL: https://github.com/elecV2/v2ku
3、然后点击Deploy，服务器搭建完成。

搭建的V2RAY 服务器默认使用 WS+TLS 模式，相关参数如下：
```
地址：见Endpoints
端口：443
UUID/密码：7c0aceec-0c5d-4468-bf61-e22c65e9abbb
WS转发路径（path/obfs-uri）：/elecV2
```

转换成 QuanX 格式为：
vmess=xxxx-xxxxxx.cloud.okteto.net:443, method=aes-128-gcm, password=7c0aceec-0c5d-4468-bf61-e22c65e9abbb, obfs=wss, obfs-uri=/elecV2, fast-open=false, udp-relay=false, tag=ELECV2OK

TG频道：[@elecV2](https://t.me/elecV2)

okteto 上的部署只需要 k8s.yaml 文件，其他文件用于 Docker 的生成。

## 关于修改密码和路径

如果懂 k8s 和 v2ray，可以添加 command -config https://config远程地址，通过加载远程 config 的方式，修改相应内容。

如果不是很了解这些，可以通过下面的方式。

fork 项目 (https://github.com/elecV2/v2ku)，然后修改 config.json 中的路径和密码，然后在 hub.docker.com 上生成自己的 v2ray Docker image，最后将 k8s.yaml 文件中的 containers image 修改为自己的 image 名称，再部署到 OKTETO 上。