# Latchwork · 对闩

双人合作解谜。本地同键盘，或用四位房间口令在两台设备上会合。纯静态页面，可免费部署。

## 怎么玩

- **本地双人**：铜匠 WASD，铜绿 方向键。手机左右各一块触控十字。
- **联网**：一人点「创建房间」，把四位口令（或带 `?room=` 的链接）发给同伴；同伴点「加入房间」。
- **R** 重开本关，**Esc** 回菜单。

规则：铜走铜路、绿走绿路；踏板有人或箱子压着才顶住门闩；对钥格要两人同时站上；各自走进门洞即过关。

## 本地预览

不要直接双击 `index.html`（`file://` 下联机库无法加载）。在本目录执行：

```bash
npx --yes serve .
```

浏览器打开提示的地址（一般是 `http://localhost:3000`）。

## 免费部署成网址

仓库里只有 `index.html`，任意静态托管都可以。部署完成后把网址发给同伴即可，无需注册。

### Cloudflare Pages（推荐）

1. 把 `latchwork` 文件夹推到 GitHub。
2. [dash.cloudflare.com](https://dash.cloudflare.com) → Workers & Pages → Create → Pages → Connect to Git。
3. 构建命令留空，输出目录填 `/`（或把 `index.html` 放在仓库根目录）。
4. 得到 `https://某名.pages.dev`。

### GitHub Pages

`index.html` 已在仓库根目录。先把本地 `main` 推上去，再开 Pages：

```bash
cd ~/Desktop/FGL/latchwork
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

然后：仓库 **Settings → Pages**

1. **Build and deployment → Source** 选 **Deploy from a branch**（不要选 GitHub Actions）。
2. **Branch** 选 `main`，文件夹选 `/ (root)`，点 Save。
3. 等一两分钟，页面顶部会出现 `https://你的用户名.github.io/仓库名/`。

「There are no verified domains」只表示没用自定义域名，可以忽略。Branch 下拉是空的，说明 GitHub 上还没有任何分支——必须先 `git push`。

### Vercel

```bash
npx --yes vercel
```

按提示登录，Framework 选 Other，输出目录留空。

## 联机说明

房间走 PeerJS 的公共信令，浏览器之间 WebRTC 直连。免费、无后端。两边都必须用 **https**（或 localhost）打开同一份页面。公司网或严格 NAT 下偶发连不上，改用本地双人即可。

## 加关

编辑 `index.html` 里的 `LEVELS`。字符含义：

| 符 | 含义 |
|---|---|
| `#` | 墙 |
| `.` | 空地 |
| `1` `2` | 铜匠 / 铜绿出生点 |
| `c` `v` | 仅铜 / 仅绿可走 |
| `a` `b` | 踏板（顶开 `p` / `q`） |
| `p` `q` | 门闩 |
| `&` | 对钥格（两人同时站上，`=` 永久打开） |
| `=` | 对钥门闩 |
| `x` | 可推箱子 |
| `A` `B` | 铜匠 / 铜绿门洞 |
