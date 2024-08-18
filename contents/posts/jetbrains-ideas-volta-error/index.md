---
title: "IntelliJ IDEA Volta 인터프리터 에러 해결하기"
description: ""
date: 2024-08-15
update: 2024-08-15
tags:
  - IDE
series: 
---

IntelliJ IDEA 2024.2가 정식으로 출시됐다. 업데이트된 여러 기능 중 'TypeScript 파일을 직접 실행 및 디버그'가 가장 흥미로웠다. 바로 업데이트하고 실행했을 때 문제가 발생했다.

```shell 
node:internal/modules/run_main:129
    triggerUncaughtException(
    ^
Error: tsx must be loaded with --import instead of --loader
The --loader flag was deprecated in Node v20.6.0 and v18.19.0
``` 

문제는 `Volta` 환경에서만 발생했다. 해결하기 위해서는 표준 `Node.js` 인터프리터를 사용해야 한다.

> `Volta`는 Package Manager 도구 중 하나다. 여러 `Node.js` 버전을 관리할 때 유용하다. `Volta` 외에도 `nvm`, `fnm`등이 있다.
> Java에서 사용하는 `jenv`와 유사하다.

## Volta 제거하기

> macOS, zsh 환경에서 진행한다.

1. `rm -rf ~/.volta`: 바이너리를 제거한다.

```shell
export VOLTA_HOME="$HOME/.volta"
export PATH="$VOLTA_HOME/bin:$PATH"
```

2. `vim ~/.zshrc`: 위와 같은 환경 변수를 제거한다.
3. `source ~/.zshrc`: 설정 파일을 다시 불러온다.
4. `volta -v`: 삭제를 확인한다.

## 기능 확인하기

```typescript
const blog = '장태근블로그 devmeeple.github.io';
const thankYou = (blogName: string) => console.log(`${blogName} 클릭해주셔서 감사합니다.`);

thankYou(blog);
```

제거를 마쳤다면, 간단한 프로그램으로 기능을 확인해 보자.

![Thank You!](./thank-you-log.avif)

업데이트가 성공하고 기능이 정상동작함을 확인할 수 있다.


## 마치며

`Volta`를 삭제하면 당장의 문제는 해결할 수 있다. 하지만 다양한 버전을 사용하기 위해서 다른 버전 관리자(Node Version Manager)를 고려해야겠다. 우선 급한 대로 `nvm`을 다시 사용 중이다.

**<참고 자료>**

* [IntelliJ IDEA 2024.2의 새로운 기능](https://www.jetbrains.com/ko-kr/idea/whatsnew/)
* [YoTrack 'Volta Node interpreter version not correctly detected when running Typescript with
  `tsx`'](https://youtrack.jetbrains.com/issue/WEB-67800/Volta-Node-interpreter-version-not-correctly-detected-when-running-Typescript-with-tsx)
* [VOLTA 'Uninstalling Volta'](https://docs.volta.sh/advanced/uninstall)
