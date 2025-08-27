# 사용자 정의 상자

## Showybox

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  [안녕하세요, 세상!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

// 첫 번째 showybox
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
  title: "분리된 섹션이 있는 빨간색 showybox!",
  lorem(20),
  lorem(12)
)

// 두 번째 showybox
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
  [밖은 위험하니 조심하세요. 위험한 바나나가 있습니다!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  title: "스토크스의 정리",
  frame: (
    border-color: blue,
    title-color: blue.lighten(30%),
    body-color: blue.lighten(95%),
    footer-color: blue.lighten(80%)
  ),
  footer: "잘 알려진 공개 백과사전에서 발췌한 정보"
)[
  $Sigma$를 경계 $diff Sigma equiv Gamma$를 갖는 $RR^3$의 매끄러운 유향 곡면이라고 가정합니다. 벡터 필드 $bold(F)(x,y,z)=(F_x (x,y,z), F_y (x,y,z), F_z (x,y,z))$가 $Sigma$를 포함하는 영역에서 정의되고 연속적인 1계 편도함수를 갖는 경우,

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
  title: "카르노 사이클의 효율성"
)[
  카르노 사이클 내부에서 효율성 $eta$는 다음과 같이 정의됩니다:

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
    $n=3$의 경우, $V$는 3차원 공간의 부피를 나타내고 $diff V = S$는 그 표면입니다
  ]
)[
  $V$가 조각적으로 매끄러운 경계 $S$(또한 $diff V = S$로 표시됨)를 갖는 $RR^n$의 부분 집합이라고 가정합니다. $bold(F)$가 $V$의 근방에서 정의된 연속적으로 미분 가능한 벡터 필드인 경우:

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
  title: "가우스의 법칙"
)[
  가상 폐쇄 표면을 통과하는 순 전기 선속은 해당 폐쇄 표면 내에 둘러싸인 순 전하량의 $1/epsilon_0$배와 같습니다. 폐쇄 표면은 가우스 표면이라고도 합니다. 적분 형태:

  $ Phi_E = integral.surf_S bold(E) dot dif bold(A) = Q/epsilon_0 $
]
```

## 다채로운 상자

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

## 정리

[수학](./math.md) 참조