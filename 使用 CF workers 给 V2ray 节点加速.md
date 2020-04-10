假如你已经按之前教程 [搭建了一个免费的 v2ray 服务器](https://elecv2.github.io/一分钟搭建一个免费的V2RAY服务器（ws+tls）)，但觉得速度有些慢，可以尝试使用 cloudflare 的 workers 给节点 CDN 加速一下。虽然有不少人感觉 cloudflare 的 CDN 就是一个减速器，但从个人体验来说，加速效果还是很明显的，尤其是在使用一些国外小水管服务器的时候。

## 操作步骤

登录 cloudflare，新建一个 worker。

![workers.png](https://i.loli.net/2020/03/23/rB5qfHFiRIb73jd.png)

然后把下面的 JS 代码粘贴到对应区域，记得把 **url.hostname** 替换成想要加速的 v2ray 节点域名（只是域名，不要添加前面的 http 和后面的路径那些）。

``` js
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="xxxx-elecv2.cloud.okteto.net";
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```

然后点击保存，会看到一个 workers 的服务器域名，类似： **https://xxxxxx.xxxx.workers.dev** ，这就是我们所需要的 CDN 域名。

## 使用方法

把客户端中被加速节点的信息复制一份，然后把域名换成 workers 服务器的域名（xxxxxx.xxxx.workers.dev）即可。

例如，原来被加速的节点信息为：
> vmess=xxxx-xxxxxx.cloud.okteto.net:443, method=aes-128-gcm, password=fc784596-c17d-46da-bbb4-7d5142b8866a, obfs=wss, obfs-uri=/elecV2, fast-open=false, udp-relay=false, tag=EVOKTETO

那么可以直接复制上面的信息，修改一下域名，然后添加一个新的节点：
> vmess=xxxxxx.xxxx.workers.dev:443, method=aes-128-gcm, password=fc784596-c17d-46da-bbb4-7d5142b8866a, obfs=wss, obfs-uri=/elecV2, fast-open=false, udp-relay=false, tag=EVOKTETO-CDN

这个操作完全不影响原来节点的使用，只是多了一个 CDN 的加速节点，很值得尝试一下。