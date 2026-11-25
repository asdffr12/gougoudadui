# 狗狗安 · H5 / PWA

「狗狗安」（养狗大队）的浏览器版：UniApp（Vue3）构建出的 H5，静态托管在 GitHub Pages，可安装到桌面/手机主屏。

- 线上地址：https://asdffr12.github.io/gougoudadui/
- 仓库：https://github.com/asdffr12/gougoudadui
- 源码项目：`C:\Users\dee\AppData\Roaming\TRAE SOLO CN\ModularData\ai-agent\work-mode-projects\6a8866fa995b7dc38d88d550\gougoudadui`

## 这个版本做了什么

- 按子目录部署重新构建：Vite `base: '/gougoudadui/'`，`manifest.json` 的 `h5.router.base` 同为 `/gougoudadui/`，解决此前 `/assets/` 绝对路径导致的 `uni-async-error`（“连接服务器超时”）。
- 增加 `.nojekyll`：GitHub Pages 默认会忽略 `_plugin-vue_export-helper...js` 这类下划线开头的文件，关掉 Jekyll 后才能正常加载。
- 增加 `manifest.webmanifest`：独立图标、主题色 `#FF5A8A`、`display: standalone`。
- 增加 `sw.js`：网络优先 + 缓存兜底，版本 `gougoudadui-v3`。
- 图标来自项目自带 `brand/logo_512.png`，缩放为 512 / 192 / 180 三种尺寸。

## 已验证

- 线上首页、附近、订单、我的四个主页面均可打开；宠物图片、TabBar、页面分块正常加载。
- `GET https://gougou.wangzhonghao.me/api/pets` 在页面内可用，订单页已读到线上 4 条订单。
- `manifest.webmanifest`、`sw.js`、`static/pets/*.jpg` 线上均返回 200。

## 更新流程

```powershell
cd <源码项目>
# 临时把 vite.config.js 的 base 改为 '/gougoudadui/'，
# 并在 src/manifest.json 增加 h5.router.base = '/gougoudadui/'
npm run build:h5
# 把 dist/build/h5 的内容覆盖到本目录
# 重新补 manifest / apple-touch-icon / SW 注册（build 会覆盖 index.html）
# sw.js 的 CACHE 版本号 +1
git add -A && git -c http.proxy= commit -m "update" && git -c http.proxy= push
```

## 边界

- 前端静态 H5 已上线；`cloudflare-worker/`、D1、R2、AI 等后端服务不在本仓库内。
- 浏览类接口（宠物、订单、消息、用户）已验证可读；登录、支付、下单写入等流程尚未逐一验证，真实交易前需补后端与支付接入。
- 微信小程序版本在源码项目 `dist/build/mp-weixin`，与本 H5 无关。
