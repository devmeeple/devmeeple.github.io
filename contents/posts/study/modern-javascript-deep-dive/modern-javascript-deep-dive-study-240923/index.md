---
title: "자바스크립트 기초 3주차 회고"
description: ""
date: 2024-09-23 22:07:00
update: 2024-09-23 22:07:00
tags:
  - JavaScript/TypeScript
series: "모던 자바스크립트 Deep Dive"
---

이른 추석을 보냈다. 2주차는 온라인 토론으로 대신했다.
무려 2주라는 시간동안 객체 리터럴, 원시 값과 객체의 비교에 대해 생각할 시간을 가졌다.

## 참여

- 도은
- 승주
- 이예지
- 장종현
- 장태근
- 진

## 문제

- 심벌 유일한 값
- 옵셔널 체이닝, 타입 추론

- 이예지: 메모리 관점에서원시 값은 왜 불변한가?
- 장태근: 객체 생성과 불변객체
- 도은: 성능차이
- 장종현: 값에 의한 전달 -> heap
- 진: 생성자, 클래스 육안으로 봤을때는 유사하다.

### 이예지

> 변수가 참조하던 메모리 공간의 주소가 변경된 이유는 변수에 할당된 원시 값이 변경 불가능한 값이기 때문이다.

## 불변 객체

- 불변 객체란 무엇인가?
- 불변 객체를 생성하는 방법
    - `Object.freeze()`: 중첩 객체는 수정 가능하다.
    - Spread 문법과 `const`: 기존 객체를 복사한 후 수정된 값을 새로운 객체로 반환한다. 중첩 객체는 수정 가능하다.
    - `Immutable.js` 라이브러리 사용하기
- 학습 테스트로 만나는 불변 객체, 어떤 상황에 적용하면 좋을까

불변 객체란 생성후 상태를 변경할 수 없는 객체를 의미한다. 객체는 변경 가능(mutable)하다. [원시 타입은 불변하다.]
변경 가능한 점이 때로는 사이드 이펙트를 초래한다. 예상할 수 없는 사이드 이펙트는 퇴근시간을 늦춘다.
문제를 해결하기 위해 불변성(immutability)을 적용한다.
불변 객체는 한 번 생성하면 수정할 수 없다.

### 사실과 오해

- `const` 키워드는 값을 재할당할 수 없다는 의미다. 참조형인 배열, 객체는 값을 변경할 수 있다.
- `Object.freeze()`는 얕은 복사만 해당한다. 중첩 객체는 수정 가능하다.
- `Spread` 또한 얕은 복사다. 새로운 객체를 생성한다.
- 배열은 불변 메서드와, 가변 메서드가 있다.

## 참고

- [/dev/solita '
  Writing Immutable JavaScript in 2022'](https://dev.solita.fi/2022/04/25/javascript-immutability.html)
- [TOAST UI '불변 객체와 immer'](https://ui.toast.com/posts/ko_20220217)
- [벨로퍼트 '23. Immer 를 사용한 더 쉬운 불변성 관리'](https://react.vlpt.us/basic/23-immer.html)

## 객체

- 객체를 만드는 다양한 방법

- 종현: `new`로 객체를 생성한다. `new Object()` 사용

### 도은

- 성능차이: 미미하다.
- 속성에 많이 접근해야 할 경우, 중첩객체 접근하는 방식이 원시값으로? 객체에 참조참조?

중첩 객체를 여러번 다룰 때는 선언해서 써라.

### 진

- 생성자, 클래스 육안으로 봤을때는 유사하다.

프로토 타입을 이야기해야 해서.

### 승주

- 중첩 객체, 코어 자바스크립트
- 얕은 복사, 깊은 복사

### 장종현

> (142쪽) 값에 의한 전달, heap

## 마치며

미루는 습관을 조심해야겠다.
