# Codex 专业工作总图：iPad / iPhone 使用包

这个目录同时包含两种已经准备好的使用方式：

- **方式 A：局域网直接使用（最快）**：Windows 电脑开着本地小型网页服务器；iPad/iPhone 用 Safari 在同一 Wi‑Fi 下访问。无需上传、无需注册、无需付费。
- **方式 B：PWA 网页应用（长期推荐）**：把本目录发布到 HTTPS 静态网页托管；iPad/iPhone 可在 Safari 中“添加到主屏幕”，以接近 App 的方式打开。首次联网完整加载后，页面核心文件会尝试离线缓存；Windows 上用 Chrome、Edge、Firefox 或 Safari 访问同一个 HTTPS 地址即可使用同样功能。

> 重要：不要把真实 API Key、Cookie、账号密码、客户数据或公司机密写进 HTML、Prompt、README 或 Git 仓库。

---

## 方式 A：Windows 局域网直接使用（已实现）

### 适合什么情况

- 你现在就想在家/办公室的 iPad、iPhone 上查看，且 Windows 电脑也会同时开机。
- 不希望把文件上传到任何外部平台。
- 需要保留完整交互：拖动、双指缩放、点节点、抽屉式右侧栏、术语批注、搜索、复制 Prompt。

### 操作

1. 将整个文件夹解压到 Windows 电脑任意目录。
2. 双击 `启动局域网服务器.bat`。
3. 终端会显示一个地址，例如 `http://192.168.1.35:8080`。
4. 让 iPad/iPhone 与电脑处于**同一个 Wi‑Fi / 同一局域网**。
5. 在 iPad/iPhone 的 **Safari** 输入该地址。
6. 首次运行如出现 Windows 防火墙提示，只勾选或允许 **专用网络**，不要随意开放公用网络。
7. 使用期间保持 Windows 弹出的终端窗口开着；关闭窗口即停止访问。

### iPad / iPhone 手势

- 单指在空白画布拖动：平移导图。
- 双指在空白画布捏合：缩放导图。
- 点节点：打开/更新右侧操作栏。
- 点英文术语：打开中文术语批注。
- 点 Prompt 每行末尾 `ⓘ`：查看该行代码/指令解释。
- 点右上角三段式图标：打开或关闭右侧栏。

### 常见打不开原因

- 两台设备没有连接同一 Wi‑Fi；
- Windows 防火墙拦截了 Python；
- 地址中误用了 IPv6 或错误的 IPv4；
- VPN / 访客网络阻止局域网设备互访；
- 电脑睡眠或终端窗口已关闭。

---

## 方式 B：发布为 PWA 网页应用（已准备文件）

本目录已经含有：

- `index.html`：触控优化版主页面；
- `manifest.webmanifest`：主屏幕网页应用信息；
- `service-worker.js`：核心静态文件离线缓存；
- `icons/`：主屏幕图标；
- `.nojekyll`：让 GitHub Pages 按原样发布静态文件；
- `_headers`：Cloudflare Pages / Netlify 可读取的基础缓存与安全响应头配置。

发布时请上传 `CodexMindMap-iOS-PWA` 目录里面的文件，而不是只上传外层 zip 或外层文件夹。站点根目录应能直接看到 `index.html`、`manifest.webmanifest`、`service-worker.js` 和 `icons/`。

### 以 GitHub Pages 为例（免费，需你自己完成发布）

1. 登录 GitHub，新建一个**不包含敏感内容**的仓库。
2. 把 `CodexMindMap-iOS-PWA` 目录内的全部文件上传到仓库根目录。
3. 打开仓库的 **Settings → Pages**。
4. 在发布来源中选择 `Deploy from a branch`，选择 `main` 分支和根目录 `/`，保存。
5. 等待页面发布后，GitHub 会给出一个 HTTPS 网站地址。
6. 在 iPad/iPhone 的 Safari 打开这个 HTTPS 地址，点分享按钮 → **添加到主屏幕**；若系统提供 **Open as Web App / 作为网页应用打开**，请启用它。
7. 首次打开时保持联网直到页面完整加载；之后核心页面文件可由 Service Worker 缓存。外部链接与日后更新仍需要网络。

### 发布后验收

1. Windows 浏览器打开 HTTPS 地址，确认导图能显示、搜索、点节点、复制 Prompt。
2. iPad/iPhone Safari 打开同一 HTTPS 地址，确认单指拖动、双指缩放、右上角侧栏按钮可用。
3. 在 Safari 点分享按钮 → **添加到主屏幕**，从主屏幕图标重新打开，确认是独立网页应用窗口。
4. 首次完整打开后，断网或开飞行模式再打开一次；如果之前已完成缓存，核心导图应仍能打开。

### Windows 也完整使用

Windows 不需要安装成 PWA 才能使用。直接访问发布后的 HTTPS 地址即可获得同样的搜索、拖动、缩放、节点详情、复制与批注功能。若使用 Chrome 或 Edge，也可以在地址栏右侧或浏览器菜单中选择“安装应用”，以后像桌面应用一样打开。

### 隐私提醒

GitHub Pages 用于静态网页发布。发布前要确认仓库的可见性和你的账户计划是否符合隐私要求。这个导图的 HTML 本身不含账号凭据；但你后续自行加进 Prompt、项目路径、内部策略或密钥时，不应上传到公开页面。

---

## 其他可选方案（尚未实施）

1. **Cloudflare Pages / Netlify / Vercel 等静态托管**：与 GitHub Pages 一样可走 HTTPS + 主屏幕网页应用；适合想绑定自有域名或采用私有代码仓库的场景。
2. **iOS/iPadOS HTML 查看器或代码编辑器 App**：可直接打开本地 HTML，但不同 App 对 JavaScript、复制、LocalStorage、文件权限和全屏体验的支持差异很大，不保证与 Safari 一致，因此不作为主方案。
3. **原生 iOS App 壳（Swift + WKWebView 或 Capacitor）**：最适合长期离线、通知、文件导入、原生分享、MDM 企业部署；但需要 Mac/Xcode，若分发到非自有设备通常还涉及 Apple Developer 账号和签名流程。

---

## 更新导图后如何替换

- 局域网方式：用新版本 `index.html` 覆盖旧文件，再重启 `启动局域网服务器.bat`。
- PWA 方式：替换托管站点的 `index.html`、`service-worker.js`、`manifest.webmanifest` 和图标后重新发布。Safari 可能保留缓存；可关闭网页应用后重新打开，必要时清除该站点的网站数据再访问。每次明显更新后建议同步修改 `service-worker.js` 里的 `CACHE_NAME`，这样旧离线缓存会被自动淘汰。
