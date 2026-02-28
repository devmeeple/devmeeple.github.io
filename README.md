# 장태근블로그

- Hugo 기반으로 운영하는 개인 기술 블로그
  - [blowfish theme](https://github.com/nunocoracao/blowfish) 사용
- 학습 기록과 실험, 시행착오

## Hugo 블로그 운영 가이드

- Hugo
- Git

Hugo와 Git이 반드시 필요하다.

- 패키지 관리자 Homebrew를 사용하여 Hugo 설치

```shell
brew install hugo
```

### 기본 디렉터리 구조

```text
config/_default/
├─ hugo.toml
├─ languages.ko.toml
├─ markup.toml
├─ menus.ko.toml
├─ module.toml  # if you installed using Hugo Modules
└─ params.toml
```

- `hugo.toml`: 사이트 설정 핵심 파일
- `languages.ko.toml`: 언어별 설정 지원
- `menus.ko.toml`: 언어별 메뉴 설정
- `params.toml`
  - `colorSheme`: 테마 색상 변경
- [Configuration](https://blowfish.page/docs/configuration/)

### 명령어

```shell
hugo server
```

- `draft`(초안) 제외
- 배포 환경과 동일

```shell
# hugo server --buildDrafts
hugo server -D
```

- `draft: true` 글 포함
- 발행하기 전 초안 작성에 사용

### 글 작성

```shell
# hugo new content posts/[게시글 디렉터리]/index.md
hugo new content posts/retrospective-2026/index.md
```

- 게시글 작성

#### Front Matter

**기본 템플릿**

```shell
title: '게시글 제목'
date: 2026-03-01
categories: ["목차"]
tags: ["태그1", "태그2"]
draft: true
```

- title: 게시글 제목
- date: 게시글 작성 일자, `2026-03-01T00:00:00+09:00` 형태로 작성이 가능하나 생략 가능, Raycast Snippets 사용
- categories: 목차
- tags: 태그
- draft: 초안, 발행 시 `false`로 변경 또는 생략 가능

**개인 설정**

- lastmod: 게시글 수정 날짜
- series

### 배포

- GitHub Pages를 사용하여 배포 진행
- GitHub main 브랜치에 `push` 하면 자동으로 작업 시작, 
  - `.github/workflows/gh-pages.yml` -> `(결과) gh-pages 브랜치`
- [Hosting & Deployment](https://blowfish.page/docs/hosting-deployment/)

### 테마 업데이트

```shell
git submodule update --remote --merge
```
