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

| 운영체제 | 최신 설치본 (1.8.13) |
|---|---|
| **macOS** 12+ (Apple Silicon) | **[⬇ PaperKo-1.8.13-arm64.dmg](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.13/PaperKo-1.8.13-arm64.dmg)** |
| **Windows** 10+ x64 | **[⬇ PaperKo-1.8.13-amd64-installer.exe](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.13/PaperKo-1.8.13-amd64-installer.exe)** |

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

### [1.8.13](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.13)
#### macOS 설치본이 실제로 최신 번역 엔진을 싣습니다 (중요)

1.8.11 · 1.8.12 의 macOS 설치본은 앱 버전만 올라갔을 뿐 **안에 들어간 번역 엔진은 1.8.10 그대로**였습니다.
빌드가 번들된 Python 엔진을 소스에서 새로 설치하지 않고 예전 것을 재사용했기 때문입니다. 그래서 그 두
판에서 **번역 관련 수정이 실제로는 적용되지 않았습니다.** (Windows 설치본은 매번 엔진을 새로 담아 영향이
없었습니다.)

이 판부터 macOS 빌드는 **매번 최신 엔진을 다시 담습니다.** 그 결과 아래 수정이 이제 실제로 동작합니다:

- **짧은 문장 조각·목록 이어지는 항목**이 영어로 남던 문제 — 조각 전용 재시도로 복구 (1.8.12 의도).
- **글꼴이 깨져 글자가 암호처럼 추출되는 페이지**를 감지해 OCR 로 다시 읽기 (1.8.11 의도).

> macOS 사용자는 이 판으로 올리면 번역 엔진까지 실제로 최신이 됩니다. 업데이트 후 그 문서를 **처음부터
> 다시 번역**하면 이전에 영어로 남던 블록들이 번역됩니다. (가로로 회전된 표는 OCR 원문이 깨져 있어 여전히
> 번역되지 않을 수 있으며, 이는 회전되지 않은 원본 PDF 가 필요합니다.)

### [1.8.12](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.12)
#### 짧은 문장 조각이 번역에서 빠지지 않습니다

긴 문서에서 **짧은 문장 조각이나 목록 이어지는 항목**(예: `c) longitudinal and transverse ...`,
`members, and ...;`)이 **영어 그대로 남던 문제**를 고쳤습니다. 이런 조각은 문맥 없이 단독으로 번역
모델에 주어지면 모델이 "이미 괜찮다"고 보고 그대로 돌려주거나, 추론형 모델에서는 숨은 추론에 예산을
다 써 빈 응답을 내놓곤 했습니다.

이제 이런 블록을 **"조각이라도 반드시 번역하라"는 지시와 넉넉한 토큰으로 한 번 더 재시도**합니다. 절
제목에만 있던 재시도를 본문 문단에도 적용한 것으로, 재번역해도 고쳐지지 않던 블록들이 복구됩니다.

> **참고:** 스캔/OCR 문서에서 **가로로 회전된 표**는 OCR이 글자를 뒤집어 읽어(예: `used on project`
> → `yafoid uo pasn`) 원문 자체가 판독 불가능할 수 있습니다. 이런 블록은 원문을 읽을 수 없어 번역되지
> 않으며, 지어내지 않고 원문을 그대로 둡니다. 회전되지 않은 원본 PDF를 쓰는 것이 가장 좋습니다.

## 라이선스 · License

**개발:** Minho Kwon ([@mikwon3](https://github.com/mikwon3)) · mikwon@me.com · © 2026 Minho Kwon

PaperKo 는 **GNU Affero General Public License v3.0 (AGPL-3.0)** 으로 배포합니다
(전문 [LICENSE](LICENSE)). 전체 소스는 [mikwon3/PaperKo](https://github.com/mikwon3/PaperKo)
에서 받을 수 있습니다. 함께 담긴 제3자 구성요소는 [NOTICE.md](NOTICE.md) 를 참조하세요.
