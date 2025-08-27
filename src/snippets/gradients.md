# 색상 및 그라데이션

## 그라데이션

그라데이션은 프레젠테이션이나 예쁜 모양을 위해 매우 멋질 수 있습니다.

```typ
/// 저자: frozolotl
#set page(paper: "presentation-16-9", margin: 0pt)
#set text(fill: white, font: "Inter")

#let grad = gradient.linear(rgb("#953afa"), rgb("#c61a22"), angle: 135deg)

#place(horizon + left, image(width: 60%, "../img/landscape.png"))

#place(top, polygon(
  (0%, 0%),
  (70%, 0%),
  (70%, 25%),
  (0%, 29%),
  fill: white,
))
#place(bottom, polygon(
  (0%, 100%),
  (100%, 100%),
  (100%, 30%),
  (60%, 30% + 60% * 4%),
  (60%, 60%),
  (0%, 64%),
  fill: grad,
))

#place(top + right, block(inset: 7pt, image(height: 19%, "../img/tub.png")))

#place(bottom, block(inset: 40pt)[
  #text(size: 30pt)[
    프레젠테이션 제목
  ]

  #text(size: 16pt)[#lorem(20) | #datetime.today().display()]
])
```
