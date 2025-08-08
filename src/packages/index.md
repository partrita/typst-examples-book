# 패키지
[Typst Universe](https://typst.app/universe)가 출시된 후, 이 챕터는 거의 불필요해졌습니다. Universe는 실제로 패키지를 찾기에 매우 멋진 곳입니다.

하지만 여전히 흥미로운 패키지 사용법에 대한 멋진 예제가 있습니다.

## 일반
Typst에는 패키지가 있지만, LaTeX와 달리 다음을 기억해야 합니다:

- 일부 특수 작업에만 필요하며, 기본 서식은 _전혀 없이도 가능합니다_.
- 패키지는 LaTeX 패키지보다 훨씬 가볍고 "설치"가 훨씬 쉽습니다.
- 패키지는 일반 Typst 파일(그리고 때로는 플러그인)이므로, 자신만의 패키지를 쉽게 작성할 수 있습니다!

강력한 패키지를 사용하려면, 다음과 같이 작성하세요:

```typ
#import "@preview/cetz:0.3.4": canvas, draw
#import "@preview/cetz-plot:0.1.1": plot

#set page(width: auto, height: auto, margin: .5cm)

#let style = (stroke: black, fill: rgb(0, 0, 200, 75))

#let f1(x) = calc.sin(x)
#let fn = (
  ($ x - x^3"/"3! $, x => x - calc.pow(x, 3)/6),
  ($ x - x^3"/"3! - x^5"/"5! $, x => x - calc.pow(x, 3)/6 + calc.pow(x, 5)/120),
  ($ x - x^3"/"3! - x^5"/"5! - x^7"/"7! $, x => x - calc.pow(x, 3)/6 + calc.pow(x, 5)/120 - calc.pow(x, 7)/5040),
)

#set text(size: 10pt)

#canvas({
  import draw: *

  // 얇은 축 스타일 설정
  set-style(axes: (stroke: .5pt, tick: (stroke: .5pt)),
            legend: (stroke: none, orientation: ttb, item: (spacing: .3), scale: 80%))

  plot.plot(size: (12, 8),
    x-tick-step: calc.pi/2,
    x-format: plot.formats.multiple-of,
    y-tick-step: 2, y-min: -2.5, y-max: 2.5,
    legend: "inner-north",
    {
      let domain = (-1.1 * calc.pi, +1.1 * calc.pi)

      for ((title, f)) in fn {
        plot.add-fill-between(f, f1, domain: domain,
          style: (stroke: none), label: title)
      }
      plot.add(f1, domain: domain, label: $ sin x  $,
        style: (stroke: black))
    })
})
```

## 기여
패키지 작성자이거나 공정한 개요를 작성하고 싶다면,
자유롭게 이슈/PR을 만드세요!
