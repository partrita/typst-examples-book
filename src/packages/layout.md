# 레이아웃 (Layouting)

일반적으로 유용한 것들입니다.

## Pinit: 핀(pins)을 이용한 상대적 배치

[pinit](https://github.com/OrangeX4/typst-pinit)의 개념은 일반적인 텍스트 흐름 위에 핀을 꽂고, 그 핀을 기준으로 콘텐츠를 배치하는 것입니다.

```typ
#import "@preview/pinit:0.2.2": *
#set page(height: 6em, width: 20em)

#set text(size: 24pt)

간단한 #pin(1)강조된 텍스트#pin(2)입니다.

#pinit-highlight(1, 2)

#pinit-point-from(2)[단순합니다.]
```

더 복잡한 예시:

```typ
#import "@preview/pinit:0.2.2": *

// 페이지 설정
#set page(paper: "presentation-4-3")
#set text(size: 20pt)
#show heading: set text(weight: "regular")
#show heading: set block(above: 1.4em, below: 1em)
#show heading.where(level: 1): set text(size: 1.5em)

// 유용한 함수들
#let crimson = rgb("#c00000")
#let greybox(..args, body) = rect(fill: luma(95%), stroke: 0.5pt, inset: 0pt, outset: 10pt, ..args, body)
#let redbold(body) = {
  set text(fill: crimson, weight: "bold")
  body
}
#let blueit(body) = {
  set text(fill: blue)
  body
}

// 본문
#block[
  = 점근 표기법: $O$

  #pin("h1")점근 표기법#pin("h2")을 사용하여 알고리즘의 점근적 효율성을 설명합니다.
  (상수 계수와 낮은 차수의 항은 무시합니다.)

  #greybox[
    함수 $g(n)$이 주어졌을 때, $O(g(n))$으로 다음 *함수들의 집합*을 나타냅니다:
    #redbold(${f(n): "존재함" c > 0 "및" n_0 > 0, "다음 조건을 만족함" f(n) <= c dot g(n) "모든" n >= n_0 "에 대하여"}$)
  ]

  #pinit-highlight("h1", "h2")

  $f(n) = O(g(n))$: #pin(1)$f(n)$은 $g(n)$보다 *점근적으로 작습니다*.#pin(2)

  $f(n) redbold(in) O(g(n))$: $f(n)$은 *점근적으로* #redbold[최대] $g(n)$입니다.

  #pinit-line(stroke: 3pt + crimson, start-dy: -0.25em, end-dy: -0.25em, 1, 2)

  #block[삽입 정렬을 #pin("r1")예시#pin("r2")로 들면:]

  - 최선의 경우: $T(n) approx c n + c' n - c''$ #pin(3)
  - 최악의 경우: $T(n) approx c n + (c' \/ 2) n^2 - c''$ #pin(4)

  #pinit-rect("r1", "r2")

  #pinit-place(3, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]
  #pinit-place(4, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]

  #blueit[Q: $n^(3) = O(n^2)$#pin("que") 인가요? 답변을 어떻게 증명할까요#pin("ans")?]

  #pinit-point-to("que", fill: crimson, redbold[아니요.])
  #pinit-point-from("ans", body-dx: -150pt)[
    방정식 $(3/2)^n >= c$ 가 \
    $n$에 대해 무수히 많은 해를 가짐을 보이세요.
  ]
]
```

## 여백 메모 (Margin notes)

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

= 여백 메모
== 설정
안타깝게도 `typst`는 호출 함수에 여백 정보를 노출하지 않으므로, 명시적으로 설정해야 합니다. 이는 *콘텐츠를 배치하기 전*에 `set-page-properties`를 사용하여 수행됩니다:

// 소스 파일 상단에서
// 물론 원하는 여백 숫자로 대체할 수 있습니다. 
// 단, 페이지 여백이 `set-page-properties`에 전달하는 값과 일치해야 합니다.

== 기본 사용법
#lorem(20)
#margin-note(side: left)[안녕, 세상아!]
#lorem(10)
#margin-note[반대편에서 인사드립니다]

#lorem(25)
#margin-note[메모가 겹치려고 하면 자동으로 이동됩니다]
#margin-note(stroke: aqua + 3pt)[충돌을 피하기 위해]
#lorem(25)

#let caution-rect = rect.with(inset: 1em, radius: 0.5em, fill: orange.lighten(80%))
#inline-note(rect: caution-rect)[
  4개 이상의 메모가 겹치면 충돌 방지가 중단될 수 있습니다. 
  이는 `typst`가 5번의 시도(초기 레이아웃 + 각 메모에 대한 조정) 후에도 
  레이아웃이 해결되지 않으면 경고를 보내기 때문입니다.
]
```````

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

== 기본 스타일 조정
모듈 상태를 업데이트하여 모든 함수의 기본값을 사용자 정의할 수 있습니다:

#lorem(4) #margin-note(dy: -2em)[기본 스타일]
#set-margin-note-defaults(stroke: orange, side: left)
#lorem(4) #margin-note[업데이트된 스타일]


기본 `rect`를 재정의하여 더 깊은 수준의 사용자 정의도 가능합니다:

#import "@preview/colorful-boxes:1.1.0": stickybox

#let default-rect(stroke: none, fill: none, width: 0pt, content) = {
  stickybox(rotation: 30deg, width: width/1.5, content)
}
#set-margin-note-defaults(rect: default-rect, stroke: none, side: right)

#lorem(20)
#margin-note(dy: -25pt)[여백에 스티키 메모를 사용해 보는 건 어떨까요?]

// 이전 예제의 변경 사항 취소
#set-margin-note-defaults(rect: rect, stroke: red)

== 여러 명의 문서 리뷰어
#let reviewer-a = margin-note.with(stroke: blue)
#let reviewer-b = margin-note.with(stroke: purple)
#lorem(20)
#reviewer-a[리뷰어 A의 의견]
#lorem(15)
#reviewer-b(side: left)[리뷰어 B의 의견]

== 인라인 메모 (Inline Notes)
#lorem(10)
#inline-note[기본 인라인 메모는 해당 위치에서 단락을 분리합니다]
#lorem(10)
/*
// 작동해야 하지만 안 됨? 저장소에 이슈 생성함.
#inline-note(par-break: false, stroke: (paint: orange, dash: "dashed"))[
  하지만 `par-break: false`를 지정하여 이를 방지할 수 있습니다
]
*/
#lorem(10)
```````

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

== 인쇄 미리보기를 위해 메모 숨기기
#set-margin-note-defaults(hidden: true)

#lorem(20)
#margin-note[이것은 전역 "숨김" 상태를 따릅니다]
#margin-note(hidden: false, dy: -2.5em)[이 메모는 절대로 숨겨지지 않습니다]

= 위치 지정 (Positioning)
== 정밀 배치: 가이드 그리드 (rule grid)
정밀한 위치 지정을 위해 공간 측정이 필요하신가요? `rule-grid`를 사용하여 
페이지에 가이드 라인을 그릴 수 있습니다:

#rule-grid(width: 10cm, height: 3cm, spacing: 20pt)
#place(
  dx: 180pt,
  dy: 40pt,
  rect(fill: white, stroke: red, width: 1in, "(180pt, 40pt)에서 시작합니다")
)

// 선택적으로 가장 작은 차원의 분할 수를 지정하여 간격을 자동으로 계산합니다
#rule-grid(dx: 10cm + 3em, width: 3cm, height: 1.2cm, divisions: 5, square: true,  stroke: green)

// 가이드 그리드는 공간을 차지하지 않으므로 명시적으로 추가합니다
#v(3cm + 1em)

== 절대 위치 지정
여백이나 상대적 위치에 상관없이 무언가를 절대적으로 배치하고 싶으신가요? 
`absolute-place`가 도와드립니다. 콘텐츠를 어디에나 둘 수 있습니다:

#context {
  let (dx, dy) = (25%, here().position().y)
  let content-str = (
    "이 절대 배치된 박스는 페이지 좌표 (" + repr(dx) + ", " + repr(dy) + ")"
    + "에서 시작합니다"
  )
  absolute-place(
    dx: dx, dy: dy,
    rect(
      fill: green.lighten(60%),
      radius: 0.5em,
      width: 2.5in,
      height: 0.5in,
      [#align(center + horizon, content-str)]
    )
  )
}
#v(1in)

`rule-grid`는 `relative: false`를 전달하여 페이지 왼쪽 상단에서의 절대 배치를 지원합니다. 
페이지 전체에 "가이드 라인"을 그리는 데 유용합니다.
```````

## 첫 글자 장식 (Dropped capitals)

> 자세한 정보는 [여기](https://github.com/EpicEricEE/typst-plugins/tree/master/droplet)에서 확인하세요.

### 기본 사용법

```typ
#import "@preview/droplet:0.3.1": dropcap

#dropcap(gap: -2pt, hanging-indent: 8pt)[
  #lorem(42)
]
```

### 확장 스타일링

```typ
#import "@preview/droplet:0.3.1": dropcap

#dropcap(
  height: 2,
  justify: true,
  gap: 6pt,
  transform: letter => context {
    let height = measure(letter).height

    grid(columns: 2, gutter: 6pt,
      align(center + horizon, text(blue, letter)),
      // "place"를 사용하여 나중에 글꼴 크기가 계산될 때 
      // 선의 높이를 무시하도록 합니다.
      place(horizon, line(
        angle: 90deg,
        length: height + 6pt,
        stroke: blue.lighten(40%) + 1pt
      )),
    )
  }
)[
  #lorem(42)
]
```

## 실제 현재 장의 제목 표시

> [hydra](https://github.com/tingerrr/hydra)를 참조하세요.

```typ-nopreamble
#import "@preview/hydra:0.6.1": hydra

#set page(header: context hydra() + line(length: 100%))
#set heading(numbering: "1.1")
#show heading.where(level: 1): it => pagebreak(weak: true) + it

= 서론
#lorem(750)

= 본문
== 첫 번째 섹션
#lorem(500)
== 두 번째 섹션
#lorem(250)
== 세 번째 섹션
#lorem(500)

= 부록 (Annex)
#lorem(10)
```
