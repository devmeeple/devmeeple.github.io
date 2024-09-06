---
title: "Enum 사용법: 안된다 이넘아"
description: ""
date: 2024-09-06 08:26:55
update: 2024-09-06 08:26:55
tags:
  - JavaScript/TypeScript
series: "금성에서 온 JVM 개발자, 화성에서 온 Node.js" 
---

TypeScript에서는 'Enum'을 주제로 파이트 클럽이 가능하다. 문서를 보고 배움에서 끝나지 않고 실무에서 사용하는 개발자분들이 특히 그렇다.
다양한 방법으로 사용하거나 사용하지 않는다. 갑론을박을 벌인다. 그렇다면 기본적인 사용방법은 무엇이고, 어떤 방법으로 사용할 수 있는지, 무엇이 문제인지 알아보자.

- 기본기
- 사용방법과 문제점
- 파이트 클럽, 갑론을박

## Enum

- 다른 언어에서는 Enum을 흔하게 접할 수 있다. 하지만 JavaScript에서는 제공하지 않는다. TypeScript에서 확장해서 사용한다.

```text
- DONE: 요청 완료 상태
- ERROR: 에러가 발생
- LOADING: 로딩 상태
- INITIAL: 초기 상태
```

## 마치며

> 은총알은 없다(No Sliver Bullet)

Enum을 가장 잘 사용하는 방법은 다른 기술을 선택하는 것과 같다. 상황에 맞게 능동적으로 선택하는 요령이 중요하다.
상황에 맞춰서 선택하는 방법을 기르자.

**<참고 자료>**

- [The TypeScript Handbook 'Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [『이펙티브 타입스크립트』(댄 밴더캄, 인사이트, 2021)](https://product.kyobobook.co.kr/detail/S000001033114)
- [향로 '기억보단 기록을'](https://jojoldu.tistory.com/621)
