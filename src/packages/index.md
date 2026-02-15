# 패키지 (Packages)
[Typst Universe](https://typst.app/universe)가 런칭된 이후, 이 장은 거의 불필요해졌습니다. Universe는 패키지를 찾기에 매우 훌륭한 곳입니다.

그럼에도 불구하고, 여전히 흥미로운 패키지 사용 예시들이 여기에 남아 있습니다.

## 일반 사항
Typst에는 패키지가 있지만, LaTeX와 달리 다음 사항을 기억해야 합니다:

- 패키지는 일부 전문적인 작업에만 필요하며, 기본적인 포맷팅은 _패키지 없이도 충분히 가능합니다_.
- 패키지는 LaTeX 패키지보다 훨씬 가볍고 "설치"하기 쉽습니다.
- 패키지는 평범한 Typst 파일(때로는 플러그인)일 뿐이므로, 직접 작성하기도 쉽습니다!

강력한 패키지를 사용하려면 다음과 같이 작성하면 됩니다:

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

  // 가느다란 축 스타일 설정
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

## 기여하기
패키지 제작자이거나 공정한 리뷰를 작성하고 싶다면 언제든지 Issue나 PR을 남겨주세요!
