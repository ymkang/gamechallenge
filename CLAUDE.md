# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

제4회 TU 게임 챌린지 2026 대회 공고용 리포지토리. 두 가지 산출물이 있다:
1. **`index.html`** — 단일 파일 공고 홈페이지 (CSS/JS 인라인, 외부 의존성 없음)
2. **`latex/main.tex`** — 공식 인쇄용 공고문 (XeLaTeX)

공고 원본은 `4회 게임챌린지_공모전공고문.pdf` (및 .hwpx)이며, 홈페이지와 LaTeX 문서 모두 이 원본의 내용을 정확히 반영해야 한다.

## Architecture

### `index.html` (~1200줄, 단일 파일)
CSS 변수(`--primary`, `--secondary` 등)로 테마 관리. 주석 `<!-- ====== 섹션명 ====== -->`으로 구분된 섹션 구조:
- 헤더 → 내비게이션 → 대회 소개(`#about`) → 일정(`#schedule`) → 참가 트랙(`#tracks`) → 시상 내역(`#prizes`) → 접수 방법(`#submit`) → G-STAR 갤러리(`#gallery`) → 문의(`#contact`) → 푸터
- `<script>` 블록: 갤러리 라이트박스 JS (키보드 탐색 지원)
- `images/` 디렉토리의 G-STAR 2025 부스 사진을 배경 및 갤러리에 사용

### `latex/main.tex` (~460줄)
XeLaTeX + `kotex` 기반. `tcolorbox`로 5가지 커스텀 박스 스타일 정의:
- `titlebanner` — 표지 타이틀 배너
- `infocard` — 섹션 내 정보 카드
- `highlightbox` — 강조 박스 (접수 안내 등, 왼쪽 빨간 보더)
- `ieeebox` — IEEE 트랙 전용 강조 박스 (왼쪽 파란 보더)
- `trackheader` — 트랙 소제목 박스

폰트: **KoPubDotum** (Light/Medium/Bold). 색상 팔레트는 파일 상단 `\definecolor`에 정의.

## Build Commands

### LaTeX 공고문 컴파일
```bash
cd latex
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex  # 2회 실행 (페이지 참조 해결)
```
- MiKTeX + XeLaTeX 환경
- 시스템에 KoPubDotum 폰트 설치 필요 (Light, Medium, Bold)

### 홈페이지 미리보기
정적 HTML이므로 `index.html`을 브라우저에서 직접 열면 된다.

## Key Conventions

- **양쪽 동기화 필수**: 대회 정보(일정, 상금, 트랙, 접수 링크 등)를 변경할 때는 반드시 `index.html`과 `latex/main.tex` 양쪽 모두 업데이트해야 한다.
- 커밋 메시지는 한국어, prefix 사용: `feat:`, `update:`, `design:`, `fix:`, `add:`
- 트랙 체계: 트랙 1-A (게임 콘텐츠 시스템), 트랙 1-B (게임그래픽), 트랙 2 (IEEE 부산섹션)
- Remote: `origin` → `https://github.com/ymkang/gamechallenge.git`, branch `main`
