<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### AI 搭載ウェブページ翻訳

  AI を活用した Chrome ブラウザ翻訳拡張機能。テキストノードレベルの DOM 操作。50 言語対応。OpenAI 互換 API。

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>対応言語</sup></td>
  <td align="center"><b>2</b><br><sup>翻訳モード</sup></td>
  <td align="center"><b>8</b><br><sup>同時翻訳</sup></td>
  <td align="center"><b>10</b><br><sup>API 対応</sup></td>
  <td align="center"><b>~1s</b><br><sup>単語説明</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_ダウンロード-最新版-7c5cfc?style=for-the-badge" alt="ダウンロード"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ 主要機能

<table>
<tr>
<td width="50%">

### 🚀 ワンクリック全ページ翻訳
フローティングウィジェットをクリック、または <kbd>Alt+T</kbd> でページ全体を翻訳。テキストノードレベルで置換し、ページ構造を維持。

</td>
<td width="50%">

### 🔍 Ctrl + スマート説明
単語にホバー + <kbd>Ctrl</kbd> タップで AI 説明バブルを表示。テキスト選択 + <kbd>Ctrl</kbd> で文章全体を説明。DOM 汚染ゼロ。

</td>
</tr>
<tr>
<td width="50%">

### ⚡ デュアル翻訳モード
**標準** — 3 並列、ビューポート優先、速度とコストのバランス。<br>
**ターボ** — 8 並列、全ページ、最大速度。

</td>
<td width="50%">

### 🔑 マルチ API 管理
10 のプロバイダープリセット内蔵。複数の API 設定を保存し、いつでも切替可能。モデル自動取得、カスタム対応。

</td>
</tr>
<tr>
<td width="50%">

### 📋 翻訳パネル <kbd>Alt+Q</kbd>
左右分割のフローティング翻訳パネル。入力した原文を即時翻訳。ページ翻訳とは独立して動作、全言語ペア対応。

</td>
<td width="50%">

### 💾 スマートキャッシュ
メモリ + 永続の二層キャッシュ、1 時間 TTL。重複コンテンツのトークン消費なし。言語切替で自動クリア。

</td>
</tr>
</table>

---

## 📦 3 ステップで開始

<table>
<tr>
<td align="center" width="33%">
  <b>1. インストール</b><br>
  <sup><a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a> から zip をダウンロード、<br>解凍して <code>chrome://extensions</code> で読込</sup>
</td>
<td align="center" width="33%">
  <b>2. API 設定</b><br>
  <sup>プロバイダーを選択、API キー入力、<br>接続テスト、保存</sup>
</td>
<td align="center" width="33%">
  <b>3. 翻訳</b><br>
  <sup>任意のページを開き、ウィジェットを<br>クリックまたは <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 の API プロバイダー

内蔵プリセット。OpenAI 互換 API ならどれでも動作：

| プロバイダー | API ベース URL |
|-------------|---------------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Zhipu | `https://open.bigmodel.cn/api/paas/v4` |
| DashScope | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| カスタム | 任意の OpenAI 互換エンドポイント |

---

## 🛠️ 仕組み

```
ユーザーが翻訳をトリガー
  → Content Script が DOM を走査し、可視テキストノードを収集
  → 可視性チェック → CJK 重複除去 → 最小長フィルター → キャッシュ重複除去
  → Y 座標でソート、隣接ノードをマージ
  → バッチ化 → Service Worker に送信（3–8 並列）
  → AI API（OpenAI 互換形式）を呼出 → 結果を返却
  → DOM テキスト置換 → リアルタイムプログレスバー
```

### スマート処理
- `<script>`、`<style>`、`<code>` などの非コンテンツタグをスキップ
- 数字、URL、絵文字など翻訳不要なコンテンツをフィルタリング
- `display:none`、`visibility:hidden` の非表示状態を検出
- HTML エンティティと特殊文字を保持
- 隣接テキストノードをマージして API に送信

### モード比較

| パラメータ | 標準 | ターボ |
|-----------|------|-------|
| 並列数 | 3 | 8 |
| バッチサイズ | 400 文字 | 250 文字 |
| ページ範囲 | ビューポートのみ | 全ページ |
| スクロール検出 | ✅ | — |
| ホバー検出 | ✅ | — |
| 動的コンテンツ | ✅ | ✅ |

### キャッシュシステム
| 層 | ストレージ | 上限 | TTL |
|----|-----------|------|-----|
| メモリ | `Map<原文, 訳文>` | 無制限 | セッション |
| 永続 | `chrome.storage.local` | 2,000 | 1 時間 |

---

## 🌍 50 言語 · 20 UI 言語

<details>
<summary>全言語リストを展開</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 プロジェクト構成

```
faluber translate/
├── manifest.json              # 拡張機能設定 (Manifest V3)
├── background/
│   └── service-worker.js      # API 呼出とメッセージルーティング
├── content/
│   ├── content.js             # DOM テキスト抽出と置換
│   └── content.css            # フローティングウィジェット
├── popup/
│   ├── popup.html             # 設定ポップアップ
│   ├── popup.js               # マルチ API 管理
│   └── popup.css              # ポップアップスタイル
├── icons/                     # 拡張機能アイコン
├── docs/                      # 製品ウェブサイト
└── generate-icons.js          # アイコン生成（開発ツール）
```

---

## 🔒 プライバシー

- API キーは Chrome 同期ストレージに**ローカル**保存
- 翻訳リクエストはブラウザから**直接**設定済み API プロバイダーに送信
- **第三者サーバーは介在しません** — データはあなたと API プロバイダー間のみ

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 リリース</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 バグ報告</a> ·
  <a href="LICENSE">📝 MIT ライセンス</a>
  <br><br>
  <sub>❤️ で制作 · ユーザーデータ収集なし</sub>
</div>
