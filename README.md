# WeRead Progress

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![CI](https://github.com/lurui1997/weread-progress/actions/workflows/ci.yml/badge.svg)](https://github.com/lurui1997/weread-progress/actions/workflows/ci.yml)
[![Install](https://img.shields.io/badge/Install-Tampermonkey-black)](https://raw.githubusercontent.com/lurui1997/weread-progress/main/src/weread-progress.user.js)

在微信读书网页版书架上，把每本书读到哪画出来。

微信读书网页版书架 / 书单不展示 App 上的阅读状态。接口已经返回 `progress` 和 `finishReading`，封面下却是空的。这个油猴脚本把状态画回封面。

> 非官方项目，与腾讯 / 微信读书无关。

## 功能

- **读完**：`progress === 100`，或书架 `finishReading === 1`
- **已读到 x%**：`progress` 为 1–99（`1` 表示 1%，不是 100%）
- **未开始**：`progress === 0` 且未标记读完

口径对齐 [微信读书官方 Skill](https://github.com/Tencent/WeChatReading/blob/main/skills/book.md)。脚本只读当前登录态下的同域接口，不上传账号。

## 安装

需要 [Tampermonkey](https://www.tampermonkey.net/)（或兼容的用户脚本管理器）。Chrome 138+ 必须先打开扩展详情里的 **允许用户脚本**，否则仪表盘会提示「没有安装任何脚本」。

1. 打开 [篡改猴详情](chrome://extensions/?id=dhdgffkkebhmkfjojejmpbldmpobfkfo)
2. 打开 **允许用户脚本**
3. 点击 [安装脚本](https://raw.githubusercontent.com/lurui1997/weread-progress/main/src/weread-progress.user.js)，在提示页选「安装」
4. 打开已登录的 [书架](https://weread.qq.com/web/shelf) 或书单页

也可以把 [`src/weread-progress.user.js`](src/weread-progress.user.js) 粘进 Tampermonkey 新建脚本。

油猴开关无效时：确认「允许运行用户脚本」已打开，然后完全退出 Chrome（`Cmd+Q` / 退出浏览器）再进书架。仪表盘版本至少 **0.1.3**。

## AI 安装

把下面整段发给 Cursor / Claude / ChatGPT 等能操作本机浏览器的助手：

```
帮我在本机 Chrome 安装微信读书书架进度油猴脚本。

1. 确认已安装 Tampermonkey。没有就先装：https://www.tampermonkey.net/
2. Chrome 138+：打开 chrome://extensions/?id=dhdgffkkebhmkfjojejmpbldmpobfkfo ，打开「允许用户脚本」或「允许运行用户脚本」。
3. 用油猴安装这个地址（打开后点安装；已装过就更新到最新）：
   https://raw.githubusercontent.com/lurui1997/weread-progress/main/src/weread-progress.user.js
4. 仪表盘里确认「微信读书书架进度」已启用，版本至少 0.1.3。
5. 打开已登录的 https://weread.qq.com/web/shelf 或某个书单封面墙，封面上应出现「读完 / 已读到 x% / 未开始」。
6. 没有进度条：完全退出 Chrome（macOS 用 Cmd+Q）再打开书架。不要只关窗口。

脚本只读当前登录态下的同域接口，不上传账号。非官方，与腾讯 / 微信读书无关。
```

助手装完后，自己打开书架看一眼封面即可。

## 使用

1. 用 Chrome 打开已登录的 [微信读书网页版](https://weread.qq.com/web/shelf)
2. 进入**书架**或某个**书单**（封面墙）。首页、阅读器内页不会画进度
3. 换书单或加载更多封面后，进度会再刷一遍；没有就整页刷新
4. 进度跟 App 同一套登录态，换账号后刷新即可

## 开发

```sh
npm test
```

进度文案逻辑在 `src/label.js`，油猴脚本在 `src/weread-progress.user.js`。

## 贡献

欢迎 Issue 和 Pull Request。请先看 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [行为准则](CODE_OF_CONDUCT.md)。安全问题请按 [SECURITY.md](SECURITY.md) 私下告知，不要公开开 Issue。

## License

[MIT](LICENSE)
