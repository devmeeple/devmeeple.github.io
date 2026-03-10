---
title: '기본형과 참조형(Primitive vs. Reference Types)'
date: '2026-03-10T10:34:57+09:00'
categories: ["Java"]
tags: ["java", "java-basic", "primitive-type", "reference-type", "type-system"]
series: ["Java에서 살아남기"]
draft: true
---

- 기본형 vs 참조형1 - 시작
- 기본형 vs 참조형2 - 변수 대입
- 기본형 vs 참조형3 - 메서드 호출
- 참조형과 메서드 호출 - 활용
- 변수와 초기화
- null
- NullPointerException
- 질문
  - 참조형은 왜 중요할까? 꼭 이해해야 하는 이유
  - 참조형과 포인터의 관계
  - pass by value vs. passy by reference
  - copy by value
  - 웹 애플리케이션에서 발생하는 문제
    - 공유변수
    - 싱글톤
  - 다른 언어는 어떻게 사용할까
  - 클래스 변수
  - `null`을 왜 만들었을까, 10억짜리 실수, GC를 사용하지 않는 언어의 처리 방법

## 개념

- Java의 자료형은 기본형과 참조형으로 분류한다.
- 기본형(Primitive Type)
  - `int`, `long`, `boolean` 처럼 소문자로 시작한다. 변수에 사용할 값을 직접 대입한다.
  - Java에서 기본으로 제공한다. 새로 정의할 수 없다.
- 참조형(Reference Type)
  - `String`[^1], `User`, `Product`와 같이 데이터에 접근하기 위한 참조(주소)를 저장한다.
  - 객체와 배열이 해당한다.
  - 객체는 실제 값에 접근하기 위해 `.`(dot operator)를 사용한다.
  - 배열은 `[]`(square bracket)을 사용한다.

## 마치며

[^1]: 문자열은 매우 자주 사용하는 자료형이다. Java에서 기본으로 제공함에도 불구하고 특별 대우를 받아 참조형에 해당한다.
