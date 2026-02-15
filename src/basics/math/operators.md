# 연산자 (Operators)

> [참조](https://typst.app/docs/reference/math/op/) 링크

Typst 수학 환경에는 수많은 내장 "텍스트 연산자"가 있습니다. 이들은 일반 텍스트와 매우 비슷하게 동작하지만, 분명히 다릅니다:

```typ
$
lim x_n, "lim" x_n, "lim"x_n
$
```
## 사전 정의된 연산자

Typst에 내장된 모든 텍스트 연산자는 다음과 같습니다:

```typ
$
arccos, arcsin, arctan, arg, cos, cosh, cot, coth, csc,\
csch, ctg, deg, det, dim, exp, gcd, hom, id, im, inf, ker,\
lg, lim, liminf, limsup, ln, log, max, min, mod, Pr, sec,\
sech, sin, sinc, sinh, sup, tan, tanh, tg "및" tr
$
```

## 사용자 정의 연산자 만들기

물론 목록에 없는 텍스트 연산자가 필요한 경우도 있을 것입니다.

걱정하지 마세요. 직접 추가하는 것은 매우 쉽습니다:

```typ
#let arcsinh = math.op("arcsinh")

$
arcsinh x
$
```

### 연산자의 극한 (Limits for operators)

연산자(적절한 간격을 가진 직립 텍스트)를 만들 때, 동시에 _디스플레이 모드_를 위한 극한을 설정할 수 있습니다:

```typ
$
op("liminf")_a, op("liminf", limits: #true)_a
$
```

이것은 대략 다음과 동일합니다.

```typ
$
limits(op("liminf"))_a
$
```

모든 것을 조합하여 새로운 연산자를 만들 수 있습니다:

```typ
#let liminf = math.op(math.underline(math.lim), limits: true)
#let limsup = math.op(math.overline(math.lim), limits: true)
#let integrate = math.op($integral dif x$)

$
liminf_(x->oo)\
limsup_(x->oo)\
integrate x^2
$
```
