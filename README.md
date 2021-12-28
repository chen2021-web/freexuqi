# VLESS Heroku

## 概述

用于在 PaaS 上部署 V2Ray WebSocket，在合理使用的程度下，本镜像不会因为大量占用资源而导致封号。

部署完成后，每次启动应用时，运行的 V2Ray 将始终为最新版本。

## 部署

### 步骤

 1. Fork 到自己的 GitHub 账户（用户名以 `example` 为例）
 2. 修改repo名称，注意不要包含 `v2ray` 和 `heroku` 两个关键字
 3. 回到专案首页，点击上面的链接以部署 V2Ray

### 变量

对部署时将以下变量设置为环境变量。

| 变量 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `ID` | `ad806487-2d26-4636-98b6-ab85cc8521f7` | VLESS 用户 ID，用于身份验证，为 UUID 格式 |
| `WSPATH` | `/` | WebSocket 所使用的 HTTP 协议路径 |

## 接入 CloudFlare

通过 CloudFlare Workers 反向代理
注意替换网址hostname
``` node
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="example.com";   
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```

## 注意

 1. **请勿滥用，免费服务少之又少，且用且珍惜**
 2. 若使用域名接入 CloudFlare，请考虑启用 TLS 1.3
 3. AWS 绝大部分 IPv4 地址已被 Twitter 屏蔽


# Paas
目前用到的PaaS平台介绍
以下介绍均为免费版

## [heroku](https://dashboard.heroku.com/)
 * 支持Docker
 * 登录需要翻墙
 * **30min**无人访问休眠
 * 每月**550h**时长

## [Render](https://dashboard.render.com/)
 * 支持Docker
 * 无需翻墙，本身域名接入Cloudflare
 * **15min**无人访问休眠
 * 每月**750h**时长(也就是一个应用可以24*31一直运行)
