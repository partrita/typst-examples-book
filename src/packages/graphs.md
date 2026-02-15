# 그래프 (Graphs)

## `cetz`

Cetz는 기본적인 그래프를 그릴 수 있는 기능을 내장하고 있습니다.
`plotst`와 같은 패키지보다 훨씬 더 사용자 정의가 가능하고 확장성이 뛰어나므로, Cetz의 기능을 살펴보는 것을 추천합니다.

> [전체 매뉴얼](https://github.com/johannes-wolf/cetz/blob/master/manual.pdf?raw=true)을 확인하세요.

```typ
#import "@preview/cetz:0.3.4"

#import cetz.plot
#plot.plot(size: (3,2), x-tick-step: 1, y-tick-step: 1, {
 let z(x, y) = {
   (1 - x/2 + calc.pow(x,5) + calc.pow(y,3)) * calc.exp(-(x*x) - (y*y))
 }
 plot.add-contour(x-domain: (-2, 3), y-domain: (-3, 3),
 z, z: (.1, .4, .7), fill: true)
})
```
-->

```typ
#let data = (
  [A], ([B], [C], [D]), ([E], [F])
)

#import "@preview/cetz:0.3.4": canvas, draw, tree

#canvas(length: 1cm, {
  import draw: *

  set-style(content: (padding: .2),
    fill: gray.lighten(70%),
    stroke: gray.lighten(70%))

  tree.tree(data, spread: 2.5, grow: 1.5, draw-node: (node, _) => {
    circle((), radius: .45, stroke: none)
    content((), node.content)
  }, draw-edge: (from, to, _) => {
    line((a: from, number: .6, abs: true, b: to),
         (a: to, number: .6, abs: true, b: from), mark: (end: ">"))
  }, name: "tree")

  // 두 노드 사이에 "사용자 정의" 연결 그리기
  let (a, b) = ("tree.0-0-1", "tree.0-1-0",)
  line((a: a, number: .6, abs: true, b: b), (a: b, number: .6, abs: true, b: a), mark: (end: ">", start: ">"))
})
```

```typ
#import "@preview/cetz:0.3.4": canvas, draw

#canvas({
    import draw: *
    circle((90deg, 3), radius: 0, name: "content")
    circle((210deg, 3), radius: 0, name: "structure")
    circle((-30deg, 3), radius: 0, name: "form")
    for (c, a) in (
    ("내용", "bottom"),
    ("구조", "top-right"),
    ("형식", "top-left")
    ) {
    content(c, box(c + " 지향", inset: 5pt), anchor:
    a)
    }
    stroke(gray + 1.2pt)
    line("내용", "구조", "형식", close: true)
    for (c, s, f, cont) in (
    (0.5, 0.1, 1, "PostScript"),
    (1, 0, 0.4, "DVI"),
    (0.5, 0.5, 1, "PDF"),
    (0, 0.25, 1, "CSS"),
    (0.5, 1, 0, "XML"),
    (0.5, 1, 0.4, "HTML"),
    (1, 0.2, 0.8, "LaTeX"),
    (1, 0.6, 0.8, "TeX"),
    (0.8, 0.8, 1, "Word"),
    (1, 0.05, 0.05, "ASCII")
    ) {
    content((bary: (내용: c, 구조: s, 형식:
    f)),cont)
    }
})
```

```typ
#import "@preview/cetz:0.3.4": canvas, chart

#let data2 = (
  ([15-24], 18.0, 20.1, 23.0, 17.0),
  ([25-29], 16.3, 17.6, 19.4, 15.3),
  ([30-34], 14.0, 15.3, 13.9, 18.7),
  ([35-44], 35.5, 26.5, 29.4, 25.8),
  ([45-54], 25.0, 20.6, 22.4, 22.0),
  ([55+],   19.9, 18.2, 19.2, 16.4),
)

#canvas({
  chart.barchart(mode: "clustered",
                 size: (9, auto),
                 label-key: 0,
                 value-key: (..range(1, 5)),
                 bar-width: .8,
                 x-tick-step: 2.5,
                 data2)
})
```

### 극좌표계에서 그래프 그리기
```typ
#import "@preview/cetz:0.3.4": canvas, plot

#figure(
canvas(length: 1cm, {
  plot.plot(size: (5, 5),
    x-tick-step: 5,
    y-tick-step: 5,
    x-max: 20,
    y-max: 20,
    x-min: -20,
    y-min: -20,
    x-grid: true,
    y-grid: true,
    {
      plot.add(
        domain: (0,2*calc.pi),
        samples: 100,
        t => (13*calc.cos(t)-5*calc.cos(2*t)-2*calc.cos(3*t)-calc.cos(4*t), 16*calc.sin(t)*calc.sin(t)*calc.sin(t))
        )
    })
}), caption: "cetz로 만든 그래프",)
```

## `diagraph`
### 테스트

```````typ
#import "@preview/diagraph:0.2.0": *
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph {
    rankdir=LR;
    f -> B
    B -> f
    C -> D
    D -> B
    E -> F
    f -> E
    B -> F
  }
  ```
)
```````

### 관계도

```````typ
#import "@preview/diagraph:0.2.0": *
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph {
    orange -> fruit
    apple -> fruit
    fruit -> food
    carrot -> vegetable
    vegetable -> food
    food -> eat
    eat -> survive
  }
  ```
)
```````

### FFT

레이블을 수동으로 재정의했습니다.

```````typ
#import "@preview/diagraph:0.2.0": *
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph {
    node [shape=none]
    1
    2
    3
    r1
    r2
    r3
    1->2
    1->3
    2->r1 [color=red]
    3->r2 [color=red]
    r1->r3 [color=red]
    r2->r3 [color=red]
  }
  ```
)
```````

### 상태 머신 (State Machine)

```````typ
#import "@preview/diagraph:0.2.0": *
#set page(width: auto)
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph finite_state_machine {
    rankdir=LR
    size="8,5"

    node [shape=doublecircle]
    LR_0
    LR_3
    LR_4
    LR_8

    node [shape=circle]
    LR_0 -> LR_2 [label="SS(B)"]
    LR_0 -> LR_1 [label="SS(S)"]
    LR_1 -> LR_3 [label="S($end)"]
    LR_2 -> LR_6 [label="SS(b)"]
    LR_2 -> LR_5 [label="SS(a)"]
    LR_2 -> LR_4 [label="S(A)"]
    LR_5 -> LR_7 [label="S(b)"]
    LR_5 -> LR_5 [label="S(a)"]
    LR_6 -> LR_6 [label="S(b)"]
    LR_6 -> LR_5 [label="S(a)"]
    LR_7 -> LR_8 [label="S(b)"]
    LR_7 -> LR_5 [label="S(a)"]
    LR_8 -> LR_6 [label="S(b)"]
    LR_8 -> LR_5 [label="S(a)"]
  }
  ```
)
```````

### 클러스터링 (Clustering)

> [문서](http://www.graphviz.org/content/cluster)를 참조하세요.

```````typ
#import "@preview/diagraph:0.2.0": *
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph G {

    subgraph cluster_0 {
      style=filled;
      color=lightgrey;
      node [style=filled,color=white];
      a0 -> a1 -> a2 -> a3;
      label = "프로세스 #1";
    }

    subgraph cluster_1 {
      node [style=filled];
      b0 -> b1 -> b2 -> b3;
      label = "프로세스 #2";
      color=blue
    }

    start -> a0;
    start -> b0;
    a1 -> b3;
    b2 -> a3;
    a3 -> a0;
    a3 -> end;
    b3 -> end;

    start [shape=Mdiamond];
    end [shape=Msquare];
  }
  ```
)
```````

### HTML

```````typ
#import "@preview/diagraph:0.2.0": *
#let renderc(code) = render(code.text)

#renderc(
  ```
  digraph structs {
      node [shape=plaintext]
      struct1 [label=<
  <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0">
    <TR><TD>left</TD><TD PORT="f1">mid dle</TD><TD PORT="f2">right</TD></TR>
  </TABLE>>];
      struct2 [label=<
  <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0">
    <TR><TD PORT="f0">one</TD><TD>two</TD></TR>
  </TABLE>>];
      struct3 [label=<
  <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" CELLPADDING="4">
    <TR>
      <TD ROWSPAN="3">안녕<BR/>세상아</TD>
      <TD COLSPAN="3">b</TD>
      <TD ROWSPAN="3">g</TD>
      <TD ROWSPAN="3">h</TD>
    </TR>
    <TR>
      <TD>c</TD><TD PORT="here">d</TD><TD>e</TD>
    </TR>
    <TR>
      <TD COLSPAN="3">f</TD>
    </TR>
  </TABLE>>];
      struct1:f1 -> struct2:f0;
      struct1:f2 -> struct3:here;
  }
  ```
)
```````

### 재정의된 레이블

노드 `big`과 `sum`의 레이블이 재정의되었습니다.

```````typ
#import "@preview/diagraph:0.2.0": *
#set page(width: auto)

#raw-render(
  ```
  digraph {
    rankdir=LR
    node[shape=circle]
    음 -> a_0
    음 -> big
    a_0 -> "a'" -> big [style="dashed"]
    big -> sum
  }
  ```,
  labels: (:
    big: [_일부_#text(2em)[ 큰 ]*텍스트*],
    sum: $ sum_(i=0)^n 1/i $,
  ),
)
```````

## `bob-draw`

 ASCII를 사용하여 쉽게 그릴 수 있게 해주는 [svgbob](https://github.com/ivanceras/svgbob)용 WASM 플러그인입니다.

`````typ
#import "@preview/bob-draw:0.1.0": *
#render(```
         /\_/\
bob ->  ( o.o )
         \ " /
  .------/  /
 (        | |
  `====== o o
```)
`````

`````typ
#import "@preview/bob-draw:0.1.0": *
#show raw.where(lang: "bob"): it => render(it)

#render(
    ```
      0       3  
       *-------* 
    1 /|    2 /| 
     *-+-----* | 
     | |4    | |7
     | *-----|-*
     |/      |/
     *-------*
    5       6
    ```,
    width: 25%,
)

```bob
"고양이들:"
 /\_/\  /\_/\  /\_/\  /\_/\ 
( o.o )( o.o )( o.o )( o.o )
```

```bob
       +10-15V           ___0,047R
      *---------o-----o-|___|-o--o---------o----o-------.
    + |         |     |       |  |         |    |       |
    -===-      _|_    |       | .+.        |    |       |
    -===-      .-.    |       | | | 2k2    |    |       |
    -===-    470| +   |       | | |        |    |      _|_
    - |       uF|     '--.    | '+'       .+.   |      \ / LED
      +---------o        |6   |7 |8    1k | |   |      -+-
             ___|___   .-+----+--+--.     | |   |       |
              -═══-    |            |     '+'   |       |
                -      |            |1     |  |/  BC    |
               GND     |            +------o--+   547   |
                       |            |      |  |`>       |
                       |            |     ,+.   |       |
               .-------+            | 220R| |   o----||-+  IRF9Z34
               |       |            |     | |   |    |+->
               |       |  MC34063   |     `+'   |    ||-+
               |       |            |      |    |       |  BYV29     -12V6
               |       |            |      '----'       o--|<-o----o--X OUT
 6000 micro  - | +     |            |2                  |     |    |
 Farad, 40V ___|_____  |            |--o                C|    |    |
 Capacitor  ~ ~ ~ ~ ~  |            | GND         30uH  C|    |   --- 470
               |       |            |3      1nF         C|    |   ###  uF
               |       |            |-------||--.       |     |    | +
               |       '-----+----+-'           |      GND    |   GND
               |            5|   4|             |             |
               |             |    '-------------o-------------o
               |             |                           ___  |
               `-------------*------/\/\/------------o--|___|-'
                                     2k              |       1k0
                                                    .+.
                                                    | | 5k6 + 3k3
                                                    | | in Serie
                                                    '+'
                                                     |
                                                    GND
```
`````

## `wavy`

## `finite`

유한 오토마타(Finite automata). 상세한 문서는 [매뉴얼](https://github.com/jneug/typst-finite/blob/main/manual.pdf)을 참조하세요.

```typ
#import "@preview/finite:0.3.0": automaton

#automaton((
  q0: (q1:0, q0:"0,1"),
  q1: (q0:(0,1), q2:"0"),
  q2: (),
))
```
