# 기호 (Symbols)

수학에서 다중 문자 단어는 지역 변수, 함수, 텍스트 연산자, 간격 또는 _특수 기호_를 나타냅니다.
후자는 고급 수학에서 매우 중요합니다.

```typ
$
forall v, w in V, alpha in KK: alpha dot (v + w) = alpha v + alpha w
$
```

유니코드를 사용하여 똑같이 작성할 수 있습니다:

```typ
$
∀ v, w ∈ V, α ∈ 𝕂: α ⋅ (v + w) = α v + α w
$
```

## 기호 명명법 (Symbols naming)

> 사용 가능한 모든 기호 목록은 [여기](https://typst.app/docs/reference/symbols/sym/)를 참조하세요.

### 일반적인 아이디어

Typst는 기억하기 쉬운 짧은 단어로 일부 "기본" 기호를 정의하고, 이를 조합하여 복잡한 기호를 만듭니다. 예를 들어:

```typ
$
// cont — contour (폐곡선)
integral, integral.cont, integral.double, integral.square, sum.integral\

// lt — less than (미만), gt — greater than (초과)
lt, lt.circle, lt.eq, lt.not, lt.eq.not, lt.tri, lt.tri.eq, lt.tri.eq.not, gt, lt.gt.eq, lt.gt.not
$
```

복잡한 기호가 많이 포함된 수학을 작성할 때는 WebApp이나 Typst LSP를 사용하는 것을 적극 권장합니다.
다양한 조합 중에서 올바른 기호를 빠르게 선택하는 데 도움이 됩니다.

가끔 이름이 직관적이지 않은 경우가 있는데, 예를 들어 `not` 대신 접두사 `n-`을 사용하는 경우가 있습니다:

```typ
$
gt.nequiv, gt.napprox, gt.ntilde, gt.tilde.not
$
```


### 일반적인 수정자 (Modifiers)

- `.b, .t, .l, .r`: bottom, top, left, right. 기호의 방향을 바꿉니다.
    ```typ
    $arrow.b, triangle.r, angle.l$
    ```
- `.bl, tr`: bottom-left, top-right 등. 대각선 방향이 가능한 경우 사용합니다.
- `.bar, .circle, .times, ...`: 기호에 해당 요소를 추가합니다.
- `.double, .triple, .quad`: 기호를 2, 3, 4번 결합합니다.
- `.not`: 기호에 사선을 긋습니다.
- `.cw, .ccw`: clock-wise(시계 방향) 및 counter-clock-wise(반시계 방향). 화살표 등에 사용됩니다.
- `.big, .small`: 크기를 조절합니다.
    ```typ
    $plus.circle.big plus.circle, times.circle.big plus.circle$
    ```
- `.filled`: 기호 내부를 채웁니다.
    ```typ
    $square, square.filled, diamond.filled, arrow.filled$
    ```

### 그리스 문자

소문자는 소문자로 시작하고, 대문자는 대문자로 시작합니다.

다른 형태의 글자를 사용하려면 `.alt`를 붙입니다.

```typ
$
alpha, Alpha, beta, Beta, beta.alt, gamma, pi, Pi,\
pi.alt, phi, phi.alt, Phi, omicron, kappa, kappa.alt, Psi,\
theta, theta.alt, xi, zeta, rho, rho.alt, kai, Kai,
$
```

### 칠판 볼드체 (Blackboard letters)

글자를 두 번 겹쳐 쓰세요. 다른 기호를 칠판 볼드체로 만들려면 `bb`를 사용합니다:

```typ
$bb(A), AA, bb(1)$
```

## 글꼴 문제 (Fonts issues)

기본 글꼴은 **New Computer Modern Math**입니다. 좋은 글꼴이지만 몇 가지 불일치가 있을 수 있습니다.

Typst는 기호 이름을 유니코드에 매핑하므로, 글꼴에 잘못된 기호가 있는 경우 Typst는 잘못된 기호를 표시합니다.

### 공집합 (Empty set)
예시를 확인하세요:

```typ
// 기본 수학 글꼴의 nothing 기호는 좋지 않습니다.
$nothing, nothing.rev, diameter$

#show math.equation: set text(font: "Fira Math")

// Fira math가 더 일관성이 있습니다.
$nothing, nothing.rev, diameter$
```

하지만 글꼴 기능(font feature)으로 이를 수정할 수 있습니다:

```typ
#show math.equation: set text(features: ("cv01",))

$nothing, nothing.rev, diameter$
```

또는 간단히 "show" 규칙을 사용할 수도 있습니다:

```typ
#show math.nothing: math.diameter

$nothing, nothing.rev, diameter$
```
