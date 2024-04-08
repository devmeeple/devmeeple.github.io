---
title: "[ERR_REQUIRE_ESM] 에러 해결하기"
date: 2024-04-08
update: 2024-04-08
tags:
  - 개발환경
---

TypeScript + Express + Yarn 환경으로 프로젝트 구성 중 에러가 발생했습니다.

```shell
yarn run v1.22.19
$ jest
Error [ERR_REQUIRE_ESM]: require() of ES Module...
```

## 해결방법

```shell
yarn cache claen
```

1. 캐시를 비워줍니다.
2. `node_modules` 디렉터리와 `yarn.lock` 파일을 삭제합니다.
3. `yarn`: 삭제한 패키지를 재설치합니다.

다음과 같은 순서로 에러를 해결했습니다. 특정 패키지의 문제인 줄 알았지만 이는 버전 호환 문제로
빈번하게 발생하는 에러입니다.
