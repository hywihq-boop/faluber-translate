[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Русский](README.ru.md) | [العربية](README.ar.md)

<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### AI-Powered Web Page Translation

  A Chrome extension that translates web pages using AI. Text-node-level DOM manipulation. 50 languages. OpenAI-compatible API.

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>Languages</sup></td>
  <td align="center"><b>2</b><br><sup>Modes</sup></td>
  <td align="center"><b>8</b><br><sup>Concurrent</sup></td>
  <td align="center"><b>10</b><br><sup>API Providers</sup></td>
  <td align="center"><b>~1s</b><br><sup>Word Explain</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_Download-Latest_Release-7c5cfc?style=for-the-badge" alt="Download"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ Core Features

<table>
<tr>
<td width="50%">

### 🚀 One-Click Full-Page
Click the floating widget or press <kbd>Alt+T</kbd> to translate the entire page. Text-node-level replacement preserves the page layout perfectly.

</td>
<td width="50%">

### 🔍 Ctrl + Smart Explain
Hover over any word + tap <kbd>Ctrl</kbd> for an AI explanation bubble. Select text + <kbd>Ctrl</kbd> to explain a whole passage. Zero DOM pollution.

</td>
</tr>
<tr>
<td width="50%">

### ⚡ Dual Translation Modes
**Standard** — 3 concurrent, viewport-first, balanced speed & cost.<br>
**Turbo** — 8 concurrent, full-page, maximum speed.

</td>
<td width="50%">

### 🔑 Multi-API Management
10 built-in provider presets. Save multiple API configs, switch anytime. Auto-fetch available models. Custom endpoints supported.

</td>
</tr>
<tr>
<td width="50%">

### 📋 Translation Panel <kbd>Alt+Q</kbd>
Side-by-side floating panel for instant input/output translation. Works independently from page translation. Any language pair.

</td>
<td width="50%">

### 💾 Smart Cache
In-memory + persistent dual-layer cache with 1-hour TTL. No duplicate token spend. Auto-clears on language change.

</td>
</tr>
</table>

---

## 📦 Quick Start

<table>
<tr>
<td align="center" width="33%">
  <b>1. Install</b><br>
  <sup>Download from <a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a>, unzip,<br>load unpacked in <code>chrome://extensions</code></sup>
</td>
<td align="center" width="33%">
  <b>2. Configure API</b><br>
  <sup>Choose a provider, enter API Key,<br>test connection, save</sup>
</td>
<td align="center" width="33%">
  <b>3. Translate</b><br>
  <sup>Open any page, click widget<br>or press <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 API Providers

Built-in presets. Any OpenAI-compatible API works:

| Provider | API Base URL |
|----------|-------------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Zhipu | `https://open.bigmodel.cn/api/paas/v4` |
| DashScope | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| Custom | Any OpenAI-compatible endpoint |

---

## 🛠️ How It Works

```
User triggers translation
  → Content Script traverses DOM, collects visible text nodes
  → Visibility check → CJK dedup → Min-length filter → Cache dedup
  → Sort by Y-coordinate, merge adjacent nodes
  → Batch → Service Worker (3–8 concurrent)
  → AI API (OpenAI-compatible) → Results back
  → DOM text replacement → Real-time progress bar
```

### Smart Processing
- Skips `<script>`, `<style>`, `<code>`, and non-content tags
- Filters numbers, URLs, emoji, and untranslatable content
- Detects `display:none`, `visibility:hidden` hidden states
- Preserves HTML entities and special characters
- Merges adjacent text nodes before sending to API

### Mode Comparison

| Parameter | Standard | Turbo |
|-----------|----------|-------|
| Concurrency | 3 | 8 |
| Batch size | 400 chars | 250 chars |
| Page scope | Viewport only | Full page |
| Scroll detect | ✅ | — |
| Hover detect | ✅ | — |
| Dynamic content | ✅ | ✅ |

### Cache System
| Layer | Storage | Limit | TTL |
|-------|---------|-------|-----|
| Memory | `Map<src, tgt>` | Unlimited | Session |
| Persistent | `chrome.storage.local` | 2,000 | 1 hour |

---

## 🌍 50 Target Languages · 20 UI Languages

<details>
<summary>Click to expand full language list</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 Project Structure

```
faluber translate/
├── manifest.json              # Extension config (Manifest V3)
├── background/
│   └── service-worker.js      # API calls & message routing
├── content/
│   ├── content.js             # DOM text extraction & replacement
│   └── content.css            # Floating widget styles
├── popup/
│   ├── popup.html             # Settings popup
│   ├── popup.js               # Multi-API management
│   └── popup.css              # Popup styles
├── icons/                     # Extension icons
├── docs/                      # Product website
└── generate-icons.js          # Icon generator (dev tool)
```

---

## 🔒 Privacy

- API key stored **locally** in Chrome sync storage
- Requests go **directly** from your browser to your API provider
- **No third-party servers** — your data stays between you and your API provider

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 Releases</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 Report Bug</a> ·
  <a href="LICENSE">📝 MIT License</a>
  <br><br>
  <sub>Made with ❤️ · No user data collected</sub>
</div>
