# PaperKo

논문·설계기준·시방서·일반 문서 PDF를 **원본 레이아웃을 유지한 채** 한국어(및 다국어)로 번역하는
데스크탑 앱입니다(macOS · Windows). 번역본을 원문 편집을 살린 **PDF**로 만들고, 편집 가능한
**한글(HWPX)·Word(DOCX)** 로도 저장합니다.

A desktop app that translates academic papers, design codes, and general PDFs into Korean (and other
languages) **while preserving the original layout**, and exports to PDF, Hangul (HWPX), and Word (DOCX)
(macOS · Windows).

**이 저장소는 설치 파일만 배포합니다.** 앱 소스는 [mikwon3/PaperKo](https://github.com/mikwon3/PaperKo) 에 있습니다.

## 내려받기 · Download

**[최신 판 받기 · Latest release →](https://github.com/mikwon3/PaperKo-releases/releases/latest)**

| 운영체제 | 최신 설치본 (1.8.15) |
|---|---|
| **macOS** 12+ (Apple Silicon) | **[⬇ PaperKo-1.8.15-arm64.dmg](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.15/PaperKo-1.8.15-arm64.dmg)** |
| **Windows** 10+ x64 | **[⬇ PaperKo-1.8.15-amd64-installer.exe](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.15/PaperKo-1.8.15-amd64-installer.exe)** |

각 릴리스에 SHA-256 체크섬을 적어 둡니다. 설치 후에는 앱이 **시작할 때 새 판을 스스로 확인**해
(하루 1회, 설정에서 끄거나 특정 판 건너뛰기 가능) 서명된 릴리스를 받아 자동으로 업데이트합니다.

## 처음 열 때 경고가 뜹니다

설치 파일에 **개발자 서명이 없습니다.** 운영체제가 확인할 수 없는 앱이라고 경고합니다.

**macOS** — "확인할 수 없어 열 수 없습니다" 가 뜨면

1. **시스템 설정 › 개인정보 보호 및 보안** 에서 아래쪽의 **"그래도 열기"** 를 누릅니다.
2. 그래도 열리지 않으면 터미널에서 한 번 실행합니다.
   ```bash
   xattr -dr com.apple.quarantine /Applications/PaperKo.app
   ```

**Windows** — "Windows의 PC 보호" 가 뜨면 **추가 정보 › 실행** 을 누릅니다.

## 핵심 기능

- **레이아웃 보존 번역 PDF** — 2단/1단 편집, 표, 그림, 수식, 절 제목, 참고문헌 구조를 그대로 둔 채
  제자리에 번역문을 다시 조판합니다.
- **HWPX·DOCX 저장** — 완전 오프라인. 표는 실제 표 객체로 복원, 그림은 이미지로 삽입합니다.
- **일반 문서 모드** — 긴 문서(설계기준·시방서·핸드북)를 페이지 범위 배치로 나누어 번역하고, 중단·
  재시작 후에도 이어서 번역합니다.
- **다국어** — 대상 언어 한국어·English·日本語·中文·Español·Deutsch·Français, UI 한/영 토글.
- **OCR** — 스캔·이미지 PDF도 번역합니다.
- **LLM 선택** — OpenAI 호환 원격 서버(vLLM 등)나 OpenAI·Anthropic·Gemini API, 또는 번들
  `llama.cpp` + 로컬 GGUF 로 완전 오프라인 번역.
- **온라인 자동 업데이트** — 서명된 릴리스를 받아 스스로 설치합니다(macOS 는 새 앱으로 교체 후
  재실행, Windows 는 설치 프로그램이 이어받음). 릴리스 정보는 Ed25519 서명으로, 설치본은 SHA-256
  으로 검증합니다.

## 변경 이력 · Releases

전체 목록은 [Releases](https://github.com/mikwon3/PaperKo-releases/releases) 를 참조하세요.

### [1.8.15](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.15)
#### 번역문이 겹쳐 보이던 문제 수정

스캔·OCR 문서에서 일부 페이지의 **번역문 여러 줄이 서로 겹쳐 뭉개져 보이던 문제**를 고쳤습니다.

OCR 과정에서 같은 본문 영역이 **두 번 잡히는 경우**(같은 문단을 중복 인식하거나, 소제목이
앞뒤 문단 상자에 겹쳐 들어가는 경우)가 있었습니다. 이때 두 번역문이 같은 자리에 겹쳐 그려져
글자가 뒤엉켜 보였습니다.

이제 한 번역 영역이 더 큰 영역 안에 대부분 포함되면, **큰 쪽만 그대로 두고 겹치는 작은 쪽은
다시 그리지 않습니다**(중복 내용은 보통 다른 위치에 이미 정상적으로 들어가 있습니다). 2단
레이아웃이나 정상적으로 떨어져 있는 문단은 전혀 영향을 받지 않습니다.

이미 번역해 둔 문서도 **다시 번역할 필요 없이 "PDF로 저장"만 다시 누르면** 재조판되어 겹침이
사라집니다.

### [1.8.14](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.14)
#### 한글(HWPX)·Word(DOCX) 저장이 멈추지 않습니다

수식이 많은(특히 스캔·OCR) 문서에서 **한글/Word로 저장을 눌러도 한참 멈춰 있던 문제**를 고쳤습니다.
저장할 때 수식 블록마다 그림을 읽어 수식으로 바꾸는 과정이 있는데, 수식으로 잘못 잡힌 블록이 많으면
그 과정이 매우 오래 걸려 멈춘 것처럼 보였습니다.

이제 수식 인식은 **시간 제한(최대 25초)** 안에서만 수행하고, 수식 후보가 너무 많으면 건너뜁니다. 인식
하지 못한 수식은 **원래 그림 그대로** 문서에 들어가며, **저장은 항상 완료**됩니다. 저장 중에는 "문서
파일로 변환 중…" 표시가 보입니다.

#### 번역하지 않고도 한글·Word로 저장

문서를 연 뒤 번역하지 않아도 **"번역 없이 저장"** 으로 PDF 를 편집 가능한 한글(HWPX)·Word(DOCX)
문서로 바로 저장할 수 있습니다. 원문 그대로 흐름 문서로 변환되며, 이때 **수식은 그림 형태로** 그대로
들어갑니다(번역이 없으므로 수식 인식은 생략). 문서 길이·수식 개수와 무관하게 즉시 저장됩니다.

## 라이선스 · License

**개발:** Minho Kwon ([@mikwon3](https://github.com/mikwon3)) · mikwon@me.com · © 2026 Minho Kwon

PaperKo 는 **GNU Affero General Public License v3.0 (AGPL-3.0)** 으로 배포합니다
(전문 [LICENSE](LICENSE)). 전체 소스는 [mikwon3/PaperKo](https://github.com/mikwon3/PaperKo)
에서 받을 수 있습니다. 함께 담긴 제3자 구성요소는 [NOTICE.md](NOTICE.md) 를 참조하세요.
