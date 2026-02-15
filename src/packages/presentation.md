# 프레젠테이션 (Presentations)
## Polylux

> [polylux 북](https://polylux.dev/book/)을 참조하세요.

```typ
// 공식 패키지 저장소에서 Polylux 가져오기
#import "@preview/polylux:0.3.1": *

// 종이 크기를 프레젠테이션에 맞게 설정하고 텍스트를 크게 만듭니다.
#set page(paper: "presentation-16-9")
#set text(size: 25pt)

// #polylux-slide를 사용하여 슬라이드를 만들고 선호하는 Typst 함수로 스타일을 지정하세요.
#polylux-slide[
  #align(horizon + center)[
    = 매우 미니멀한 슬라이드

    게으른 저자

    2023년 7월 23일
  ]
]

#polylux-slide[
  == 첫 번째 슬라이드

  이 슬라이드의 정적 텍스트입니다.
]

#polylux-slide[
  == 이 슬라이드는 변합니다!

  이 내용은 항상 보입니다.
  // #uncover, #only 등과 같은 기능을 사용하여 동적 콘텐츠를 만듭니다.
  #uncover(2)[하지만 이 내용은 나중에 나타납니다!]
]
```

## Slydst
> [여기](https://github.com/glambrechts/slydst?ysclid=lr2gszrkck541184604)에서 문서를 확인하세요.

Polylux보다 훨씬 간단하고 기능이 적습니다:

```typ
#import "@preview/slydst:0.1.0": *

#show: slides.with(
  title: "여기에 제목을 입력하세요", // 필수 항목
  subtitle: none,
  date: none,
  authors: (),
  layout: "medium",
  title-color: none,
)

== 개요 (Outline)

#outline()

= 첫 번째 섹션

== 첫 번째 슬라이드

#figure(rect(width: 60%), caption: "캡션")

#v(1fr)

#lorem(20)

#definition(title: "흥미로운 정의")[
  #lorem(20)
]
```
