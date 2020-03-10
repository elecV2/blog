# 一分钟搭建一个免费的V2RAY服务器（ws+tls）

## 准备

- 先登录Github（用于第三方平台-okteto授权登录）

## 开始

- 打开网页：https://cloud.okteto.com
- 点击授权登录。会自动跳转到Github平台，授权一下即可。
- 登录成功后台页面

![okteto后台界面](https://i.loli.net/2020/03/10/X6c1itgRL5P2uwQ.jpg)

- 点击deploy（部署）。如图操作

![部署操作](https://i.loli.net/2020/03/10/ivOHka9XKBpFDVP.jpg)

> 1. 点击container（容器）
  2. 起个名字（随便填入几个英文字符）
  3. Docker镜像。必填：**kuanfinn/caddyandv:oqr**

其他不用管，然后点击右下的deploy按钮，一台V2RAY服务器就部署完成了。

## 使用

部署成功后，会在后台看到一个类似：*https://xxxxx-xxxx.cloud.okteto.net* 的地址，这就是V2RAY服务器的地址。此服务器使用的传输协议是ws+tls，相关参数如下：

> 服务器地址（address）：xxxxx-xxxx.cloud.okteto.net
端口：443

> UUID/密码：fc784596-c17d-46da-bbb4-7d5142b8866a

> WS转发路径（path/obfs-uri）：/elecV2


有了这几个参数，把他们填写到相关软件的对应位置就可以直接使用了。

比如，Quantumult X格式：
vmess=xxxx-xxxxxx.cloud.okteto.net:443, method=aes-128-gcm, password=fc784596-c17d-46da-bbb4-7d5142b8866a, obfs=wss, obfs-uri=/elecV2, fast-open=false, udp-relay=false, tag=EVOKTETO

v2rayN格式：
{"port":"443","tls":"tls","add":"xxxx-xxxxxx.cloud.okteto.net","id":"fc784596-c17d-46da-bbb4-7d5142b8866a","aid":"64","v":"2","host":"xxxx-xxxxxx.cloud.okteto.net","type":"none","path":"/elecV2","net":"ws","ps":"EVOKTETO"}

（实际使用时记得把服务器地址替换成你的。）

如果想通过**vmess://**的链接形式导入或分享给别人，把上面的格式文字，替换里面的服务器地址，然后通过base64编码，得到类似编码字符串：eyJwb3J0IjoiNDQzIiwidGxzIjoidGxzIiwiYWRkIjoieHh4eC14eHh4eHguY2xvdWQub2t0ZXRvLm5ldCIsImlkIjoiZmM3ODQ1OTYtYzE3ZC00NmRhLWJiYjQtN2Q1MTQyYjg4NjZhIiwiYWlkIjoiNjQiLCJ2IjoiMiIsImhvc3QiOiJ4eHh4LXh4eHh4eC5jbG91ZC5va3RldG8ubmV0IiwidHlwZSI6Im5vbmUiLCJwYXRoIjoiL2VsZWNWMiIsIm5ldCI6IndzIiwicHMiOiJFVk9LVEVUTyJ9，把这个字符串加在vmess://后面即可。

# 后（PI）话

- 免费的平台不多，薅羊毛的人多了，它可能就倒了。不少平台已经直接对China进行了限制，希望大家好好珍惜。
- 本教程是为了让大家更快的上手V2ray，然后才能有更大的兴趣去了解v2ray。
- 本人与okteto平台无任何利益相关。
- 他人根据此教程在okteto上从事的任何网络活动与本人无关，风险自负。

作者：[elecV2](https://github.com/elecV2)


