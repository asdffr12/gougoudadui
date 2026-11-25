# 狗狗安 · H5 / PWA

「狗狗安」（养狗大队）的浏览器版：UniApp（Vue3）构建出的 H5，静态托管，可安装到桌面/手机主屏。

- 线上地址：https://asdffr12.github.io/gougoudadui/
- 源码项目：`C:\Users\dee\AppData\Roaming\TRAE SOLO CN\ModularData\ai-agent\work-mode-projects\6a8866fa995b7dc38d88d550\gougoudadui`

## 这个版本做了什么

- 用项目里现成的 `dist/build/h5` 产物，把 `index.html` 的绝对路径 `/assets/` 改成相对路径，放到子目录也能跑。
- 增加 `manifest.webmanifest`：独立图标、主题色、`display: standalone`。
- 增加 `sw.js`：网络优先 + 缓存兜底，装完后断网能打开用过的页面。
- 图标来自项目自带的 `brand/logo_512.png`。

## 更新流程

```powershell
cd <源码项目>
npm run build:h5
# 把 dist/build/h5 的内容覆盖到本目录（index.html 要重新改相对路径、补 manifest/ SW 注册）
# sw.js 的 CACHE 版本号 +1
git add . && git commit -m "update" && git push
```

## 边界

- 这是演示数据版：宠物、订单、消息来自前端本地数据；`server/` 和 `cloudflare-worker/` 的后端没有一起部署。
- 真实交易需要登录、支付、地图、审核，这些不在这个静态版里。
- 微信小程序版本仍在原项目 `dist/build/mp-weixin`，与本 H5 无关。
