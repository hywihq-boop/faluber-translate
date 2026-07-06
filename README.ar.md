<div align="center" dir="rtl">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### ترجمة صفحات الويب بالذكاء الاصطناعي

  إضافة Chrome تترجم صفحات الويب باستخدام الذكاء الاصطناعي. معالجة على مستوى عقد DOM. 50 لغة. واجهة API متوافقة مع OpenAI.

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)
</div>

<br>

<div align="center">

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>لغة</sup></td>
  <td align="center"><b>2</b><br><sup>وضع</sup></td>
  <td align="center"><b>8</b><br><sup>متزامن</sup></td>
  <td align="center"><b>10</b><br><sup>مزود API</sup></td>
  <td align="center"><b>~1s</b><br><sup>شرح كلمة</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_تحميل-أحدث_إصدار-7c5cfc?style=for-the-badge" alt="تحميل"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ الميزات الأساسية

<table>
<tr>
<td width="50%">

### 🚀 ترجمة الصفحة كاملة بنقرة
انقر الأداة العائمة أو اضغط <kbd>Alt+T</kbd> لترجمة الصفحة كاملة. استبدال على مستوى عقد النص يحافظ على هيكل الصفحة.

</td>
<td width="50%">

### 🔍 Ctrl + شرح ذكي
مرر فوق أي كلمة + اضغط <kbd>Ctrl</kbd> لإظهار فقاعة شرح بالذكاء الاصطناعي. حدد نصاً + <kbd>Ctrl</kbd> لشرح فقرة كاملة. بدون تلويث DOM.

</td>
</tr>
<tr>
<td width="50%">

### ⚡ وضعان للترجمة
**قياسي** — 3 متزامن، أولوية المنطقة المرئية، توازن بين السرعة والتكلفة.<br>
**توربو** — 8 متزامن، الصفحة كاملة، سرعة قصوى.

</td>
<td width="50%">

### 🔑 إدارة متعددة لواجهات API
10 إعدادات مسبقة لمزودين. احفظ عدة إعدادات API وبدّل بينها. جلب تلقائي للنماذج، دعم نقاط نهاية مخصصة.

</td>
</tr>
<tr>
<td width="50%">

### 📋 لوحة الترجمة <kbd>Alt+Q</kbd>
لوحة عائمة جنباً إلى جنب للإدخال/الإخراج. ترجمة فورية للنص المدخل. تعمل بشكل مستقل عن ترجمة الصفحة. أي زوج لغوي.

</td>
<td width="50%">

### 💾 تخزين مؤقت ذكي
ذاكرة + تخزين دائم، TTL ساعة واحدة. لا استهلاك متكرر للرموز. مسح تلقائي عند تغيير اللغة.

</td>
</tr>
</table>

---

## 📦 ابدأ في 3 خطوات

<table>
<tr>
<td align="center" width="33%">
  <b>1. تثبيت</b><br>
  <sup>حمّل zip من <a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a>،<br>فك الضغط وحمّل في <code>chrome://extensions</code></sup>
</td>
<td align="center" width="33%">
  <b>2. إعداد API</b><br>
  <sup>اختر مزوداً، أدخل مفتاح API،<br>اختبر الاتصال، احفظ</sup>
</td>
<td align="center" width="33%">
  <b>3. ترجم</b><br>
  <sup>افتح أي صفحة، انقر الأداة<br>أو اضغط <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 مزودي API

إعدادات مسبقة مدمجة. أي واجهة متوافقة مع OpenAI تعمل:

| المزود | عنوان API الأساسي |
|--------|------------------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Zhipu | `https://open.bigmodel.cn/api/paas/v4` |
| DashScope | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| مخصص | أي نقطة نهاية متوافقة مع OpenAI |

---

## 🛠️ آلية العمل

```
يقوم المستخدم بتشغيل الترجمة
  → يتصفح Content Script شجرة DOM ويجمع عقد النص المرئية
  → التحقق من الظهور → إزالة تكرار CJK → تصفية الطول → إزالة تكرار التخزين
  → ترتيب حسب المحور Y ودمج المتجاورة
  → تجميع → إرسال إلى Service Worker (3–8 عمال)
  → استدعاء AI API (متوافق مع OpenAI) → إرجاع النتائج
  → استبدال النص في DOM → شريط تقدم مباشر
```

### معالجة ذكية
- تخطي `<script>` و`<style>` و`<code>` والوسوم غير المحتواية
- تصفية الأرقام والروابط والرموز التعبيرية والمحتوى غير القابل للترجمة
- كشف `display:none` و`visibility:hidden`
- الحفاظ على كيانات HTML والرموز الخاصة
- دمج عقد النص المتجاورة قبل الإرسال

### مقارنة الأوضاع

| المعامل | قياسي | توربو |
|---------|-------|-------|
| التوازي | 3 | 8 |
| حجم الدفعة | 400 حرف | 250 حرف |
| نطاق الصفحة | المنطقة المرئية فقط | الصفحة كاملة |
| كشف التمرير | ✅ | — |
| كشف المرور | ✅ | — |
| المحتوى الديناميكي | ✅ | ✅ |

### نظام التخزين المؤقت
| الطبقة | التخزين | الحد | TTL |
|--------|---------|------|-----|
| الذاكرة | `Map<أصل, ترجمة>` | غير محدود | الجلسة |
| دائم | `chrome.storage.local` | 2,000 | ساعة واحدة |

---

## 🌍 50 لغة مستهدفة · 20 لغة واجهة

<details>
<summary>انقر لعرض قائمة اللغات الكاملة</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 هيكل المشروع

```
faluber translate/
├── manifest.json              # إعدادات الإضافة (Manifest V3)
├── background/
│   └── service-worker.js      # استدعاءات API وتوجيه الرسائل
├── content/
│   ├── content.js             # استخراج نصوص DOM واستبدالها
│   └── content.css            # أنماط الأداة العائمة
├── popup/
│   ├── popup.html             # نافذة الإعدادات
│   ├── popup.js               # إدارة API المتعددة
│   └── popup.css              # أنماط النافذة المنبثقة
├── icons/                     # أيقونات الإضافة
├── docs/                      # الموقع الإلكتروني
└── generate-icons.js          # مولد الأيقونات (أداة تطوير)
```

---

## 🔒 الخصوصية

- مفتاح API مخزن **محلياً** في تخزين Chrome المتزامن
- الطلبات تذهب **مباشرة** من متصفحك إلى مزود API
- **لا توجد خوادم طرف ثالث** — بياناتك بينك وبين مزود API فقط

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 الإصدارات</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 الإبلاغ عن خطأ</a> ·
  <a href="LICENSE">📝 رخصة MIT</a>
  <br><br>
  <sub>مصنوع بـ ❤️ · لا يتم جمع بيانات المستخدم</sub>
</div>
