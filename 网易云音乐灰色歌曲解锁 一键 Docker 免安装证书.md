# 网易云音乐灰色歌曲解锁 一键 Docker 免安装证书

## 前期准备

- 服务器一台
- 域名一个（提前 A 记录解析到服务器 IP)
- 服务器安装好 Docker

## Docker 命令

假设的解析域名是: `music.test.com` (根据实际情况替换)

运行命令:

`docker run -d --name ubmusic -v $HOME/.caddy:/root/.caddy -p 443:443 -p 8017:8080 -e hs=https://music.test.com kuanfinn/ubmusic`

其中
- `8017` 是代理端口，可自行调整为其他
- `hs=` 后面的域名使用你自己解析好的域名替换

## 使用

Docker 成功运行后，就可以正常使用了。

代理地址为 `服务器 IP:代理端口（8017 或 你自己调整的端口)`

然后在手机端通过代理软件把

> music.163.com
> interface.music.163.com

这两个域名代理到服务器即可

*** 

### 一些说明
- 此 Docker 镜像使用 caddy 自动申请 ssl 证书
- Caddy 的运行会占用服务器 443/80 端口，如果已有其他服务运行在这两个端口，启动会失败
- 默认开启严格模式，只能代理网易云音乐的流量
- 目前只在 iPhone 端做了测试，可用，其他平台没测试