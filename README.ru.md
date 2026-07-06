<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### ИИ-переводчик веб-страниц

  Расширение Chrome для перевода веб-страниц с помощью ИИ. Манипуляции DOM на уровне текстовых узлов. 50 языков. OpenAI-совместимое API.

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>Языков</sup></td>
  <td align="center"><b>2</b><br><sup>Режима</sup></td>
  <td align="center"><b>8</b><br><sup>Потоков</sup></td>
  <td align="center"><b>10</b><br><sup>Провайдеров</sup></td>
  <td align="center"><b>~1с</b><br><sup>Объяснение</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_Скачать-Последнюю_версию-7c5cfc?style=for-the-badge" alt="Скачать"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ Основные возможности

<table>
<tr>
<td width="50%">

### 🚀 Перевод страницы в один клик
Нажмите на виджет или <kbd>Alt+T</kbd> для перевода всей страницы. Замена на уровне текстовых узлов сохраняет структуру.

</td>
<td width="50%">

### 🔍 Ctrl + Умное объяснение
Наведите на слово + нажмите <kbd>Ctrl</kbd> для ИИ-объяснения. Выделите текст + <kbd>Ctrl</kbd> для объяснения абзаца. Без изменения DOM.

</td>
</tr>
<tr>
<td width="50%">

### ⚡ Два режима перевода
**Стандартный** — 3 потока, сначала видимая область, баланс скорости и затрат.<br>
**Турбо** — 8 потоков, вся страница, максимальная скорость.

</td>
<td width="50%">

### 🔑 Мульти-API управление
10 встроенных пресетов провайдеров. Сохраняйте несколько конфигураций, переключайтесь в любое время. Автозагрузка моделей, свои endpoint'ы.

</td>
</tr>
<tr>
<td width="50%">

### 📋 Панель перевода <kbd>Alt+Q</kbd>
Плавающая панель с двумя колонками для мгновенного перевода. Работает независимо от перевода страницы. Любые языковые пары.

</td>
<td width="50%">

### 💾 Умный кэш
Двухуровневый кэш: в памяти и постоянный, TTL 1 час. Повторный контент не тратит токены. Автоочистка при смене языка.

</td>
</tr>
</table>

---

## 📦 Начало за 3 шага

<table>
<tr>
<td align="center" width="33%">
  <b>1. Установка</b><br>
  <sup>Скачайте zip из <a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a>,<br>распакуйте и загрузите в <code>chrome://extensions</code></sup>
</td>
<td align="center" width="33%">
  <b>2. Настройка API</b><br>
  <sup>Выберите провайдера, введите ключ,<br>проверьте соединение, сохраните</sup>
</td>
<td align="center" width="33%">
  <b>3. Перевод</b><br>
  <sup>Откройте любую страницу, нажмите<br>виджет или <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 API-провайдеров

Встроенные пресеты. Любое OpenAI-совместимое API работает:

| Провайдер | Базовый URL API |
|-----------|----------------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Zhipu | `https://open.bigmodel.cn/api/paas/v4` |
| DashScope | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| Свой | Любой OpenAI-совместимый endpoint |

---

## 🛠️ Как это работает

```
Пользователь запускает перевод
  → Content Script обходит DOM, собирает видимые текстовые узлы
  → Проверка видимости → Дедупликация CJK → Фильтр длины → Дедупликация кэша
  → Сортировка по Y, слияние соседних
  → Пакет → Service Worker (3–8 потоков)
  → Вызов AI API (OpenAI-совместимое) → Возврат результата
  → Замена текста в DOM → Прогресс-бар в реальном времени
```

### Умная обработка
- Пропуск `<script>`, `<style>`, `<code>` и неконтентных тегов
- Фильтрация чисел, URL, эмодзи и нетекстового содержимого
- Обнаружение `display:none`, `visibility:hidden`
- Сохранение HTML-сущностей и спецсимволов
- Слияние соседних текстовых узлов перед отправкой

### Сравнение режимов

| Параметр | Стандарт | Турбо |
|----------|---------|-------|
| Потоков | 3 | 8 |
| Размер пакета | 400 симв. | 250 симв. |
| Охват | Только viewport | Вся страница |
| Отслеж. скролла | ✅ | — |
| Отслеж. наведения | ✅ | — |
| Дин. контент | ✅ | ✅ |

### Система кэширования
| Уровень | Хранилище | Лимит | TTL |
|---------|-----------|-------|-----|
| Память | `Map<ориг, перев>` | Без лимита | Сессия |
| Постоянный | `chrome.storage.local` | 2 000 | 1 час |

---

## 🌍 50 языков перевода · 20 языков интерфейса

<details>
<summary>Показать полный список языков</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 Структура проекта

```
faluber translate/
├── manifest.json              # Конфигурация (Manifest V3)
├── background/
│   └── service-worker.js      # Вызовы API и маршрутизация
├── content/
│   ├── content.js             # Извлечение и замена текста DOM
│   └── content.css            # Стили виджета
├── popup/
│   ├── popup.html             # Окно настроек
│   ├── popup.js               # Управление API
│   └── popup.css              # Стили попапа
├── icons/                     # Иконки расширения
├── docs/                      # Веб-сайт продукта
└── generate-icons.js          # Генератор иконок (инструмент)
```

---

## 🔒 Приватность

- API-ключ хранится **локально** в синхронизированном хранилище Chrome
- Запросы идут **напрямую** из браузера к вашему API-провайдеру
- **Без сторонних серверов** — данные только между вами и провайдером

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 Релизы</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 Баг-репорт</a> ·
  <a href="LICENSE">📝 MIT Лицензия</a>
  <br><br>
  <sub>Сделано с ❤️ · Данные не собираются</sub>
</div>
