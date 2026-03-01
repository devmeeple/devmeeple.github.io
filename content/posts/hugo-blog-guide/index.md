---
title: '#2. 고급 설정'
date: '2026-03-01T14:26:21+09:00'
categories: ["기타"]
tags: ["Hugo", "Blog"]
series: ["Hugo 블로그 운영 가이드"]
series_order: 2
draft: true
---

## 1. 명령어로 게시글 작성하기

```shell
# hugo new content posts/[제목(URL)]/index.md
hugo new content posts/hugo-blog-guide/index.md
```

- 명령어가 익숙하지 않으면 직접 만드는 방법이 간편하다고 생각할지도 모른다. 하지만 Hugo는 명령어를 사용했을 때 빛을 발한다. 익숙해지는 것을 강력 추천한다.
- IDE에서 따로 Live templates[^1], Snippets[^2]을 활용하지 않아도 기본 구조를 자동으로 넣어준다.

### 1.1 기본 템플릿 수정하기

> [!INFO] archetypes/default.md 수정

```text
+++
date = '{{ .Date }}'
draft = true
title = '{{ replace .File.ContentBaseName `-` ` ` | title }}'
+++
```

- 게시글을 쉽게 작성할 수 있도록 명령어를 사용했다. 하지만 기본 템플릿을 수정하지 않으면 front matter를 역시 추가 수정해야 한다. 마음에 들지 않는다.

```yaml
---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: '{{ .Date }}'
categories: []
tags: []
draft: true
---
```

- `Archetypes`를 사용하면 명령어로 만들어지는 기본 템플릿도 수정할 수 있다. 자신의 환경에 맞게 수정한다.
  - `yaml`, `toml`, `json` 형식을 지원한다. 가장 대중적으로 사용하는 `yaml` 형식을 추천한다.

## 2. 업데이트 날짜 표시하기

### 2.1 Front matter 수정하기

> [!INFO] config/_default/params.toml 수정

![업데이트 날짜 표시하기(front matter 수정)](img/show-date-updated.png "업데이트 날짜 표시하기")

- `showDateUpdated` 옵션의 값을 `true`로 수정한다.

### 2.2 수정 날짜 자동으로 추가하기(feat. Git)

> [!INFO] config/_default/hugo.toml 수정

- `enableGitInfo = true`를 추가한다.
  - 옵션을 추가하지 않으면 front matter를 직접 수정해야 하는 번거로움이 발생한다.

## 3. 폰트 변경하기 (feat. Pretendard)

> [!INFO] assets/css/custom.css를 수정하고 static/fonts에 폰트를 위치한다.

```text
.
├── assets
│   └── css
│       └── custom.css
...
└─── static
    └── fonts
        └─── font.ttf
```

- [Pretendard](https://github.com/orioncactus/pretendard)를 다운로드 받아 `custom.css` 파일을 수정, 기존 설정을 덮어쓴다.

```text
@font-face {
    font-family: "Pretendard-Regular";
    src: url('/fonts/Pretendard-Regular.woff2') format('woff2');
}

html {
    font-family: Pretendard-Regular, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
}
```

- 폰트는 `static/fonts/Pretendard.woff2`에 위치한다.

> [!NOTE]
> TTF, OTF 파일은 로컬에 설치하는 파일이다. 반면 웹에서 사용하는 폰트는 WOFF(Web Open Font Format) 또는 WOFF2를 사용한다.
> WOFF는 기존 폰트 파일(TTF, OTF)을 압축한 형태다. GZIP 알고리즘을 사용한다. 대부분의 브라우저에서 지원한다.
> WOFF2(Web Open Font Format2): WOFF는 WOFF를 개선했다. Brotli 알고리즘을 사용하여 WOFF에 비해 평균 30% 더 작은 파일 크기를 유지한다.
> 하지만 WOFF2는 최신 브라우저에서는 거의 모두 지원하지만 일부 브라우저에서는 지원하지 않을 수 있다.

## 마치며

### 참고 자료

- [Archetypes](https://gohugo.io/content-management/archetypes/)
- [Lastmod](https://gohugo.io/methods/page/lastmod/)
- [Gitinfo](https://gohugo.io/methods/page/gitinfo/)
- [Advanced Customisation](https://blowfish.page/docs/advanced-customisation/)

[^1]: https://www.jetbrains.com/help/idea/using-live-templates.html
[^2]: https://code.visualstudio.com/docs/editing/userdefinedsnippets
