# 기호

수학에서 여러 글자로 된 단어는 지역 변수, 함수, 텍스트 연산자, 간격 또는 _특수 기호_를 나타냅니다.
후자는 고급 수학에 매우 중요합니다.

```typ
$
forall v, w in V, alpha in KK: alpha dot (v + w) = alpha v + alpha w
$
```

유니코드로 동일하게 작성할 수 있습니다:

```typ
$
∀ v, w ∈ V, α ∈ 𝕂: α ⋅ (v + w) = α v + α w
$
```

## 기호 이름 지정

> 사용 가능한 모든 기호 목록은 [여기](https://typst.app/docs/reference/symbols/sym/)에서 확인하세요.

### 일반적인 아이디어

Typst는 작고 기억하기 쉬운 단어로 일부 "기본" 기호를 정의하고,
조합을 사용하여 복잡한 기호를 만드는 것을 목표로 합니다. 예를 들어,

```typ
$
// cont — 윤곽선
integral, integral.cont, integral.double, integral.square, sum.integral\

// lt — 보다 작음, gt — 보다 큼
lt, lt.circle, lt.eq, lt.not, lt.eq.not, lt.tri, lt.tri.eq, lt.tri.eq.not, gt, lt.gt.eq, lt.gt.not
$
```

복잡한 기호가 많은 수학을 작성할 때는 WebApp/Typst LSP를 사용하는 것을 강력히 권장합니다.
이를 통해 모든 조합 내에서 올바른 기호를 빠르게 선택할 수 있습니다.

때로는 이름이 명확하지 않을 수 있습니다. 예를 들어, 때로는 `not` 대신 접두사 `n-`이 사용됩니다:

```typ
$
gt.nequiv, gt.napprox, gt.ntilde, gt.tilde.not
$
```


### 일반적인 수정자

- `.b, .t, .l, .r`: 아래, 위, 왼쪽, 오른쪽. 기호의 방향을 변경합니다.
    ```typ
    $arrow.b, triangle.r, angle.l$
    ```
- `.bl, tr`: 왼쪽 아래, 오른쪽 위 등. 대각선 방향이 가능한 경우.
- `.bar, .circle, .times, ...`: 기호에 해당 요소를 추가합니다.
- `.double, .triple, .quad`: 기호를 2, 3 또는 4번 결합합니다.
- `.not`은 기호를 가로지릅니다.
- `.cw, .ccw`: 시계 방향 및 반시계 방향. 화살표 및 기타 항목용.
- `.big, .small`:
    ```typ
    $plus.circle.big plus.circle, times.circle.big plus.circle$
    ```
- `.filled`: 기호를 채웁니다.
    ```typ
    $square, square.filled, diamond.filled, arrow.filled$
    ```

### 그리스 문자

소문자는 소문자로 시작하고, 대문자는 대문자로 시작합니다.

다른 버전의 문자는 `.alt`를 사용하세요.

```typ
$
alpha, Alpha, beta, Beta, beta.alt, gamma, pi, Pi,\
pi.alt, phi, phi.alt, Phi, omicron, kappa, kappa.alt, Psi,\
theta, theta.alt, xi, zeta, rho, rho.alt, kai, Kai,
$
```

### 칠판 문자

그냥 두 번 사용하세요. 다른 기호를 칠판 문자로 만들고 싶다면 `bb`를 사용하세요:

```typ
$bb(A), AA, bb(1)$
```

## 글꼴 문제

기본 글꼴은 **New Computer Modern Math**입니다. 좋은 글꼴이지만 몇 가지 불일치가 있습니다.

Typst는 기호 이름을 유니코드에 매핑하므로, 글꼴에 잘못된 기호가 있으면 Typst는 잘못된 기호를 표시합니다.

### 공집합
예제를 보세요:

```typ
// 기본 수학 글꼴의 nothing은 좋지 않습니다
$nothing, nothing.rev, diameter$

#show math.equation: set text(font: "Fira Math")

// Fira math가 더 일관성이 있습니다
$nothing, nothing.rev, diameter$
```

그러나 글꼴 기능으로 이 문제를 해결할 수 있습니다:

```typ
#show math.equation: set text(features: ("cv01",))

$nothing, nothing.rev, diameter$
```

또는 단순히 "show" 규칙을 사용하세요:

```typ
#show math.nothing: math.diameter

$nothing, nothing.rev, diameter$
```