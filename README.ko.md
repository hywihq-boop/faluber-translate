<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### AI 기반 웹페이지 번역

  AI를 활용한 Chrome 브라우저 번역 확장 프로그램. 텍스트 노드 수준 DOM 조작. 50개 언어. OpenAI 호환 API.

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>지원 언어</sup></td>
  <td align="center"><b>2</b><br><sup>번역 모드</sup></td>
  <td align="center"><b>8</b><br><sup>동시 번역</sup></td>
  <td align="center"><b>10</b><br><sup>API 제공업체</sup></td>
  <td align="center"><b>~1s</b><br><sup>단어 설명</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_다운로드-최신_버전-7c5cfc?style=for-the-badge" alt="다운로드"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ 주요 기능

<table>
<tr>
<td width="50%">

### 🚀 원클릭 전체 페이지 번역
플로팅 위젯 클릭 또는 <kbd>Alt+T</kbd>로 전체 페이지 번역. 텍스트 노드 수준 치환으로 페이지 구조 보존.

</td>
<td width="50%">

### 🔍 Ctrl + 스마트 설명
단어에 호버 + <kbd>Ctrl</kbd> 탭으로 AI 설명 버블 표시. 텍스트 선택 + <kbd>Ctrl</kbd>으로 문단 설명. DOM 오염 제로.

</td>
</tr>
<tr>
<td width="50%">

### ⚡ 듀얼 번역 모드
**표준** — 3 동시, 뷰포트 우선, 속도와 비용 균형.<br>
**터보** — 8 동시, 전체 페이지, 최대 속도.

</td>
<td width="50%">

### 🔑 다중 API 관리
10개 제공업체 프리셋 내장. 여러 API 설정 저장, 언제든 전환. 모델 자동 가져오기, 사용자 정의 지원.

</td>
</tr>
<tr>
<td width="50%">

### 📋 번역 패널 <kbd>Alt+Q</kbd>
좌우 분할 플로팅 번역 패널. 입력한 원문 즉시 번역. 페이지 번역과 독립적, 모든 언어 쌍 지원.

</td>
<td width="50%">

### 💾 스마트 캐시
메모리 + 영구 이중 캐시, 1시간 TTL. 중복 콘텐츠 토큰 소비 없음. 언어 변경 시 자동 삭제.

</td>
</tr>
</table>

---

## 📦 3단계로 시작

<table>
<tr>
<td align="center" width="33%">
  <b>1. 설치</b><br>
  <sup><a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a>에서 zip 다운로드,<br>압축 해제 후 <code>chrome://extensions</code>에서 로드</sup>
</td>
<td align="center" width="33%">
  <b>2. API 설정</b><br>
  <sup>제공업체 선택, API 키 입력,<br>연결 테스트, 저장</sup>
</td>
<td align="center" width="33%">
  <b>3. 번역</b><br>
  <sup>아무 페이지나 열고 위젯 클릭<br>또는 <kbd>Alt+T</kbd> 누르기</sup>
</td>
</tr>
</table>

---

## 🔧 10개 API 제공업체

내장 프리셋. 모든 OpenAI 호환 API 사용 가능:

| 제공업체 | API 기본 URL |
|---------|-------------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Zhipu | `https://open.bigmodel.cn/api/paas/v4` |
| DashScope | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| 사용자 정의 | 모든 OpenAI 호환 엔드포인트 |

---

## 🛠️ 작동 방식

```
사용자 번역 트리거
  → Content Script가 DOM 순회, 보이는 텍스트 노드 수집
  → 가시성 확인 → CJK 중복 제거 → 최소 길이 필터 → 캐시 중복 제거
  → Y 좌표 정렬, 인접 노드 병합
  → 배치 → Service Worker로 전송 (3–8 동시)
  → AI API 호출 (OpenAI 호환) → 결과 반환
  → DOM 텍스트 치환 → 실시간 진행률 표시줄
```

### 스마트 처리
- `<script>`, `<style>`, `<code>` 등 비콘텐츠 태그 건너뛰기
- 숫자, URL, 이모지 등 번역 불필요 콘텐츠 필터링
- `display:none`, `visibility:hidden` 숨김 상태 감지
- HTML 엔티티 및 특수 문자 보존
- 인접 텍스트 노드 병합 후 API 전송

### 모드 비교

| 매개변수 | 표준 | 터보 |
|---------|------|------|
| 동시성 | 3 | 8 |
| 배치 크기 | 400자 | 250자 |
| 페이지 범위 | 뷰포트만 | 전체 페이지 |
| 스크롤 감지 | ✅ | — |
| 호버 감지 | ✅ | — |
| 동적 콘텐츠 | ✅ | ✅ |

### 캐시 시스템
| 계층 | 저장소 | 제한 | TTL |
|------|--------|------|-----|
| 메모리 | `Map<원문, 번역>` | 무제한 | 세션 |
| 영구 | `chrome.storage.local` | 2,000 | 1시간 |

---

## 🌍 50개 대상 언어 · 20개 UI 언어

<details>
<summary>전체 언어 목록 보기</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 프로젝트 구조

```
faluber translate/
├── manifest.json              # 확장 프로그램 설정 (Manifest V3)
├── background/
│   └── service-worker.js      # API 호출 및 메시지 라우팅
├── content/
│   ├── content.js             # DOM 텍스트 추출 및 교체
│   └── content.css            # 플로팅 위젯 스타일
├── popup/
│   ├── popup.html             # 설정 팝업
│   ├── popup.js               # 다중 API 관리
│   └── popup.css              # 팝업 스타일
├── icons/                     # 확장 프로그램 아이콘
├── docs/                      # 제품 웹사이트
└── generate-icons.js          # 아이콘 생성기 (개발 도구)
```

---

## 🔒 개인정보 보호

- API 키는 Chrome 동기화 저장소에 **로컬**로 저장
- 번역 요청은 브라우저에서 **직접** 설정된 API 제공업체로 전송
- **제3자 서버 없음** — 데이터는 사용자와 API 제공업체 간에만 유지

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 릴리스</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 버그 신고</a> ·
  <a href="LICENSE">📝 MIT 라이선스</a>
  <br><br>
  <sub>❤️로 제작 · 사용자 데이터 수집 없음</sub>
</div>
