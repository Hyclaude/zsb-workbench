---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: ca5cc7d1ca9271dc1e8d9f879b19f0e3_9b229adfdd7b11f1997d52540024e231
    ReservedCode1: 5YZHZY5ALzTsl8IY3B0wqX4IszTk/cUXFEuF+We9kLKcp2HulDDfYCxTCcxBPZC3vl2rSO3v8HsN2IJaJoZfsNGzAkjBN4x66ul74COzXw80CB2CuNrxGOcbjENjr3g8ZBiwP1NLxAADrmOeY5TNrJpP7+Hd3YBU8WjsF+LF2UZMG1LgnWvI4wGqgdA=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: ca5cc7d1ca9271dc1e8d9f879b19f0e3_9b229adfdd7b11f1997d52540024e231
    ReservedCode2: 5YZHZY5ALzTsl8IY3B0wqX4IszTk/cUXFEuF+We9kLKcp2HulDDfYCxTCcxBPZC3vl2rSO3v8HsN2IJaJoZfsNGzAkjBN4x66ul74COzXw80CB2CuNrxGOcbjENjr3g8ZBiwP1NLxAADrmOeY5TNrJpP7+Hd3YBU8WjsF+LF2UZMG1LgnWvI4wGqgdA=
---

# 备考工作台 · 平板部署说明（DEPLOY）

> 版本：v6 · 2026-11-11
> 适用设备：安卓平板 / 手机 / Windows 电脑浏览器
> 特点：纯静态、零后端、零构建、双击即可打开；公式（KaTeX）与字体已全部本地化，**断网可用**。

---

## 一、包里有什么

```
zsb-workbench/
├─ index.html            工作台主页（入口卡片、各功能页，单文件 ES5，无构建）
├─ gt800-text.html       杰哥800题 · 纯文本题库（800 题，题干/答案/解析全文可检索）
├─ DEPLOY.md             本说明文件
└─ assets/
   └─ katex/             KaTeX 本地资产（katex.min.css、katex.min.js、contrib/auto-render.min.js、fonts/*.woff2）
```

工作台内「杰哥800题」入口：

| 入口卡片 | 文件 | 说明 |
|---|---|---|
| 杰哥800题·纯文本 | index.html 内置页 `gt800t` → `gt800-text.html` | 800 题结构化文本，可按题号/关键词搜索、按章节筛选、顺序刷题；公式本地渲染 |

纯文本页右上角「← 工作台」可返回主页入口页。图片版（扫描原图）模块已下线，不再随包分发。

---

## 二、用法 A：在线访问（GitHub Pages，推荐多人/多设备使用）

1. 注册/登录 GitHub，新建仓库（Public），例如 `zsb-workbench`。
2. 把本文件夹的**全部内容**上传到仓库根目录（网页端 "Add file → Upload files" 可直接拖入整个 `zsb-workbench` 目录内的文件，注意 `index.html` 要在仓库根目录）。
3. 仓库 → **Settings → Pages** → Source 选 `Deploy from a branch` → Branch 选 `main` / 目录选 `/ (root)` → Save。
4. 等 1~3 分钟，访问 `https://<你的用户名>.github.io/zsb-workbench/`。
5. 平板 Chrome 打开该地址 → 菜单「添加到主屏幕」，之后像 App 一样点开即用。

提示：仓库仅含 HTML 与 KaTeX 本地资产（约 1 MB 量级），上传/克隆都很快，GitHub Pages 完全够用。

---

## 三、用法 B：完全离线（把文件夹拷进平板本地）

1. 用数据线把平板连电脑，选择「传输文件 / MTP」。
2. 在平板存储里建目录，例如 `内部存储/Documents/zsb-workbench`，把本文件夹**连同 `assets` 子目录整体**拷进去（不要只拷 html）。
3. 平板上用文件管理器（ES 文件浏览器 / 系统「文件」）找到 `index.html`，选择用 **Chrome** 打开。
   若浏览器地址栏显示 `file:///storage/emulated/0/Documents/zsb-workbench/index.html` 即为成功。
4. 建议在 Chrome 中把该页面「添加到主屏幕」，下次一键进入。

离线可用性说明：

- 公式渲染使用 `assets/katex/` 本地资产，**不需要网络**；若本地资产缺失才会回退到 CDN（jsdelivr → unpkg → npmmirror）。
- 题库文本、公式资产均在本目录内，断网照常浏览。
- 学习进度（已掌握标记、浏览位置）保存在浏览器 `localStorage`，题库键名 `zsb6_gt800_text`。

⚠️ 关于本地 `file://` 打开的进度保存：部分安卓浏览器对本地文件的存储限制较严，可能出现"刷新后进度丢失/主题不记忆"。若遇到，改用「用法 A」在线访问，或把站点放到局域网（如电脑上跑 Python 简易服务、平板访问 `http://电脑IP:端口/`）。

---

## 四、平板适配已做的事

- 所有可点元素的点击区 **≥ 44×44 px**（触控标准），`pointer: coarse` 设备上进一步加高到 46 px。
- 页面 `overflow-x` 锁定，无横向滚动条；长标题、长公式自动换行，不撑破屏幕。
- 宽屏平板（700–1200 px）自动切 2 列卡片，竖屏窄屏单列。
- 深色模式适配（跟随系统 `prefers-color-scheme`）：深底高对比文字，公式无黑块。
- 题库 800 张卡片使用 `content-visibility` 离屏跳过渲染，首屏更快、滑动更稳。
- 输入框字号 16 px，避免移动端聚焦时页面被自动放大。
- 保留 `viewport` 与 `text-size-adjust`，横竖屏旋转不乱版。

---

## 五、更新与维护

- 替换文件即完成更新：覆盖 `index.html`、`gt800-text.html` 或 `assets/` 下对应文件，刷新页面（建议 Ctrl+F5 或平板下拉刷新）即可。
- 在线版更新后，GitHub Pages 需 1~3 分钟生效。
- 备份：包内 `index.html.bak-*` 若存在为改动前快照，可随时回滚；该文件不参与站点运行，可删除。

---

## 六、常见问题

| 现象 | 处理 |
|---|---|
| 打开是空白 / 只显示代码 | 确认是用浏览器打开 `index.html`，而不是文本编辑器 |
| 公式显示成红字或 `$...$` | 确认 `assets/katex/katex.min.js`、`contrib/auto-render.min.js` 存在；该情况只在本地资产缺失且无网络时出现 |
| 进度不保存 | 换用在线访问或局域网访问；本地 `file://` 受浏览器存储策略限制 |
| 页面加载慢 | 题库约几百 KB，若加载慢多为浏览器缓存或网络问题，刷新一次即可 |
| GitHub Pages 404 | 确认仓库根目录有 `index.html`，且 Pages 的 Branch/目录设置正确，稍等几分钟再刷新 |

---

## 七、自测记录（本次交付）

- 单文件语法自检：`index.html`、`gt800-text.html` 内联脚本 `node --check` 通过。
- jsdom 功能回归：35 项断言全部通过 —— 入口卡生成、题量/章节统计（800 / 16 章 / 基础 327 / 强化 473）、掌握进度读取 `zsb6_gt800_text`、章节掌握明细、全站 25 个页面遍历渲染无报错、题库 800 题渲染、勾选写回 `mastered`。
- 真实浏览器（Edge headless / CDP，模拟安卓平板）：
  - 800×1280、960×600、600×960、1024×768 四种视口下 `scrollWidth == clientWidth`，**无横向溢出**。
  - 可点元素最小高度 44 px、最小宽度 44 px，无小于 44 px 的漏网元素（共 1604 个交互元素抽检）。
  - 纯文本题库渲染 800 张卡片、5849 个公式节点、`katex-error` 为 **0**；KaTeX 走本地 `./assets/katex/`，无 CDN 脚本加载记录。
  - 深色模式截图核对：文字对比正常、公式正常、无截断。
- 返回按钮：`a.iconbtn.back → index.html`，44×44 px，位于页头，滚动常驻。
*（内容由AI生成，仅供参考）*
