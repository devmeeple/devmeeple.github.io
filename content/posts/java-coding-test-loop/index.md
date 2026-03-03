---
title: '코드업(CodeUp) Java 풀이 1071 ~ 1077'
date: '2026-03-03T23:00:41+09:00'
categories: ["코딩 테스트"]
tags: ["CodeUp", "Java", "반복문"]
draft: true
---

## 1071. 0 입력될 때 까지 무한 출력하기1

```java
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            int n = scanner.nextInt();

            if (n == 0) {
                break;
            }
            System.out.println(n);
        }

        scanner.close();
    }
}
```

- `while`, `for`, `do~while` 3가지 선택지 중 `while`문을 사용했다.
- 반복 횟수가 명확하면 `for`문으로 해결하는 방법이 편리하지만 명확하지 않기 때문에 `while`이 적합하다.

### 1. Sentinal Values를 사용하여 개선

```java
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        while (n != 0) {
            System.out.println(n);
            n = scanner.nextInt();
        }

        scanner.close();
    }
}
```

- 무한루프 + `break` 조합이 아닌 `while` 헤더에 종료 조건을 작성하여 코드를 개선할 수 있다.
- 종료 조건이 명확하고 불필요한 `break`문을 사용하지 않아도 흐름을 바로 알 수 있다.
- 스트림/파일 읽기, 네트워크/서버 루프, Iterator기반 반복 등 자주 사용하는 방식이다.

## 1072. 정수 입력받아 계속 출력하기

```java
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int count = scanner.nextInt();
        for (int i = 0; i < count; i++) {
            int number = scanner.nextInt();
            System.out.println(number);
        }

        scanner.close();
    }
}
```

- Scanner는 어떻게 동작할까? (feat. Buffer)

## 1073. 0 입력될 때까지 무한 출력하기2

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int number = scanner.nextInt();
        while (number != 0) {
            System.out.println(number);
            number = scanner.nextInt();
        }

        scanner.close();
    }
}
```

## 1074. 정수 1개 입력받아 카운트 다운 출력하기1

```java
public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int startNumber = scanner.nextInt();
        for (int current = startNumber; current >= 1; current--) {
            System.out.println(current);
        }

        scanner.close();
    }
}
```

## 1075. 정수 1개 입력받아 카운트다운 출력하기2

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int current = scanner.nextInt();
        while (current > 0) {
            current--;
            System.out.println(current);
        }

        scanner.close();
    }
}
```

## 1076. 문자 1개 입력받아 알파벳 출력하기

```java
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        char endCharacter = scanner.next().charAt(0);
        for (char current = 'a'; current <= endCharacter; current++) {
            System.out.print(current + " ");
        }

        scanner.close();
    }
}
```

- `for`문에 `char` 사용이 가능한 건 처음 알았다.

## 1077.

```java
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int endNumber = scanner.nextInt();
        for (int i = 0; i <= endNumber; i++) {
            System.out.println(i);
        }

        scanner.close();
    }
}
```

## 마치며

### 참고 자료

- [Understanding Sentinel Values in Java: A Practical Guide](https://www.oreateai.com/blog/understanding-sentinel-values-in-java-a-practical-guide/e5082a625e68c93bc2c9eb0fbe6fb2d8)
