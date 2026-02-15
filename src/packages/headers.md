# 헤더 (Headers)

## `hydra`: 문맥 의존적 헤더

`Typst 기초` 섹션에서 `query(selector(heading).before(here()))`를 사용하여 현재 제목을 가져와 헤더를 만드는 방법을 논의했습니다. 하지만 이 방식은 번호가 매겨진 중첩된 제목 등에서 제대로 작동하지 않는 경우가 있습니다. 이런 상황을 위해 `hydra` 패키지가 있습니다:

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

= 본문
== 첫 번째 섹션
#lorem(50)
== 두 번째 섹션
#lorem(100)
```
