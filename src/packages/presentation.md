# 프레젠테이션
## Polylux

> [polylux 책](https://polylux.dev/book/) 참조

```typ
// 공식 패키지 저장소에서 Polylux 가져오기
#import "@preview/polylux:0.3.1": *

// 용지 크기를 프레젠테이션에 맞게 조정하고 텍스트를 더 크게 만들기
#set page(paper: "presentation-16-9")
#set text(size: 25pt)

// #polylux-slide를 사용하여 슬라이드를 만들고 좋아하는 Typst 함수를 사용하여 스타일 지정
#polylux-slide[
  #align(horizon + center)[
    = 매우 미니멀한 슬라이드

    게으른 저자

    2023년 7월 23일
  ]
]

#polylux-slide[
  == 첫 번째 슬라이드

  이 슬라이드의 일부 정적 텍스트.
]

#polylux-slide[
  == 이 슬라이드는 변경됩니다!

  이것은 항상 볼 수 있습니다.
  // #uncover, #only 등과 같은 기능을 사용하여 동적 콘텐츠 만들기
  #uncover(2)[하지만 이것은 나중에 나타납니다!]
]
```

## Slydst
> [여기](https://github.com/glambrechts/slydst?ysclid=lr2gszrkck541184604)에서 설명서 참조.

polulyx보다 훨씬 간단하고 덜 강력합니다:

```typ
#import "@preview/slydst:0.1.0": *

#show: slides.with(
  title: "여기에 제목 삽입", // 필수
  subtitle: none,
  date: none,
  authors: (),
  layout: "medium",
  title-color: none,
)

== 개요

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
