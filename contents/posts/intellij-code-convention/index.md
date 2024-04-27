---
title: "IntelliJ Code convention 적용하기"
description: ""
date: 2024-04-27
update: 2024-04-27
tags:
  - IDE
series: 
---

코드 컨벤션을 지키면서 어떻게 프로그래밍할 수 있을까요? IntelliJ에서 코드 컨벤션을 적용하는 방법을 알아봅시다.

> [네이버 캠퍼스 핵데이 Java 코딩 컨벤션](https://github.com/naver/hackday-conventions-java/blob/master/rule-config/naver-intellij-formatter.xml)

## 적용하기

![Settings -> Editor -> Code Style -> Java](./images/naver-convention.png)

1. 다운로드한 컨벤션을 import 합니다.
2. 스키마의 이름을 설정합니다. 다양한 컨벤션을 적용하는 상황에는 유의미한 이름을 권합니다.

> 만약 IDE 설정이 아닌 일부 프로젝트에 적용하고 싶다면 Default가 아닌 Project를 선택하세요.

## 추가 설정

자동으로 컨벤션이 적용될 수 있도록 추가설정을 하겠습니다.

![Settings -> Tools -> Action on Save](./images/action-on-save.png)

- Reformat code: 자동으로 포맷 적용
- Optimize imports: 사용하지 않는 import 제거

자동으로 포맷이 적용되고 사용하지 않는 import를 제거하도록 적용했습니다.

## 함께 자라기

- [Code convention과 개발자가 지켜야할 수칙에 관하여](https://novemberde.github.io/post/2017/05/21/Javascript_policy/)
