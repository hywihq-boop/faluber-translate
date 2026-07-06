<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### AI 智能网页翻译插件

  基于 AI 的 Chrome 浏览器翻译插件。文本节点级 DOM 操作，50 种语言，兼容 OpenAI 格式 API。

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>支持语言</sup></td>
  <td align="center"><b>2</b><br><sup>翻译模式</sup></td>
  <td align="center"><b>8</b><br><sup>并发翻译</sup></td>
  <td align="center"><b>10</b><br><sup>API 提供商</sup></td>
  <td align="center"><b>~1s</b><br><sup>词语解释</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_下载-最新版本-7c5cfc?style=for-the-badge" alt="下载"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ 核心功能

<table>
<tr>
<td width="50%">

### 🚀 一键整页翻译
点击悬浮球或按 <kbd>Alt+T</kbd> 翻译整个页面。文本节点级替换，不破坏页面结构。

</td>
<td width="50%">

### 🔍 Ctrl + 智能解释
鼠标指向词汇 + 单击 <kbd>Ctrl</kbd> 弹出 AI 解释气泡。选中文字 + <kbd>Ctrl</kbd> 解释整段。零 DOM 污染。

</td>
</tr>
<tr>
<td width="50%">

### ⚡ 双档翻译模式
**标准** — 3 并发，视野优先，速度与消耗均衡。<br>
**极速** — 8 并发，全页翻译，速度拉满。

</td>
<td width="50%">

### 🔑 多 API 管理
内置 10 家提供商预设。保存多个 API 配置，随时切换。自动拉取可用模型，支持自定义接口。

</td>
</tr>
<tr>
<td width="50%">

### 📋 翻译面板 <kbd>Alt+Q</kbd>
左右布局的浮动翻译面板，输入原文即时翻译。独立于页面翻译，支持任意语言对。

</td>
<td width="50%">

### 💾 智能缓存
内存 + 持久化双层缓存，1 小时 TTL。重复内容不消耗 token。语言切换自动清除。

</td>
</tr>
</table>

---

## 📦 三步开始

<table>
<tr>
<td align="center" width="33%">
  <b>1. 安装</b><br>
  <sup>从 <a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a> 下载 zip，解压后<br>在 <code>chrome://extensions</code> 加载</sup>
</td>
<td align="center" width="33%">
  <b>2. 配置 API</b><br>
  <sup>选择提供商，填入 API Key，<br>测试连接，保存</sup>
</td>
<td align="center" width="33%">
  <b>3. 翻译</b><br>
  <sup>打开任意网页，点击悬浮球<br>或按 <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 家 API 提供商

内置预设，兼容任意 OpenAI 格式 API：

| 提供商 | API 地址 |
|--------|----------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| 智谱 | `https://open.bigmodel.cn/api/paas/v4` |
| 阿里百炼 | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| 自定义 | 任意 OpenAI 兼容端点 |

---

## 🛠️ 工作原理

```
用户触发翻译
  → Content Script 遍历 DOM，收集可见文本节点
  → 可见性检测 → CJK 去重 → 最小长度过滤 → 缓存去重
  → 按 Y 坐标排序，相邻节点合并
  → 分包 → 发 Service Worker（3–8 并发）
  → 调 AI API（OpenAI 兼容格式）→ 返回结果
  → DOM 文本替换 → 实时进度条
```

### 智能处理
- 跳过 `<script>`、`<style>`、`<code>` 等非内容标签
- 过滤数字、URL、Emoji 等不可翻译内容
- 检测 `display:none`、`visibility:hidden` 隐藏状态
- 保留 HTML 实体和特殊字符
- 相邻文本节点合并后发送

### 模式对比

| 参数 | 标准 | 极速 |
|------|------|------|
| 并发数 | 3 | 8 |
| 分批大小 | 400 字符 | 250 字符 |
| 翻译范围 | 仅可见区域 | 全页 |
| 滚动检测 | ✅ | — |
| 悬停检测 | ✅ | — |
| 动态内容 | ✅ | ✅ |

### 缓存系统
| 层级 | 存储 | 上限 | TTL |
|------|------|------|-----|
| 内存 | `Map<原文, 译文>` | 无限制 | 会话 |
| 持久化 | `chrome.storage.local` | 2,000 | 1 小时 |

---

## 🌍 50 种目标语言 · 20 种界面语言

<details>
<summary>展开查看完整语言列表</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 项目结构

```
faluber translate/
├── manifest.json              # 扩展配置 (Manifest V3)
├── background/
│   └── service-worker.js      # API 调用与消息路由
├── content/
│   ├── content.js             # DOM 文本提取与替换
│   └── content.css            # 悬浮球样式
├── popup/
│   ├── popup.html             # 设置弹窗
│   ├── popup.js               # 多 API 管理
│   └── popup.css              # 弹窗样式
├── icons/                     # 扩展图标
├── docs/                      # 产品官网
└── generate-icons.js          # 图标生成器（开发工具）
```

---

## 🔒 隐私

- API Key 仅存储在 Chrome **本地**同步存储中
- 翻译请求**直接**从浏览器发送到你的 API 提供商
- **不经过第三方服务器** — 数据只在你和 API 提供商之间传输

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 下载</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 反馈 Bug</a> ·
  <a href="LICENSE">📝 MIT 许可证</a>
  <br><br>
  <sub>用 ❤️ 制作 · 不收集任何用户数据</sub>
</div>
