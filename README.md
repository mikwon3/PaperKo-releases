# PaperKo

논문·설계기준·시방서·일반 문서 PDF를 **원본 레이아웃을 유지한 채** 한국어(및 다국어)로 번역하는
데스크탑 앱입니다(macOS · Windows). 번역본을 원문 편집을 살린 **PDF**로 만들고, 편집 가능한
**한글(HWPX)·Word(DOCX)** 로도 저장합니다.

A desktop app that translates academic papers, design codes, and general PDFs into Korean (and other
languages) **while preserving the original layout**, and exports to PDF, Hangul (HWPX), and Word (DOCX)
(macOS · Windows).

**이 저장소는 설치 파일만 배포합니다.** 앱 소스는 [mikwon3/PDF-translator](https://github.com/mikwon3/PDF-translator) 에 있습니다.

## 내려받기 · Download

**[최신 판 받기 · Latest release →](https://github.com/mikwon3/PaperKo-releases/releases/latest)**

| 운영체제 | 파일 |
|---|---|
| macOS 12 이상 (Apple Silicon) | `PaperKo-<판>-arm64.dmg` |
| Windows 10 이상 x64 (Windows 11 에서 확인) | `PaperKo-<판>-amd64-installer.exe` |

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

### [1.8.6](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.6)
빌드·배포 도구 정리 판입니다. **앱 기능·번역 동작은 1.8.5와 동일**하며, 새로 받을 기능 변화는 없습니다.

#### 바뀐 점 (내부)

- 릴리스 스크립트가 발행 후 릴리스 저장소 README 의 "변경 이력"을 자동으로 갱신하도록 정리했습니다.
- 사용하지 않던 Windows MSIX 패키징 경로와 남아 있던 플레이스홀더(회사명) 흔적을 제거했습니다. 배포는
  기존과 같이 NSIS 설치본입니다.

### [1.8.5](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.5)
표기·문서 정리 판(엔진·기능은 1.8.4와 동일).
- 개발자·저작권 표기를 **Minho Kwon (@mikwon3)** · mikwon@me.com · **AGPL-3.0** 으로 통일(앱 정보 및 macOS·Windows 설치본 속성), 부서·소속 항목 정리.
- 검증 저널 6종 추가(문서) — Structures·Journal of Building Engineering(Elsevier), Journal of Structural Engineering(ASCE), Advances in Structural Engineering(SAGE), Earthquake Engineering & Structural Dynamics(Wiley), Journal of Applied Mathematics(Hindawi). 총 8개 발행 계열.

### [1.8.4](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.4)
첫 공개 판.
- **온라인 자동 업데이트** — 시작 시 새 판 확인(하루 1회, 끄기·건너뛰기 가능) 후 서명된 릴리스를 받아 스스로 설치. 릴리스는 Ed25519 서명, 설치본은 SHA-256 으로 검증.
- **AGPL-3.0 공개** — 소스를 [mikwon3/PDF-translator](https://github.com/mikwon3/PDF-translator) 에 공개.
- 레이아웃 보존 번역 PDF, HWPX·DOCX 저장, 일반 문서 배치·이어받기, 다국어, OCR, 원격/로컬(오프라인) LLM.

## 라이선스 · License

**개발:** Minho Kwon ([@mikwon3](https://github.com/mikwon3)) · mikwon@me.com · © 2026 Minho Kwon

PaperKo 는 **GNU Affero General Public License v3.0 (AGPL-3.0)** 으로 배포합니다
(전문 [LICENSE](LICENSE)). 전체 소스는 [mikwon3/PDF-translator](https://github.com/mikwon3/PDF-translator)
에서 받을 수 있습니다. 함께 담긴 제3자 구성요소는 [NOTICE.md](NOTICE.md) 를 참조하세요.
