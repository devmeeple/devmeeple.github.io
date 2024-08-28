---
title: "빈 문자열 검증하기"
description: ""
date: 2024-08-19 19:36:33
update: 2024-08-19 19:36:33
tags:
  - JavaScript/TypeScript
series: "학습 테스트로 배우는 JavaScript & TypeScript"
---

프로그래밍 언어를 공부할 때 유명 기본서, 강의, 공식문서 외에도 다양한 방법으로 공부하는 것을 선호한다.
'과거에 정의한 개념'과 '현재 정의한 개념'이 충돌할 수 있다고 생각하기 때문이다. 그리고 고정된 사고를 하고 싶지 않다.
매번 '내가 틀릴 수도 있습니다' 외치며 반복한다.

Java/Spring은 한국어로 된 발표, 기술 블로그 자료를 흔하게 찾아볼 수 있다. 하지만 비교적 TypeScript/NestJS은 한정적이다.
문법은 쉽게 찾아볼 수 있는데 조금 더 깊이 나누고 싶은 주제는 물음표를 남긴다. 특히 테스트가 그랬다.

Java는 테스트를 작성할 때 JUnit을 주로 사용한다. 하지만 JavaScript는 실행 환경에 따라 사용하는 프레임워크가 다르다.
다양한 프레임워크 중 이 시리즈는 NestJS에서 기본으로 사용하는 Jest를 사용한다. [^1]

> 다른 언어를 사용해 봤거나, 테스트를 작성해 봤다면 이해할 수 있도록 난이도를 설정했다.
> 전체 코드는 [GitHub](https://github.com/devmeeple/javascript-in-action/tree/main/test/javacan)에서 제공한다.

## 비밀번호 빈 문자열 검증하기

책[^2]을 읽고 예제를 반복해서 구현했다. 그런데 문제를 만났다. 비밀번호가 빈 문자열인지 검증하는 테스트를 리팩터링 할 때
옵셔널 체이닝(Optional chaining)과 trim() 메서드 개념이 부족하다고 느꼈다.

```javascript
// 1. 명시적으로 빈 문자열을 검증한다. 
if (password === null || password === undefined || password === '') {
  return PasswordStrength.INVALID;
}

// 2. 옵셔널 체이닝(Optional chaining) 활용
if (!password?.trim()) {
  return PasswordStrength.INVALID;
}
```

구현을 먼저 진행할 땐 검증을 명시적으로 하면 된다고 생각했다. 그런데 조금 더 나은 방법은 없을까 고민했다.
검색결과 옵셔널 체이닝과 trim()을 사용했다.

### 옵셔널 체이닝(Optional chaining)

```javascript
it('객체가 존재하면 객체를 반환한다. [성공]', () => {
  // given
  const baseballPlayer = {
    name: '원태인',
  };

  // when
  const sut = baseballPlayer?.name;

  // then
  expect(sut).toBe('원태인');
});

it('객체가 존재하지 않으면 undefined를 반환한다. [실패]', () => {
  // given
  const baseballPlayer = {};

  // when
  const sut = baseballPlayer?.name;

  // then
  expect(sut).toBeUndefined();
});
```

옵셔널 체이닝은 프로퍼티가 없는 중첩 객체를 안전하게 접근할 때 사용한다.
위와 같은 방법으로 사용가능하다.

### trim

trim() 메서드는 공백을 제거할 때 사용한다. 원본 문자열을 수정하지 않고 새로운 문자열을 반환한다.

```javascript
it('문자열의 양쪽 끝 공백을 제거하고 새로운 문자열을 반환한다. [성공]', () => {
  // given
  const poem =
    '   가야 할 때가 언제인가를 분명히 알고 가는 이의 뒷모습은 얼마나 아름다운가.   ';

  // when
  const sut = poem.trim();

  // then
  expect(sut).toBe(
    '가야 할 때가 언제인가를 분명히 알고 가는 이의 뒷모습은 얼마나 아름다운가.',
  );
});
```

### 전체 검증하기

옵셔널 체이닝과 trim()의 사용법을 간단하게 알아봤다. 그렇다면 리팩터링 한 코드를 다시 테스트해보자.

```javascript
describe('PasswordStrengthMeterTest', () => {
  it('유효한 비밀번호를 입력한다. [성공]', () => {
    // given
    const password = '1q2w3e4r';

    // when
    const sut = meter(password);

    // then
    expect(sut).toBe('유효한 비밀번호 입니다.');
  });

  describe('유효하지 않은 비밀번호를 입력하면 에러 메시지를 출력한다. [실패]', () => {
    it.each([null, undefined, ''])(
      '비밀번호 "%s"은(는) 유효하지 않은 비밀번호다.',
      (invalidPassword) => {
        // given

        // when
        const sut = meter(invalidPassword);

        // then
        expect(sut).toBe('유효하지 않은 비밀번호 입니다.');
      },
    );
  });
});
```

![password-strength-meter.spec.js 단위 테스트 실행 결과 <출처: GitHub>](./password-strength-meter-result.avif)

테스트를 실행하면 위와 같은 결과를 얻는다.

## 동작 순서 요약

```javascript
if (!password?.trim()) {
  return PasswordStrength.INVALID;
}
```

정리하면 리팩터링 한 코드는 다음과 같은 순서로 동작한다.

1. `password`가 `null`또는 `undefined`라면 `trim()` 메서드를 실행하지 않고[^1] `undefined`를 반환한다.
2. `password`가 빈 문자열이라면 `password?.trim()`은 빈 문자열 `''`을 반환한다.
3. `!` 연산자는 `undefined`, 빈 문자열, `null`과 같은 `Falsy`값[^2]을 `true`로 변환한다.
4. 조건문이 실행돼서 `PasswordStrength.INVALID`를 반환한다.

> 물론 조건식도 `isPasswordValid()` 메서드로 추가 리팩터링 할 수 있다.

## 마치며

![알게 뭐야 지금 내가 신나는데 <출처: 무한도전>](./excited.avif)

학습 테스트[^5]가 무엇인지 경험하고 글도 작성하니 재밌다. 비록 간단한 테스트지만 이번 기회에 작성하지 않았다면 한참 동안 모르고 지나갈 개념이었다.
부족함을 기본서를 다시 보며 풀어낼까 했는데 문제가 발생할 때마다 이렇게 테스트 코드와 글로 남겨야겠다.

쌓여있는 문서, 이제는 공개할 시간이다. 해방이다.

**<참고 자료>**

- [The Modern JavaScript Tutorial 'Optional chaining](https://javascript.info/optional-chaining)
- [MDN Web Docs 'Optional chaining (?.)'](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
- [MDN Web Docs 'String.prototype.trim()'](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim)

[^1]: [Jest](https://jestjs.io/)
[^2]: [최범균 『테스트 주도 개발 시작하기』](https://product.kyobobook.co.kr/detail/S000001248962)
[^3]: 단락(short-circuit, 혹은 단축) 평가
[^4]: [Mdn Web Docs 'Falsy'](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
[^5]: [이일민(토비) '공부 방법에 대해서 질문드립니다.']https://www.inflearn.com/community/questions/763626
