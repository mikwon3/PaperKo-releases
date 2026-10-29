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

| 운영체제 | 최신 설치본 (1.8.17) |
|---|---|
| **macOS** 12+ (Apple Silicon) | **[⬇ PaperKo-1.8.17-arm64.dmg](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.17/PaperKo-1.8.17-arm64.dmg)** |
| **Windows** 10+ x64 | **[⬇ PaperKo-1.8.17-amd64-installer.exe](https://github.com/mikwon3/PaperKo-releases/releases/download/v1.8.17/PaperKo-1.8.17-amd64-installer.exe)** |

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

### [1.8.17](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.17)
#### 한글(.hwpx)로 내보낸 문서에 엉뚱한 "책갈피"가 따라오던 문제 수정

번역 결과를 **한글 문서(.hwpx)로 내보낼 때**, 문서 안에 전혀 관계없는 **책갈피(북마크)**가
딸려 들어가 한글의 책갈피 목록에 엉뚱한 이름(예: `asad-v1.2-사용자-매뉴얼`, `ubuntu-24.04-설치`)이
뜨던 문제를 고쳤습니다.

내보내기에 쓰는 **뼈대(skeleton) 파일**이 한컴으로 만든 실제 문서라, 그 문서의 책갈피 88개가
그대로 들어 있었습니다. 변환기가 뼈대의 문단을 **틀(template)로 복사**해 쓰는 과정에서 이 책갈피가
만들어진 모든 .hwpx 로 따라붙었습니다(두 문단짜리 문서에서도 2개가 보였습니다).

이제 뼈대를 읽어들인 **직후** 책갈피를 모두 걷어낸 뒤 틀 복사를 시작합니다. 책갈피를 이루는
`fieldBegin`–`fieldEnd` 짝과 빈 껍데기까지 함께 제거해, 한글이 "손상된 문서"로 보고 복구를
시도하는 일도 없습니다. 본문 텍스트는 **한 글자도 바뀌지 않습니다**. 사용자가 **직접 올린 뼈대**를
쓸 때도 똑같이 정리됩니다.

### [1.8.16](https://github.com/mikwon3/PaperKo-releases/releases/tag/v1.8.16)
#### 번역본의 글자 크기가 더 고르게 보입니다

재조판(번역본 PDF 만들기) 단계에서 **본문 일부 줄이 주변보다 크게 찍혀 글자 크기가 들쭉날쭉해
보이던 문제**를 고쳤습니다.

문서 분석이 본문 한 줄을 "제목"으로 잘못 분류하는 경우가 있었습니다(특히 줄마다 줄번호가 붙는
저널 교정본에서 각 줄이 따로 잡히는 경우). 이렇게 잘못 잡힌 줄은 제목처럼 12~30% 크게 찍혀 주변
본문과 어긋나 보였습니다.

이제 "제목"으로 잡혔더라도 **실제로는 본문인 줄**(여러 줄에 걸친 문단, 긴 문장, 쉼표로 이어지거나
"~다"로 끝나는 서술문)은 **본문 크기로 통일**해 찍습니다. 반대로 진짜 제목(짧은 표제, `2.1`·
`3.1.1` 같은 절 번호, `표/그림` 캡션)은 그대로 조금 크게 유지됩니다. 글자 크기의 신뢰도가 낮은
스캔·OCR 문서에서도 안전하게 동작하도록, 글자 크기 값이 아니라 블록의 모양과 문구로 판단합니다.

#### 2단 논문에서 번역문이 겹쳐 보이던 문제 수정

2단으로 조판된 학술지 PDF(줄번호가 붙은 Elsevier 형식 등)에서 **번역문 몇 줄이 겹쳐 찍히던
문제**를 고쳤습니다. 세 가지 원인을 함께 바로잡았습니다.

- **단(column) 인식 오류** — 페이지에 폭이 넓은 표나 그림 설명이 몇 개 있으면, 분석기가 2단을
  1단으로 잘못 보고 좌·우 단의 읽기 순서가 뒤섞였습니다. 이제 가운데를 가로지르는 넓은 요소와
  쪽번호는 단 판별에서 제외합니다.
- **수식이 섞인 문단의 분리** — 분수·아래첨자·위첨자(`f'_c`, `l_d/d_b` 등)가 든 줄은 PDF가
  내부적으로 겹치는 두 조각으로 쪼개어, 두 번역문이 같은 자리에 찍혔습니다. 이제 앞 문단 안쪽에서
  시작하는 조각을 하나로 다시 이어 붙입니다.
- **이웃 영역을 뚫고 늘어나던 번역문** — 번역문이 들어갈 칸을 넓힐 때 바로 아래 영역을 지나쳐
  그 위에 겹쳐 그리던 문제를 고치고, 남는 미세한 겹침은 두 영역 사이 중간선에서 깔끔히 나눕니다.

함께 들어간 1.8.15 의 겹침 방지 개선과 더불어, 겹쳐 찍히던 번역문이 사라집니다. 개선 효과는
**문서를 다시 번역**하거나, 기존 번역본을 **"PDF로 저장"으로 다시 저장**하면 반영됩니다.

## 라이선스 · License

**개발:** Minho Kwon ([@mikwon3](https://github.com/mikwon3)) · mikwon@me.com · © 2026 Minho Kwon

PaperKo 는 **GNU Affero General Public License v3.0 (AGPL-3.0)** 으로 배포합니다
(전문 [LICENSE](LICENSE)). 전체 소스는 [mikwon3/PaperKo](https://github.com/mikwon3/PaperKo)
에서 받을 수 있습니다. 함께 담긴 제3자 구성요소는 [NOTICE.md](NOTICE.md) 를 참조하세요.
