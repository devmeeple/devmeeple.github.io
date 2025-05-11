---
title: "3장. 문법의 탄생"
description: ""
date: 2025-05-05 09:00:00
update: 2025-05-05 18:00:00
tags:
  - 개발환경
series: "코딩을 지탱하는 기술" 
---

> 이 글은 『코딩을 지탱하는 기술』을 읽고 생각과 지식을 덧붙여 정리했다. 책 내용과 100% 일치하지 않기 때문에 자세한 내용은 원문 참고를 권장한다.

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6Rqn2GFlmvmV4w9Ala0I1e?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

## 3.1 문법이란

문법이란 언어 설계자가 정한 규칙이다. 문제를 바라보고 해결하는 사고방식에 영향 준다.

## 3.2 스택 머신과 Forth

```text
1 2 +
```

- 1958년 개발된 FORTH는 문법이 거의 존재하지 않는 언어다.
- 계산 흐름을 명시적으로 표현하며, 스택 머신 개념을 확장시켰다. 
- JVM(Java Virtual Machine)과 같은 가상 머신도 내부적으로 스택을 사용한다.
- NASA 우주 탐사 프로젝트[^1]에 활용했다. 

## 3.3 구문 트리와 Lisp

```
(+ 1 2)
```

- 1958년 개발된 LISP는 코드를 구문 트리 구조 그대로 표현한다.
- Garbage Collection을 최초 도입했다.
- 일급 함수형 프로그래밍의 핵심 개념[^2] 대중화에 기여했다.
- JavaScript의 프로토타입 기반에 간접적으로 영향을 끼쳤다.

## 마치며

다양한 프로그래밍 언어들이 사실 깊이 연결되어 있음을 느꼈다. Forth와 Lisp를 중심으로 다뤘지만, Smalltalk나 Self 같은 언어들이 어떻게 영향을 주고받았는지 살펴봤다.

[^1]: https://www.forth.com/resources/space-applications/
[^2]: 일급 함수(First-class Function), 클로저(Closure), 불변성(Immutable)