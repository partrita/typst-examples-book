# 사용자 정의 상자 (Custom boxes)

## Showbox

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  [Hello world!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

// First showybox
#showybox(
  frame: (
    border-color: red.darken(50%),
    title-color: red.lighten(60%),
    body-color: red.lighten(80%)
  ),
  title-style: (
    color: black,
    weight: "regular",
    align: center
  ),
  shadow: (
    offset: 3pt,
  ),
  title: "섹션이 분리된 붉은색 showybox!",
  lorem(20),
  lorem(12)
)

// Second showybox
#showybox(
  frame: (
    dash: "dashed",
    border-color: red.darken(40%)
  ),
  body-style: (
    align: center
  ),
  sep: (
    dash: "dashed"
  ),
  shadow: (
	  offset: (x: 2pt, y: 3pt),
    color: yellow.lighten(70%)
  ),
  [이것은 중요한 메시지입니다!],
  [밖을 조심하세요. 위험한 바나나가 있습니다!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  title: "스토크스 정리",
  frame: (
    border-color: blue,
    title-color: blue.lighten(30%),
    body-color: blue.lighten(95%),
    footer-color: blue.lighten(80%)
  ),
  footer: "잘 알려진 공개 백과사전에서 발췌한 정보"
)[
  $Sigma$를 경계 $diff Sigma equiv Gamma$를 갖는 $RR^3$의 매끄러운 방향성 표면이라 하자. 벡터 필드 $bold(F)(x,y,z)=(F_x (x,y,z), F_y (x,y,z), F_z (x,y,z))$가 정의되고 $Sigma$를 포함하는 영역에서 연속적인 1계 편미분을 갖는다면, 다음이 성립한다:

  $ integral.double_Sigma (bold(nabla) times bold(F)) dot bold(Sigma) = integral.cont_(diff Sigma) bold(F) dot dif bold(Gamma) $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  title-style: (
    weight: 900,
    color: red.darken(40%),
    sep-thickness: 0pt,
    align: center
  ),
  frame: (
    title-color: red.lighten(80%),
    border-color: red.darken(40%),
    thickness: (left: 1pt),
    radius: 0pt
  ),
  title: "카르노 사이클의 효율"
)[
  카르노 사이클 내에서 효율 $eta$는 다음과 같이 정의된다:

  $ eta = W/Q_H = frac(Q_H + Q_C, Q_H) = 1 - T_C/T_H $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  footer-style: (
    sep-thickness: 0pt,
    align: right,
    color: black
  ),
  title: "발산 정리",
  footer: [
    $n=3$인 경우, $V$는 3차원 공간의 부피를 나타내며, $diff V = S$는 그 표면이다.
  ]
)[
  $V$가 콤팩트하고 조각마다 매끄러운 경계 $S$($diff V = S$로도 표시)를 갖는 $RR^n$의 부분 집합이라고 가정하자. $bold(F)$가 $V$의 근방에서 정의된 연속적으로 미분 가능한 벡터 필드라면:

  $ integral.triple_V (bold(nabla) dot bold(F)) dif V = integral.surf_S (bold(F) dot bold(hat(n))) dif S $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  frame: (
    border-color: red.darken(30%),
    title-color: red.darken(30%),
    radius: 0pt,
    thickness: 2pt,
    body-inset: 2em,
    dash: "densely-dash-dotted"
  ),
  title: "가우스 법칙"
)[
  어떤 가상의 폐곡면을 통과하는 알짜 전기 선속은 그 폐곡면 내에 둘러싸인 알짜 전하의 $1/epsilon_0$배와 같다. 이 폐곡면은 가우스 면이라고도 한다. 적분 형태는 다음과 같다:

  $ Phi_E = integral.surf_S bold(E) dot dif bold(A) = Q/epsilon_0 $
]
```

## 다채로운 상자 (Colorful boxes)

```typ
#import "@preview/colorful-boxes:1.2.0": colorbox, slantedColorbox, outlinebox, stickybox

#colorbox(
  title: lorem(5),
  color: "blue",
  radius: 2pt,
  width: auto
)[
  #lorem(50)
]

#slantedColorbox(
  title: lorem(5),
  color: "red",
  radius: 0pt,
  width: auto
)[
  #lorem(50)
]

#outlinebox(
  title: lorem(5),
  color: none,
  width: auto,
  radius: 2pt,
  centering: false
)[
  #lorem(50)
]

#outlinebox(
  title: lorem(5),
  color: "green",
  width: auto,
  radius: 2pt,
  centering: true
)[
  #lorem(50)
]

#stickybox(
  rotation: 3deg,
  width: 7cm
)[
  #lorem(20)
]
```

## 정리 (Theorems)

[수학](./math.md)을 참조하세요.
