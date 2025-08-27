# 헤더

## `hydra`: 컨텍스트 헤더

`Typst Basics`에서 헤더에 대해 `query(selector(heading).before(here()))`를 사용하여 현재 제목을 가져오는 방법을 논의했습니다. 그러나 이것은 번호 매기기 및 유사한 것들이 있는 중첩된 제목에 대해서는 잘 작동하지 않습니다. 이러한 경우를 위해 `hydra`가 있습니다:

```typ
#import "@preview/hydra:0.6.1": hydra

#set page(height: 10 * 20pt, margin: (y: 4em), numbering: "1", header: context {
  if calc.odd(here().page()) {
    align(right, emph(hydra(1)))
  } else {
    align(left, emph(hydra(2)))
  }
  line(length: 100%)
})
#set heading(numbering: "1.1")
#show heading.where(level: 1): it => pagebreak(weak: true) + it

= 서론
#lorem(50)

= 내용
== 첫 번째 섹션
#lorem(50)
== 두 번째 섹션
#lorem(100)
```