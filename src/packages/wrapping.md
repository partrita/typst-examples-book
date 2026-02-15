# 그림 감싸기 (Wrapping figures)

그림 감싸기에 대한 더 나은 네이티브 지원이 계획되어 있지만, 현재 패키지를 통해 일부 기능이 가능합니다:

```typ
#import "@preview/wrap-it:0.1.1": wrap-content, wrap-top-bottom

#set par(justify: true)
#let fig = figure(
  rect(fill: teal, radius: 0.5em, width: 8em),
  caption: [그림 예시],
)
#let body = lorem(40)
#wrap-content(fig, body)

#wrap-content(
  fig,
  body,
  align: bottom + right,
  column-gutter: 2em
)

#let boxed = box(fig, inset: 0.5em)
#wrap-content(boxed)[
  #lorem(40)
]

#let fig2 = figure(
  rect(fill: lime, radius: 0.5em),
  caption: [또 다른 그림],
)
#wrap-top-bottom(boxed, fig2, lorem(60))
```

<div class="warning">제한 사항: 감싸는 부분 근처의 간격이 이상적이지 않을 수 있으며, 상단-하단 왼쪽/오른쪽 배치만 지원됩니다.</div>
