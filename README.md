# Jacklin 的个人博客

基于 [imsyy/home](https://github.com/imsyy/home) 搭建的个人主页，用于展示个人简介、常用链接、实时时间、天气和一言。

## 本地开发

```bash
pnpm install
pnpm dev
```

浏览器访问 `http://localhost:3000`。

## 构建

```bash
pnpm build
pnpm preview
```

构建产物位于 `dist` 目录，可部署到 GitHub Pages、Vercel、Cloudflare Pages 或任意静态站点服务器。

## 个性化配置

- 站点信息、简介、天气和音乐：`.env`
- 首页网站入口：`src/assets/siteLinks.json`
- 社交链接：`src/assets/socialLinks.json`
- 背景图片：`public/images/background*.jpg`
- 站点图标：`public/images/icon`

首次部署前，请将 `.env` 中的站点域名和 `package.json` 中的 GitHub 地址替换为真实地址。需要天气服务时，请在 `.env` 中填写高德开放平台 Web 服务 Key。

## 开源说明

本项目保留原项目的开源许可证及作者署名。原项目已于 2026 年 3 月 2 日归档，当前模板版本为 `v4.1.4`。
