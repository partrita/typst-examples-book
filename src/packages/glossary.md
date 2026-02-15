# 용어 사전 (Glossary)

## glossarium

>[Universe 링크](https://typst.app/universe/package/glossarium)

용어 사전과 약어를 관리하는 패키지입니다.

<div class="info">Typst의 아주 초기 패키지 중 하나로, (아마도) Typst로 작성된 첫 번째 학위 논문을 위해 특별히 제작되었습니다.<div>

```typ
#import "@preview/glossarium:0.5.4": make-glossary, register-glossary, print-glossary, gls, glspl
#show: make-glossary

// 링크 시인성을 높이기 위해
#show link: set text(fill: blue.darken(60%))

#let entry-list = (
    (
    // 최소 용어
    (key: "kuleuven", short: "KU Leuven"),

    // 긴 형태와 그룹이 있는 용어
    (key: "unamur", short: "UNamur", long: "남루르 대학교", group: "대학"),

    // 마크업 설명이 있는 용어
    (
      key: "oidc",
      short: "OIDC",
      long: "OpenID Connect",
      description: [OpenID는 비영리 단체인 
      #link("https://en.wikipedia.org/wiki/OpenID#OpenID_Foundation")[OpenID Foundation]에서 추진하는 오픈 표준이자 분산형 인증 프로토콜입니다.],
      group: "약어",
    ),

    // 짧은 복수형이 있는 용어
    (
      key: "potato",
      short: "potato",
      // "plural"은 "short"를 복수형으로 만들 때 사용됩니다.
      plural: "potatoes",
      description: [#lorem(10)],
    ),

    // 긴 복수형이 있는 용어
    (
      key: "dm",
      short: "DM",
      long: "대각 행렬 (diagonal matrix)",
      // "longplural"은 "long"을 복수형으로 만들 때 사용됩니다.
      longplural: "대각 행렬들 (diagonal matrices)",
      description: "아마도 어떤 수학 관련 내용인 것 같습니다.",
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
// 강제로 긴 형태 표시
#gls("oidc", long: true)

// 참조 구문을 사용하여 OIDC 용어 참조
@oidc

복수형: #glspl("potato")

#gls("oidc", display: "원하는 대로 표시")
```
