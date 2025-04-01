---
title: "2025-03-31 계속 웃을 순 없어!"
description: ""
date: 2025-03-31 05:00:00
update: 2025-03-31 23:30:00
tags:
  - 회고/일간
  - Kotlin/코틀린
  - HTTP
  - 독서
series: "일간 장태근" 
---

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/6ZPIZDuCF5qcVZIcKgifRN?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

웃음 참기 실패!

## Kotlin

```kotlin
// Long 타입 추론
val numL1 = 10L
val numL2 = 12345678912345
val numL3 = 100_000_000_000
```

- 숫자 끝에 `L`을 붙이면 `Long` 타입으로 추론한다. 또는 `Int`의 표현 범위[^1]를 넘으면 정수 리터럴을 `Long`으로 추론한다.
- 숫자에 언더바를 사용할 때는, 뒤에서부터 3자리씩 나눠 사용하는 것이 가독성에 좋다.
- [Numbers](https://kotlinlang.org/docs/numbers.html)

## HTTP

- 초기, 개인 컴퓨터가 보급됐지만 서로의 해답을 공유할 수 없었다.
- 1991년, 월드와이드웹(www)의 창시자 '팀 버너스 리'는 **서로 각기 다른 사람들의 생각을 모아 하나의 해답을 만들기 위해 웹이 등장했다.** 완벽하진 않았지만 완벽에 가까웠다.
- HTTP는 무상태(stateless) 프로토콜이다. 간단한 요청을 주고받기 위해 무상태로 설계했다. 요청과 응답을 서버가 알고 있지 않기 때문에 확장성이 좋다.
- 무상태에서 로그인은 어떻게 이뤄질까? 간단한 HTTP에서 새로운 기술이 필요했다. 세션과 쿠키가 등장했다.
- [[SDF2013] '팀 버너스 리'가 월드와이드웹(www)을 만든 이유]((https://www.youtube.com/watch?v=1OTsLkvPwH8))
- [1991년, 인터넷의 발명과 인터넷 브라우저 전쟁](https://www.youtube.com/watch?v=taJV5cigzNY)

## 정재승의 과학 콘서트

꾸글 글쓰기 스터디에 나눌 이야기를 미리 정리했다.

### 책속으로

> 어떤 물리학자는 로키 산맥에 줄지어 선 산봉우리들의 높낮이를 소리로 변환하여 아주 그럴듯한 음악을 작곡하기도 했다. 그래서 컴퓨터 음악을 전공하는 사람들 중에는 **자연의 패턴을 음악으로 변환하여 작곡하는 경우도 늘어났는데, 이런 장르를 '프랙털 음악(fractal music)'이라고 부른다.**
> -127쪽

>  앞서 설명했듯이 작은 구조가 전체 구조와 유사한 형태로 되풀이 되는 구조를 '프랙털'이라고 한다. (...) 프랙털은 자연이 만들어낸 가장 중요한 내재적인 특징 중의 하나이며 우리는 그속에서 아름다움을 느낀다고 물리학자들은 믿고 있다. 바흐가 작곡한 음악의 악보를 자세히 들여다보면 음표둘의 분포가 매우 질서 정연하며, 전체 패턴이 하나의 악절, 심지어는 한 마디 안에서 유사한 구조가 되풀이 되는 것을 발견할 수 있다.
>  -133쪽 ∼ 134쪽

- [부분과 전체가 동일한 모양으로 끊임없이 반복되는 프랙탈 구조 / YTN 사이언스](https://www.youtube.com/watch?v=bGhKj01mCLY)

## 마치며 

- 아생연후살타, 나에게 주어진 문제를 해결하고 주위를 둘러보자.
- 남아있는 돈을 확인한 결과, 소비습관을 정비하고 잡다한 생각이 사라졌다. 당장 해야 할 일을 하자.

### 오늘의 함께 읽기

- [더이상 웹을 탐험하지 않는 시대](https://mag.surfit.io/the-end-of-web-exploration/): 조화가 중요하다고 느꼈다. 개인적으로 직접 검색하고, 개요를 전혀 모르는 지식만 AI의 도움을 받고 있다.
- [시간 절약해주는 무료 아이콘 사이트](https://brunch.co.kr/@mobiinside/5383): 픽토그램을 사용해 생활코딩 방식으로 글을 작성할 수 있다.
- [『해커, 광기의 랩소디(복간판)』(스티븐 레비, 한빛미디어, 2019)](https://product.kyobobook.co.kr/detail/S000001810147): 해커정신의 흥망성쇠
- [김영한의 실전 자바 로드맵 소개](https://www.youtube.com/watch?v=mcD_lLViQqw): 문법을 넘어 깊이를 다루는 강의
    - **백문이 불여일타**
    - 예제를 꼭 따라 하세요. 명심하세요.
    - 이해가 잘 되지 않아도 처음에는 쭉 따라 하며 익숙해지세요.
    - 돌아와서 복습하며 정리하세요. 권장드립니다.
- [튜링의 사과 '아르코 의자'](https://office.hyundailivart.co.kr/p/P200188609)
- [카일 스쿨 '글또 1~10기. 7년의 커뮤니티 운영 회고'](https://zzsza.github.io/diary/2025/03/30/geultto-operation-retrospective/): 꾸글에 참고하기 좋은 자료, 전문 리뷰어가 가장 흥미롭다.
- [안 보면 강의만 쌓인 개발자가 가질 공부법](https://www.youtube.com/watch?v=XO-r1PFCf3U&t=8s): 불안을 뒤로하는 방법
    - 지금 당장 해야 할 문제를 탐색하고 실천한다.
    - 포기를 하는 순간 핑계를, 할 수 있다고 다짐하는 순간 방법을 찾는다.

[^1]: -2,147,483,648 (2의 31승)
