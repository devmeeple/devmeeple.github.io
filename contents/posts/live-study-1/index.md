---
title: "JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가"
description: ""
date: 2025-04-13 16:50:00
update: 2025-04-13 18:00:00
tags:
  - Java/Kotlin
series: "스터디 할래? 온라인 자바 스터디"
---

## 목표

- 자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기

## 목차

- JVM이란 무엇인가
- 컴파일 하는 방법
- 실행하는 방법
- 바이트코드란 무엇인가
- JIT 컴파일러란 무엇이며 어떻게 동작하는지
- JVM 구성 요소
- JDK와 JRE의 차이

## JVM이란 무엇인가

JVM(Java Virtual Machine)은 자바 프로그램을 실행하기 위한 가상 머신이다. 작성한 코드, 즉 소스 코드를 기계가
이해할 수 있는 코드로 변환하여 프로그램을 실행할 수 있도록 돕는다. 핵심 가치인 'WORA(Write Once, Run Anywhere)[^1]'를 제공한다.

## 컴파일 하는 방법

```shell 
javac HelloWorld.java 
``` 

자바 소스 파일(.java)은 `javac` 명령을 통해 컴파일된다. 명령을 실행하면 바이트 코드를 담은 `.class`파일을 생성한다.

```shell 
kotlinc HelloWorld.kt -inclunde-runtime -d HelloWorld.jar 
``` 

코틀린은 `kotlinc`명령을 통해 컴파일하며, 동일한 `.class`파일을 생성한다.

## 실행하는 방법

```shell
java HelloWorld
```

생성된 `.class`파일은 `java`명령을 통해 실행한다.

```shell
java -jar HelloWorld.jar
```

코틀린은 보통 생성된 `JAR`를 실행한다. 

## 바이트코드란 무엇인가

바이트코드(Bytecode)는 소스 코드를 컴파일한 결과물이며, JVM이 이해하고 실행할 때 사용한다.

## 마치며 

[^1]: 한 번 작성하면 어디서든 실행 가능