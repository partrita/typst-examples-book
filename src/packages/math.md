# 수학

## 일반
### `physica`

> Physica(라틴어로 _자연 과학_)는 자연 과학에서 복잡하고 반복적인 수학적 표현을 단순화하는 유틸리티를 제공합니다.

> [설명서](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)는 패키지가 어떻게 도움이 될 수 있는지에 대한 전체 데모 세트를 제공합니다.

#### 일반적인 표기법

* 미적분학: 미분, 상미분 및 편미분
  * 선택적 함수 이름,
  * 선택적 순서 번호 또는 그 배열,
  * 사용자 정의 가능한 "d" 기호 및 곱 결합자(예: 외적),
  * 재정의 가능한 총 순서 계산,
* 벡터 및 벡터장: 발산, 기울기, 회전,
* 테일러 전개,
* 디랙 브라켓 표기법,
* 추상 인덱스 표기법이 있는 텐서,
* 행렬 전치 및 대거(켤레 전치).
* 특수 행렬: 행렬식, (반)대각, 항등, 영, 야코비,
헤세 등 <!-- TODO physica:0.9.2에 회전 및 그램 행렬 추가 -->

아래는 이러한 표기법의 미리보기입니다.

```typ
#import "@preview/physica:0.9.1": * // 아래에 주석이 달린 기호 이름

#table(
  columns: 4, align: horizon, stroke: none, gutter: 1em,

  // 벡터: 굵게, 단위, 화살표
  [$ vb(a), vb(e_i), vu(a), vu(e_i), va(a), va(e_i) $],
  // dprod(내적), cprod(외적), iprod(내적)
  [$ a dprod b, a cprod b, iprod(a, b) $],
  // 라플라시안(내장 라플라스와 다름)
  [$ dot.double(u) = laplacian u =: laplace u $],
  // 기울기, 발산, 회전(벡터장)
  [$ grad phi, div vb(E), \ curl vb(B) $],
)
```

```typ
#import "@preview/physica:0.9.1": * // 아래에 주석이 달린 기호 이름

#table(
  columns: 4, align: horizon, stroke: none, gutter: 1em,

  // 행 1.
  // dd(미분), var(변분), difference(차분)
  [$ dd(f), var(f), difference(f) $],
  // dd, 순서 번호 또는 그 배열 포함
  [$ dd(x,y), dd(x,y,2), \ dd(x,y,[1,n]), dd(vb(x),t,[3,]) $],
  // dd, 사용자 정의 "d" 기호 및 결합자 포함
  [$ dd(x,y,p:and), dd(x,y,d:Delta), \ dd(x,y,z,[1,1,n+1],d:d,p:dot) $],
  // dv(상미분), 사용자 정의 "d" 기호 및 결합자 포함
  [$ dv(phi,t,d:Delta), dv(phi,t,d:upright(D)), dv(phi,t,d:delta) $],

  // 행 2.
  // dv, 선택적 함수 이름 및 순서 포함
  [$ dv(,t) (dv(x,t)) = dv(x,t,2) $],
  // pdv(편미분)
  [$ pdv(f,x,y,2), pdv(,x,y,[k,]) $],
  // pdv, 재정의 가능한 총합 자동 추가
  [$ pdv(,x,y,[i+2,i+1]), pdv(,y,x,[i+1,i+2],total:3+2i) $],
  // 플랫 형식으로
  [$ dv(u,x,s:slash), \ pdv(u,x,y,2,s:slash) $],
)
```

<!--
// TODO physica:0.9.2가 병합되면 Order/order 추가.
// TODO physica:0.9.2가 병합되면 expval(A, phi) 데모.
-->
```typ
#import "@preview/physica:0.9.1": * // 아래에 주석이 달린 기호 이름

#table(
  columns: 3, align: horizon, stroke: none, gutter: 1em,

  // 텐서
  [$ tensor(T,+a,-b,-c) != tensor(T,-b,-c,+a) != tensor(T,+a',-b,-c) $],
  // 집합 빌더 표기법
  [$ Set(p, {q^*, p} = 1) $],
  // taylorterm(테일러 급수 항)
  [$ taylorterm(f,x,x_0,1) \ taylorterm(f,x,x_0,(n+1)) $],
)
```
```typ
#import "@preview/physica:0.9.1": * // 아래에 주석이 달린 기호 이름

#table(
  columns: 3, align: horizon, stroke: none, gutter: 1em,

  // expval(평균/기댓값), eval(평가 경계)
  [$ expval(X) = eval(f(x)/g(x))^oo_1 $],
  // 디랙 브라켓 표기법
  [$
    bra(u), braket(u), braket(u, v), \
    ket(u), ketbra(u), ketbra(u, v), \
    mel(phi, hat(p), psi) $],
  // 명시적으로 활성화해야 하는 위 첨자 표시 규칙.
  // 콘텐츠 블록에 넣으면 해당 블록의 범위만 제어합니다.
  [
    #show: super-T-as-transpose // "..^T" 필기처럼
    #show: super-plus-as-dagger // "..^+" 필기처럼
    $ op("conj")A^T =^"def" A^+ \
      e^scripts(T), e^scripts(+) $ ], // scripts()로 재정의
)
```

#### 행렬

Typst의 내장 `mat()` 외에도 physica는 행렬을 더 쉽게 작성할 수 있도록 여러 가지 편리한 도구를 제공합니다.

```typ
#import "@preview/physica:0.9.1": TT, mdet

$
// "TT"를 사용한 행렬 전치, 하지만 "A^T"도 작동하도록
// super-T-as-transpose를 사용하는 것이 좋습니다(나중에 자세히 설명).
A^TT,
// "mdet(...)"를 사용한 행렬식.
det mat(a, b; c, d) := mdet(a, b; c, d)
$
```

대각 행렬 `dmat(...)`, 반대각 행렬 `admat(...)`,
항등 행렬 `imat(n)` 및 영 행렬 `zmat(n)`.
```typ
#import "@preview/physica:0.9.1": dmat, admat, imat, zmat

$ dmat(1, 2)  dmat(1, a_1, xi, fill:0)               quad
  admat(1, 2) admat(1, a_1, xi, fill:dot, delim:"[") quad
  imat(2)     imat(3, delim:"{",fill:*) quad
  zmat(2)     zmat(3, delim:"|") $
```

`jmat(func; ...)` 또는 더 긴 이름 `jacobianmatrix`를 사용한 야코비 행렬,
`hmat(func; ...)` 또는 더 긴 이름 `hessianmatrix`를 사용한 헤세 행렬, 그리고
마지막으로 행렬을 빌드하기 위한 `xmat(row, col, func)`.
```typ
#import "@preview/physica:0.9.1": jmat, hmat, xmat

$
jmat(f_1,f_2; x,y) jmat(f,g; x,y,z; delim:"[") quad
hmat(f; x,y)       hmat(; x,y; big:#true)      quad

#let elem-ij = (i,j) => $g^(#(i - 1)#(j - 1)) = #calc.pow(i,j)$
xmat(2, 2, #elem-ij)
$
```

### `mitex`

> MiTeX는 Typst에서 WASM으로 구동되는 LaTeX 지원을 제공하며, LaTeX 수학 방정식의 실시간 렌더링을 포함합니다.
> LaTeX 구문을 사용하여 `\ref` 및 `\label`을 작성할 수도 있습니다.

> 자세한 내용은 [설명서](https://github.com/mitex-rs/mitex)를 참조하세요.

```typ
#import "@preview/mitex:0.2.4": *

#mi("x") 또는 #mi[y]와 같은 인라인 방정식을 작성합니다.

또한 블록 방정식:

#mitex(`
  \newcommand{\f}[2]{#1f(#2)}
  \f\relax{x} = \int_{-\infty}^\infty
    \f\hat\xi\,e^{2 \pi i \xi x}
    \,d\xi
`)

텍스트 모드:

#mitext(`
  \iftypst
    #set math.equation(numbering: "(1)", supplement: "equation")
  \fi

  인라인 방정식 $x + y$ 및 블록 \eqref{eq:pythagoras}.

  \begin{equation}
    a^2 + b^2 = c^2 \label{eq:pythagoras}
  \end{equation}
`)
```


### `i-figured`

Typst에서 섹션별로 구성 가능한 방정식 번호 매기기.
섹션별 그림 번호 매기기도 있으며, 자세한 예는 [설명서](https://github.com/RubixDev/typst-i-figured)에서 확인하세요.


```typ
#import "@preview/i-figured:0.2.3"

// 제목 번호 매기기가 설정되어 있는지 확인하세요
#set heading(numbering: "1.1")

// 표시 규칙 적용(사용자 정의 가능)
#show heading: i-figured.reset-counters
#show math.equation: i-figured.show-equation.with(
  level: 1,
  zero-fill: true,
  leading-zero: true,
  numbering: "(1.1)",
  prefix: "eqt:",
  only-labeled: false,  // 모든 블록 방정식을 암시적으로 번호 매기기
  unnumbered-label: "-",
)


= 서론

$x + y$와 같은 인라인 방정식을 작성할 수 있으며, 다음과 같이 번호가 매겨진 블록 방정식도 작성할 수 있습니다:

$ phi.alt := (1 + sqrt(5)) / 2 $ <ratio>

수학 방정식을 참조하려면 `eqt:` 접두사를 사용하세요. 예를 들어, @eqt:ratio를 사용하면 다음과 같습니다:

$ F_n = floor(1 / sqrt(5) phi.alt^n) $


= 부록

또한, <-> 태그를 사용하여 블록 수식에 번호를 매기지 않아야 함을 나타낼 수 있습니다:

$ y = integral_1^2 x^2 dif x $ <->

이후의 수학 방정식은 평소와 같이 계속 번호가 매겨집니다:

$ F_n = floor(1 / sqrt(5) phi.alt^n) $
```



## 정리
### `ctheorem`

Typst의 번호 매기기 정리 환경. 자세한 예는
[설명서](https://github.com/sahasatvik/typst-theorems/blob/main/manual.pdf)에서 확인하세요.

```typ
#import "@preview/ctheorems:1.1.0": *
#show: thmrules

#set page(width: 16cm, height: auto, margin: 1.5cm)
#set heading(numbering: "1.1")

#let theorem = thmbox("theorem", "Theorem", fill: rgb("#eeffee"))
#let corollary = thmplain("corollary", "Corollary", base: "theorem", titlefmt: strong)
#let definition = thmbox("definition", "Definition", inset: (x: 1.2em, top: 1em))

#let example = thmplain("example", "Example").with(numbering: none)
#let proof = thmplain(
  "proof", "Proof", base: "theorem",
  bodyfmt: body => [#body #h(1fr) $square$]
).with(numbering: none)

= 소수
#lorem(7)
#definition[ 자연수는 ...인 경우 #highlight[_소수_]라고 합니다. ]
#example[
  숫자 $2$, $3$, $17$은 소수입니다. @cor_largest_prime은 이 목록이 완전하지 않음을 보여줍니다!
]
#theorem("유클리드")[소수는 무한히 많습니다.]
#proof[
  모든 소수의 유한한 열거가 $p_1, p_2, dots, p_n$이라고 가정합니다. ... 모순입니다.
]
#corollary[
  가장 큰 소수는 없습니다.
] <cor_largest_prime>
#corollary[합성수는 무한히 많습니다.]
```

### `lemmify`

Lemmify는 많은 선택자 및 번호 매기기 기능이 있는 또 다른 정리 환경 생성기입니다. [readme](https://github.com/Marmare314/lemmify)에서 문서를 참조하세요.

```typ
#import "@preview/lemmify:0.1.5": *

#let my-thm-style(
  thm-type, name, number, body
) = grid(
  columns: (1fr, 3fr),
  column-gutter: 1em,
  stack(spacing: .5em, [#strong(thm-type) #number], emph(name)),
  body
)
#let my-styling = ( thm-styling: my-thm-style )
#let (
  definition, theorem, proof, lemma, rules
) = default-theorems("thm-group", lang: "en", ..my-styling)
#show: rules
#show thm-selector("thm-group"): box.with(inset: 0.8em)
#show thm-selector("thm-group", subgroup: "theorem"): it => box(
  it, fill: rgb("#eeffee"))

#set heading(numbering: "1.1")

= 소수
#lorem(7) @proof 및 @thm[정리]
#definition[ 자연수는 ...인 경우 #highlight[_소수_]라고 합니다. ]
#theorem(name: "정리 이름")[소수는 무한히 많습니다.]<thm>
#proof[
  모든 소수의 유한한 열거가 $p_1, p_2, dots, p_n$이라고 가정합니다. ... #highlight[_모순_].]<proof>
#lemma[합성수는 무한히 많습니다.]
```

### `frame-it`
[Frame-It](https://typst.app/universe/package/frame-it/)은 2개의 미리 정의된 스타일과 임의의 사용자 정의 스타일을 정의하는 옵션으로 정리를 강조 표시할 수 있습니다.
프레임에 색상이 제공되지 않으면 자동으로 생성됩니다.
문서는 [README](https://github.com/marc-thieme/frame-it)를 참조하세요.

```typst
#import "@preview/frame-it:1.0.0": *

// 필요한 프레임 종류를 정의해야 합니다
#let (theorem, lemma, definition, important) = make-frames(
  // 이 정의의 모든 정리에 사용되는 카운터를 식별합니다
  "counter-id",
  theorem: ("정리",),
  // 색상을 제공하거나 생략하면 생성됩니다
  lemma: ("보조 정리", gray),
  // 각 프레임 종류에 대해 표시할 보충 제목을 제공해야 합니다
  definition: ("정의",),
  // 원하는 만큼 추가할 수 있습니다
  important: ("중요", blue.lighten(25%)),
)

= 소수

프레임에는 제목이 있습니다.

#definition[소수][
  1보다 큰 자연수는 1과 자신으로만 나누어 떨어지는 경우 _소수_라고 합니다. 예를 들어, 2, 3, 5, 7은 모두 소수입니다.
]

원하는 경우 생략할 수도 있습니다.

#lemma[][2보다 큰 각 소수는 2로 나누어 떨어지거나 홀수이지만, 2 자체를 제외한 다른 짝수로는 나누어 떨어지지 않습니다.
]

사용자 정의 스타일이 필요한 경우 프로젝트 README를 참조하여 사용자 정의 스타일링 함수를 정의하는 방법을 확인하세요.
기본적으로 두 가지 다른 스타일이 미리 정의되어 있습니다.
이것은 두 번째 스타일입니다:

#important(style: styles.hint)[고유 소인수 분해][주의][
  1보다 큰 모든 양의 정수는 소수로 고유하게 인수분해될 수 있습니다. 이것은 산술의 기본 정리로 알려져 있습니다. 정수론에서 정수의 구조를 이해하는 데 중요합니다.
]

추가 정보가 있는 태그를 추가하는 추가 기능이 있습니다

#theorem[유클리드의 정리][매우 중요][시험 관련][
  소수는 무한히 많습니다. 이 정수론의 기본 결과는 발견된 소수 집합이 아무리 크더라도 소수가 고갈될 수 없음을 보여줍니다.
]
```
