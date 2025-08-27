# 용어집

## glossarium

>[우주 링크](https://typst.app/universe/package/glossarium)

용어집 및 약어를 관리하는 패키지입니다.

<div class="info">Typst 최초의 멋진 패키지 중 하나로, 아마도 Typst로 작성된 최초의 논문을 위해 특별히 제작되었습니다.<div>

```typ
#import "@preview/glossarium:0.5.4": make-glossary, register-glossary, print-glossary, gls, glspl
#show: make-glossary

// 더 나은 링크 가시성을 위해
#show link: set text(fill: blue.darken(60%))

#let entry-list = (
    (
    // 최소 용어
    (key: "kuleuven", short: "KU Leuven"),

    // 긴 형식과 그룹이 있는 용어
    (key: "unamur", short: "UNamur", long: "Namur University", group: "Universities"),

    // 마크업 설명이 있는 용어
    (
      key: "oidc",
      short: "OIDC",
      long: "OpenID Connect",
      description: [OpenID는 비영리 단체인
      #link("https://en.wikipedia.org/wiki/OpenID#OpenID_Foundation")[OpenID Foundation]이 추진하는 개방형 표준 및 분산 인증 프로토콜입니다.],
      group: "Accronyms",
    ),

    // 짧은 복수형이 있는 용어
    (
      key: "potato",
      short: "potato",
      // "plural"은 "short"를 복수형으로 만들어야 할 때 사용됩니다.
      plural: "potatoes",
      description: [#lorem(10)],
    ),

    // 긴 복수형이 있는 용어
    (
      key: "dm",
      short: "DM",
      long: "diagonal matrix",
      // "longplural"은 "long"을 복수형으로 만들어야 할 때 사용됩니다.
      longplural: "diagonal matrices",
      description: "아마도 수학적인 내용일 겁니다. 잘 모르겠네요",
    ),
  )
)

#register-glossary(entry-list)

// 문서 본문
#print-glossary(
 entry-list
)

// gls를 사용하여 OIDC 용어 참조
#gls("oidc")
// 긴 형식을 강제로 표시
#gls("oidc", long: true)

// 참조 구문을 사용하여 OIDC 용어 참조
@oidc

복수형: #glspl("potato")

#gls("oidc", display: "원하는 대로 표시")
```