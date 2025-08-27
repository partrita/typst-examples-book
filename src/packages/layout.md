# 레이아웃

일반적으로 유용한 것들.

## Pinit: 핀으로 상대적 위치 지정

[pinit](https://github.com/OrangeX4/typst-pinit)의 아이디어는 텍스트의 일반적인 흐름에 핀을 고정하고, 핀을 기준으로 콘텐츠를 배치하는 것입니다.

```typ
#import "@preview/pinit:0.2.2": *
#set page(height: 6em, width: 20em)

#set text(size: 24pt)

간단한 #pin(1)강조된 텍스트#pin(2).

#pinit-highlight(1, 2)

#pinit-point-from(2)[간단합니다.]
```

더 복잡한 예:

```typ
#import "@preview/pinit:0.2.2": *

// 페이지
#set page(paper: "presentation-4-3")
#set text(size: 20pt)
#show heading: set text(weight: "regular")
#show heading: set block(above: 1.4em, below: 1em)
#show heading.where(level: 1): set text(size: 1.5em)

// 유용한 함수
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

  알고리즘의 점근적 효율성을 설명하기 위해 #pin("h1")점근 표기법#pin("h2")을 사용합니다.
  (상수 계수 및 저차 항 무시)

  #greybox[
    함수 $g(n)$이 주어졌을 때, $O(g(n))$은 다음 *함수 집합*을 나타냅니다:
    #redbold(${f(n): "존재" c > 0 "그리고" n_0 > 0, "그런" f(n) <= c dot g(n) "모든" n >= n_0}$)
  ]

  #pinit-highlight("h1", "h2")

  $f(n) = O(g(n))$: #pin(1)$f(n)$은 $g(n)$보다 *점근적으로 작습니다*.#pin(2)

  $f(n) redbold(in) O(g(n))$: $f(n)$은 *점근적으로* #redbold[최대] $g(n)$입니다.

  #pinit-line(stroke: 3pt + crimson, start-dy: -0.25em, end-dy: -0.25em, 1, 2)

  #block[삽입 정렬 #pin("r1")예시#pin("r2"):]

  - 최상의 경우: $T(n) approx c n + c' n - c''$ #pin(3)
  - 최악의 경우: $T(n) approx c n + (c' \/ 2) n^2 - c''$ #pin(4)

  #pinit-rect("r1", "r2")

  #pinit-place(3, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]
  #pinit-place(4, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]

  #blueit[Q: $n^(3) = O(n^2)$#pin("que")입니까? 답을 증명하는 방법#pin("ans")?]

  #pinit-point-to("que", fill: crimson, redbold[아니요.])
  #pinit-point-from("ans", body-dx: -150pt)[
    방정식 $(3/2)^n >= c$가 \
    $n$에 대해 무한히 많은 해를 가짐을 보이세요.
  ]
]
```

## 여백 노트

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

= 여백 노트
== 설정
불행히도 `typst`는 호출 함수에 여백을 노출하지 않으므로, 명시적으로 설정해야 합니다. 이것은 콘텐츠를 배치하기 *전에* `set-page-properties`를 사용하여 수행됩니다:

// 소스 파일 상단에
// 물론, 페이지 여백이 `set-page-properties`에 전달하는 것과 일치하는 한
// 원하는 여백 번호를 대체할 수 있습니다

== 기본
#lorem(20)
#margin-note(side: left)[안녕하세요, 세상!]
#lorem(10)
#margin-note[다른 쪽에서 안녕하세요]

#lorem(25)
#margin-note[노트가 겹치려고 하면 자동으로 이동됩니다]
#margin-note(stroke: aqua + 3pt)[충돌을 피하기 위해]
#lorem(25)

#let caution-rect = rect.with(inset: 1em, radius: 0.5em, fill: orange.lighten(80%))
#inline-note(rect: caution-rect)[
  4개 이상의 노트가 겹치면 노트가 자동으로 충돌을 피하는 것을 멈춘다는 점에 유의하세요.
  이것은 `typst`가 5번의 시도(초기 레이아웃 + 각 노트에 대한 조정) 후에 레이아웃이 해결되지 않으면 경고하기 때문입니다
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
모든 함수 기본값은 모듈 상태를 업데이트하여 사용자 정의할 수 있습니다:

#lorem(4) #margin-note(dy: -2em)[기본 스타일]
#set-margin-note-defaults(stroke: orange, side: left)
#lorem(4) #margin-note[업데이트된 스타일]


기본 `rect`를 재정의하여 더 깊은 사용자 정의가 가능합니다:

#import "@preview/colorful-boxes:1.1.0": stickybox

#let default-rect(stroke: none, fill: none, width: 0pt, content) = {
  stickybox(rotation: 30deg, width: width/1.5, content)
}
#set-margin-note-defaults(rect: default-rect, stroke: none, side: right)

#lorem(20)
#margin-note(dy: -25pt)[여백에 스티커 노트를 사용하지 않을 이유가 없죠?]

// 마지막 예제의 변경 사항 취소
#set-margin-note-defaults(rect: rect, stroke: red)

== 여러 문서 검토자
#let reviewer-a = margin-note.with(stroke: blue)
#let reviewer-b = margin-note.with(stroke: purple)
#lorem(20)
#reviewer-a[검토자 A의 댓글]
#lorem(15)
#reviewer-b(side: left)[검토자 B의 댓글]

== 인라인 노트
#lorem(10)
#inline-note[기본 인라인 노트는 해당 위치에서 단락을 나눕니다]
#lorem(10)
/*
// 작동해야 하지만, 그렇지 않습니까? 저장소에 이슈를 만들었습니다.
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

== 인쇄 미리보기를 위해 노트 숨기기
#set-margin-note-defaults(hidden: true)

#lorem(20)
#margin-note[이것은 전역 "hidden" 상태를 존중합니다]
#margin-note(hidden: false, dy: -2.5em)[이 노트는 절대 숨겨지지 않습니다]

= 위치 지정
== 정밀한 배치: 규칙 그리드
미세 조정된 위치 지정을 위해 공간을 측정해야 합니까? `rule-grid`를 사용하여 페이지에 규칙 선을 그을 수 있습니다:

#rule-grid(width: 10cm, height: 3cm, spacing: 20pt)
#place(
  dx: 180pt,
  dy: 40pt,
  rect(fill: white, stroke: red, width: 1in, "이것은 (180pt, 40pt)에서 시작됩니다")
)

// 선택적으로 가장 작은 차원의 분할을 지정하여 간격을 자동으로 계산합니다
#rule-grid(dx: 10cm + 3em, width: 3cm, height: 1.2cm, divisions: 5, square: true,  stroke: green)

// 규칙 그리드는 공간을 차지하지 않으므로 명시적으로 추가하세요
#v(3cm + 1em)

== 절대 위치 지정
여백 및 상대 위치에 관계없이 무언가를 절대적으로 배치하는 것은 어떻습니까? `absolute-place`가 친구입니다. 콘텐츠를 어디에나 배치할 수 있습니다:

#context {
  let (dx, dy) = (25%, here().position().y)
  let content-str = (
    "이 절대적으로 배치된 상자는 페이지 좌표에서 (" + repr(dx) + ", " + repr(dy) + ")에서 시작됩니다"
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

"rule-grid"는 `relative: false`를 전달하여 페이지의 왼쪽 상단에 절대 배치를 지원합니다. 이것은 전체 페이지를 "규칙"하는 데 도움이 됩니다.
```````

## 드롭 캡

> [여기](https://github.com/EpicEricEE/typst-plugins/tree/master/droplet)에서 자세한 정보 얻기

### 기본 사용법

```typ
#import "@preview/droplet:0.3.1": dropcap

#dropcap(gap: -2pt, hanging-indent: 8pt)[
  #lorem(42)
]
```

### 확장된 스타일링

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
      // 글꼴 크기가 나중에 계산될 때 줄의 높이를 무시하려면 "place"를 사용하세요.
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

## 실제 현재 챕터의 제목

> [hydra](https://github.com/tingerrr/hydra) 참조

```typ-nopreamble
#import "@preview/hydra:0.6.1": hydra

#set page(header: context hydra() + line(length: 100%))
#set heading(numbering: "1.1")
#show heading.where(level: 1): it => pagebreak(weak: true) + it

= 서론
#lorem(750)

= 내용
== 첫 번째 섹션
#lorem(500)
== 두 번째 섹션
#lorem(250)
== 세 번째 섹션
#lorem(500)

= 부록
#lorem(10)
```
