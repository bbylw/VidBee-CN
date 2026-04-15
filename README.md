<div align="left">
  <a href="https://github.com/nexmoe/VidBee">
    <img src="https://github.com/nexmoe/VidBee/raw/main/apps/desktop/build/icon.png" alt="Logo" width="80" height="80">
  </a>

  <h3>VidBee</h3>
  <p>
    <a href="https://github.com/nexmoe/VidBee/stargazers"><img src="https://img.shields.io/github/stars/nexmoe/VidBee?color=ffcb47&labelColor=black&logo=github&label=Stars" /></a>
    <a href="https://github.com/nexmoe/VidBee/graphs/contributors"><img src="https://img.shields.io/github/contributors/nexmoe/VidBee?ogo=github&label=Contributors&labelColor=black" /></a>
    <a href="https://github.com/nexmoe/VidBee/releases"><img src="https://img.shields.io/github/downloads/nexmoe/VidBee/total?color=369eff&labelColor=black&logo=github&label=Downloads" /></a>
    <a href="https://github.com/nexmoe/VidBee/releases/latest"><img src="https://img.shields.io/github/v/release/nexmoe/VidBee?color=369eff&labelColor=black&logo=github&label=Latest%20Release" /></a>
    <a href="https://x.com/intent/follow?screen_name=nexmoex"><img src="https://img.shields.io/badge/Follow-blue?color=1d9bf0&logo=x&labelColor=black" /></a>
    <a href="https://deepwiki.com/nexmoe/VidBee"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
    <br />
    <br />
    <a href="https://github.com/nexmoe/VidBee/releases/latest" target="_blank"><img src="https://github.com/nexmoe/VidBee/raw/main/screenshots/main-interface.png" alt="VidBee Desktop" width="46%"/></a>
    <a href="https://github.com/nexmoe/VidBee/releases/latest" target="_blank"><img src="https://github.com/nexmoe/VidBee/raw/main/screenshots/download-queue.png" alt="VidBee Download Queue" width="46%"/></a>
    <br />
    <br />
  </p>
</div>

> [!NOTE]
> 本项目汉化自 [https://github.com/nexmoe/VidBee](https://github.com/nexmoe/VidBee)

VidBee 是一款现代化的开源视频下载器，支持从全球 1000+ 网站下载视频和音频。基于 Electron 构建，由 yt-dlp 驱动，VidBee 提供简洁直观的界面和强大的功能，满足您的各种下载需求，包括 RSS 自动下载功能，可自动订阅订阅源并在后台自动下载您喜爱的创作者的新视频。

## 👋🏻 快速开始

VidBee 目前正在积极开发中，欢迎反馈遇到的任何 [问题](https://github.com/nexmoe/VidBee/issues)。

[📥 下载 VidBee](https://vidbee.org/download/) | [📚 文档](https://docs.vidbee.org)

> [!IMPORTANT]
>
> **为我们加星**，您将无延迟地收到 GitHub 的所有版本通知 ~

<a href="https://next.ossinsight.io/widgets/official/compose-last-28-days-stats?repo_id=1081230042" target="_blank" style="display: block" align="left">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://next.ossinsight.io/widgets/official/compose-last-28-days-stats/thumbnail.png?repo_id=1081230042&image_size=auto&color_scheme=dark" width="655" height="auto">
    <img alt="Performance Stats of nexmoe/VidBee - Last 28 days" src="https://next.ossinsight.io/widgets/official/compose-last-28-days-stats/thumbnail.png?repo_id=1081230042&image_size=auto&color_scheme=light" width="655" height="auto">
  </picture>
</a>

<!-- Made with [OSS Insight](https://ossinsight.io/) -->

## ✨ 功能特性

### 🌍 全球视频下载支持

通过强大的 yt-dlp 引擎，从全球几乎任何网站下载视频。支持 1000+ 网站，包括 YouTube、TikTok、Instagram、Twitter 等等。

![VidBee 主界面](https://github.com/nexmoe/VidBee/raw/main/screenshots/main-interface.png)

### 🎨 卓越的用户界面体验

现代化、简洁的界面，操作直观。一键暂停/恢复/重试，实时进度跟踪，以及全面的下载队列管理。

![VidBee 下载队列](https://github.com/nexmoe/VidBee/raw/main/screenshots/download-queue.png)

### 📡 RSS 自动下载

自动订阅 RSS 订阅源，并在后台自动下载来自 YouTube、TikTok 等平台您喜爱的创作者的新视频。只需设置一次 RSS 订阅，VidBee 将自动下载新上传的内容，无需手动干预，非常适合跟进您喜爱的频道和创作者。

## 🌐 支持的网站

VidBee 通过 yt-dlp 支持 1000+ 视频和音频平台。如需查看完整支持网站列表，请访问 [https://vidbee.org/supported-sites/](https://vidbee.org/supported-sites/)

## 🧱 Web + API（支持 Docker）

此 monorepo 现在包括：

- `packages/downloader-core`: 共享的 yt-dlp/ffmpeg 下载核心
- `apps/api`: Fastify API 服务器，支持 oRPC 和 SSE 事件
- `apps/web`: 使用 oRPC 的 TanStack Start Web 客户端

本地运行：

```bash
pnpm run start:web
```

此命令将同时启动 `apps/api` 和 `apps/web`。

使用 Docker 运行：

```bash
docker compose up -d --build
```

使用 GitHub Container Registry 镜像运行：

```yaml
services:
  api:
    image: ghcr.io/nexmoe/vidbee-api:latest
    environment:
      VIDBEE_API_HOST: 0.0.0.0
      VIDBEE_API_PORT: 3100
      VIDBEE_DOWNLOAD_DIR: /data/downloads
      VIDBEE_HISTORY_STORE_PATH: /data/vidbee/vidbee.db
    ports:
      - "3100:3100"
    volumes:
      - vidbee-downloads:/data/downloads
      - vidbee-data:/data/vidbee
    restart: unless-stopped

  web:
    image: ghcr.io/nexmoe/vidbee-web:latest
    depends_on:
      - api
    ports:
      - "3000:3000"
    restart: unless-stopped

volumes:
  vidbee-downloads:
  vidbee-data:
```

停止服务：

```bash
docker compose down
```

可选环境变量（通过 `.env`）：

```bash
VIDBEE_API_PORT=3100
VIDBEE_WEB_PORT=3000
VITE_API_URL=http://localhost:3100
```

## 🤝 贡献

欢迎您加入开源社区共同建设。更多详情，请查看：

- Monorepo 应用：
  - `apps/desktop`: VidBee 桌面应用 (Electron)
  - `apps/docs`: 文档站点 (Next.js)
  - `apps/extension`: 浏览器扩展 (WXT)
  - `apps/desktop/docs/glitchtip.md`: GlitchTip 和 `sentry-cli` 桌面监控设置
- [贡献指南](https://github.com/nexmoe/VidBee/blob/main/CONTRIBUTING.md)
- [DeepWiki 文档](https://deepwiki.com/nexmoe/VidBee)

## 📄 许可证

本项目采用 MIT 许可证发布。详见 [`LICENSE`](https://github.com/nexmoe/VidBee/blob/main/LICENSE)。

## 🙏 致谢

- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - 强大的视频下载引擎
- [FFmpeg](https://ffmpeg.org/) - 用于视频和音频处理的多媒体框架
- [Electron](https://www.electronjs.org/) - 构建跨平台桌面应用
- [React](https://react.dev/) - UI 库
- [Vite](https://vitejs.dev/) - 下一代前端工具
- [Tailwind CSS](https://tailwindcss.com/) - 实用优先的 CSS 框架
- [shadcn/ui](https://ui.shadcn.com/) - 精心设计的组件
