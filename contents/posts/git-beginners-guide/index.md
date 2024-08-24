---
title: "Git 초보자 가이드"
description: ""
date: 2024-08-24
update: 2024-08-24
tags:
  - Git
series: 
---

Git을 처음 배울 땐 이정도로 자주 사용하는 기술이될지 몰랐다. 회사에서 SVN(Subversion)을 사용했지만 자주 언급하는 이유가 궁금해서 배웠던 기억이 있다.
하지만 지금은 개발을 공부할 때 Git은 빼놓을 수 없는 친구다. (프로그래밍 언어보다 먼저 배우면 좋다고 생각한다. 특히, 만들면서 배우길 원한다면 특히 더)

스터디에서 Git 관련 이야기를 나눴다. 'Merge vs. Rebase'에 대해 의견을 정리하다 기존에 알고 있던 내용이 수정되어 글을 작성한다.

> Git 다운로드는 생략한다.

## 사전 지식: 주로 사용하는 용어

- Working directory: 작업이 일어나는 공간이다. 추적하지 않는 프로젝트의 현재 상태를 유지하는 공간이다.
- Staging area: 커밋하기 전에 준비하는 공간이다.
- Local repository: 개인 기록을 관리하는 공간이다. 모든 커밋과 브랜치가 포함된다.
- Remote repository: 인터넷이나 네트워크에 올라가는 공간이다. 주로 GitHub를 의미한다.
- Branches: 나무에 가지와 같다. 프로젝트에 영향을 주지 않고 독립적인 공간을 만들어 작업한다.
- Pull request(PR): 변경 사항을 검토, 논의하고 병합하는 요청이다. '예의있는 병합'이라고 말하기도 한다.
- Merge: 분기된 변경 사항을 다른 분기에 합친다. 두 가지 가지를 합쳐서 하나의 가지를 만든다.

## 자주 사용하는 명령어

1. config
2. init
3. status
4. add
5. commit
6. clone
7. checkout
8. branch
9. switch
10. push
11. pull
12. show

## 마치며

소프트웨어는 변화한다. 프레임워크와 언어의 메이저 버전 업데이트는 지속적으로 신경썼다. 하지만 Git은 신경 쓰지 않았다.
언어와 프레임워크보다 더 많이 사용하는 기술인데 한번도 고민하지 않았다. 지금이라도 관심 가지고 정리할 수 있어 다행이다.

**<참고 자료>**

- [GitHub Blog 'Top 12 Git commands every developer must know'](https://github.blog/developer-skills/github/top-12-git-commands-every-developer-must-know/)
- [GitHub Blog 'Highlights from Git 2.23'](https://github.blog/open-source/git/highlights-from-git-2-23/)
- [『팀 개발을 위한 팀 개발을 위한 Git, GitHub 시작하기』(정호영, 진유림, 한빛미디어, 2020)](https://product.kyobobook.co.kr/detail/S000202039327)
- [GitHub '커밋 메시지 가이드'](https://github.com/RomuloOliveira/commit-messages-guide/blob/master/README_ko-KR.md)
