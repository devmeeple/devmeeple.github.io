---
title: 'final'
date: '2026-03-12T23:46:02+09:00'
categories: ["Java"]
tags: ["java", "final keyword", "constants"]
series: ["Java에서 살아남기"]
draft: true
---

- final 변수와 상수1
- final 변수와 상수2
- final 변수와 참조

## 마치며

- `static`을 설명할 때 메모리 구조를 학습한 점이 빛을 발했다. 왜 Java에서 상수를 선언할 때 `static final`을 사용하는지 명쾌하게 이해했다.
- `final`이 가장 헷갈리는 부분은 참조형이다. 참조형은 객체 필드의 실제 값이 아닌 참조할 수 있는 주소, 참조값을 갖고 있다. 따라서 참조값으로 객체 필드의 값을 변경할 수 있다.
- `final`을 사용하면 값을 변경할 수 없다는 말은 재할당이 불가능하다는 말과 같은 의미다. 
