# 📋 Field Note — Setup Guide

## 파일 구조
```
fieldnote/
├── code.gs          ← Google Apps Script (GAS 편집기에 붙여넣기)
├── index.html       ← GitHub Pages 메인 앱
├── manifest.json    ← PWA 설정 (안드로이드 홈화면 설치용)
├── sw.js            ← Service Worker (오프라인 캐시)
└── icons/
    ├── icon-192.png ← 앱 아이콘 192×192
    └── icon-512.png ← 앱 아이콘 512×512
```

---

## ① Google Apps Script 설정

1. [script.google.com](https://script.google.com) → 새 프로젝트
2. `Code.gs` 내용을 전부 **붙여넣기**
3. **프로젝트 설정 → 스크립트 속성** 에서 추가:
   - 키: `GEMINI_API_KEY`
   - 값: 발급받은 Gemini API Key

4. 편집기 상단 함수 드롭다운에서 **`setup`** 선택 → **실행** (최초 1회)
   - 시트 헤더 자동 생성

5. **배포 → 새 배포** 클릭
   - 유형: **웹 앱**
   - 다음 사용자로 실행: **나 (본인)**
   - 액세스 권한: **모든 사용자**
   - → **배포** → URL 복사 ✂️

---

## ② GitHub Pages 설정

1. GitHub 새 저장소 생성 (예: `field-note`)
2. 아래 4개 파일 업로드:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192.png` (별도 제작 필요)
   - `icons/icon-512.png` (별도 제작 필요)
3. **Settings → Pages → Branch: main → Save**
4. 발급된 GitHub Pages URL 메모 (예: `https://yourname.github.io/field-note/`)

> **아이콘 빠른 제작:** [favicon.io](https://favicon.io/emoji-favicons/clipboard/) 에서 📋 이모지 아이콘 다운로드 후 사용

---

## ③ 앱 첫 실행 설정

1. 안드로이드 Chrome에서 GitHub Pages URL 접속
2. **⚙ 설정 탭** 진입
3. **Google Apps Script URL** 란에 ①에서 복사한 GAS URL 붙여넣기
4. **SAVE SETTINGS** 클릭

---

## ④ 안드로이드 홈화면 설치

1. Chrome 브라우저에서 앱 URL 접속
2. Chrome 메뉴(⋮) → **홈 화면에 추가** 또는
3. 하단에 자동으로 뜨는 **"앱 설치"** 배너 클릭
4. 홈화면에서 실행하면 **전체화면 모드** (상/하단 브라우저 UI 없음)

---

## 시트 컬럼 구조 (자동 생성)

| # | 컬럼명 | 설명 |
|---|--------|------|
| A | No. | 자동 번호 |
| B | Date&time | 등록 일시 |
| C | Equipment Tag | 장비 태그 |
| D | Name | 등록자 이름 |
| E | Location | 위치 |
| F | Drawing No. | 도면 번호 |
| G | Type | 문제 유형 |
| H | Comment(Korean) | 한국어 코멘트 |
| I | Comment(English) | 영어 코멘트 |
| J~AC | Photo1~Photo20 | 사진 Google Drive URL |

---

## 주요 기능 요약

| 기능 | 설명 |
|------|------|
| 📌 등록 | Equipment Tag, Name, Location, Drawing No., Type, Comment, 사진 최대 20장 |
| 🌐 자동 번역 | 한국어만 입력 → 영어 자동 번역 (Gemini 1.5 Flash) |
| 📷 사진 압축 | 업로드 전 최대 1200px로 자동 압축 (용량 절감) |
| 💾 캐시 | 시트 변경 감지 후 자동 동기화, 변경 없으면 로컬 캐시 사용 |
| 🔍 검색 | Tag / Location / Drawing / Type / 키워드 / 날짜 범위 복합 검색 |
| 📱 PWA | 안드로이드 홈화면 설치 → 전체화면 실행 |

---

## Gemini API Key 발급

1. [aistudio.google.com](https://aistudio.google.com) 접속
2. **Get API Key → Create API key** 클릭
3. 생성된 키를 GAS Script Properties에 저장
