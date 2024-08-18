---
title: "5. 클린코드 이해하기"
description: ""
date: 2024-05-09 21:57:26
update: 2024-05-09 21:57:26
tags:
  - Java
series: "인프런 워밍업 클럽 - 스터디 BE 1기"
---

![인프런 워밍업 클럽 - 스터디 1기](../images/inflearn-warmup-club-study.png)

5일 차는 클린코드의 개념과 리팩터링을 배웠다. 실제 코드에 적용해 가면서 클린코드와 친해지자.

```java
public class Main {

    public static void main(String[] args) throws Exception {
        System.out.print("숫자를 입력하세요 : ");
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();

        int r1 = 0, r2 = 0, r3 = 0, r4 = 0, r5 = 0, r6 = 0;

        for (int i = 0; i < a; i++) {
            double b = Math.random() * 6;
            if (b >= 0 && b < 1) {
                r1++;
            } else if (b >= 1 && b < 2) {
                r2++;
            } else if (b >= 2 && b < 3) {
                r3++;
            } else if (b >= 3 && b < 4) {
                r4++;
            } else if (b >= 4 && b < 5) {
                r5++;
            } else if (b >= 5 && b < 6) {
                r6++;
            }
        }

        System.out.printf("1은 %d번 나왔습니다. \n", r1);
        System.out.printf("2는 %d번 나왔습니다. \n", r2);
        System.out.printf("3은 %d번 나왔습니다. \n", r3);
        System.out.printf("4는 %d번 나왔습니다. \n", r4);
        System.out.printf("5는 %d번 나왔습니다. \n", r5);
        System.out.printf("6은 %d번 나왔습니다. \n", r6);
    }
}
```

위 예제는 다음과 기능과 요구사항을 가진다.

## 기능

- 숫자를 입력받는다.
- 숫자만큼 주사위를 굴려, 숫자가 몇 번 나왔는지 출력한다.

## 요구사항

- 주사위가 정육면체가 아닌 n면체 일 때 최소한으로 수정하도록 고려하여 코드를 작성하라.

## 리팩터링

리팩터링을 진행할 때 아래 순서로 진행했다.

1. 의미있는 변수명 사용하기
2. 주사위 게임을 실행하는 메인 클래스와 주사위 게임 클래스를 선언하고 분리했다.
3. 입력받기, 굴리기, 출력하기 메서드 구현하기
4. 조합하기 + 출력하기

```java
public class DiceGame {
    private static final int DICE_FACE = 6;

    private final int rolls;
    private final int[] rollCounts;

    public DiceGame(int rolls) {
        this.rolls = rolls;
        this.rollCounts = new int[DICE_FACE];
    }

    public void playGame() {
        countRolls();
        printResults();
    }

    private void countRolls() {
        IntStream.range(0, rolls)
                .map(i -> rollDice())
                .forEach(roll -> rollCounts[roll - 1]++);
    }

    private int rollDice() {
        return (int) (Math.random() * DICE_FACE) + 1;
    }

    private void printResults() {
        IntStream.range(0, rollCounts.length)
                .forEach(i -> System.out.printf("[%d] 은(는) [%d번] 나왔습니다.\n", i + 1, rollCounts[i]));
    }
}
```

```java
public class Main {

    public static void main(String[] args) throws Exception {
        System.out.print("주사위를 몇번 굴릴까요? : ");
        Scanner scanner = new Scanner(System.in);
        int rolls = scanner.nextInt();
        scanner.close();

        System.out.println("==================================");
        DiceGame game = new DiceGame(rolls);
        game.playGame();
    }
}
```

주사위가 정육면체가 아닌 n면체가 되었을 때 DICE_FACE 변수를 수정하면 모두 수정되도록 전역으로 선언했다.

## 마치며

어떤식으로 작성해야 가독성이 좋을지 고려하며 작성했다. 하지만 객체지향 프로그래밍과 함수형 프로그래밍이 능숙했다면 더 가독성 좋은 코드를 작성할 수 있을 것 같다고 느꼈다. 과제를 진행하는 다른 스터디원들은
어떻게 문제를 해결했는지 참고하며 배워야겠다.
