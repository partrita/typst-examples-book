# 연산자

> [참조](https://typst.app/docs/reference/math/op/)를 참조하세요.

Typst 수학에는 많은 내장 "텍스트 연산자"가 있습니다. 이것은 일반 텍스트와 매우 유사하게 작동하는 기호입니다. 그럼에도 불구하고 다릅니다:

```typ
$
lim x_n, "lim" x_n, "lim"x_n
$
```
## 미리 정의된 연산자

Typst에 내장된 모든 텍스트 연산자는 다음과 같습니다:

```typ
$
arccos, arcsin, arctan, arg, cos, cosh, cot, coth, csc,\
csch, ctg, deg, det, dim, exp, gcd, hom, id, im, inf, ker,\
lg, lim, liminf, limsup, ln, log, max, min, mod, Pr, sec,\
sech, sin, sinc, sinh, sup, tan, tanh, tg "and" tr
$
```

## 사용자 정의 연산자 만들기

물론, 목록에 없는 필요한 텍스트 연산자가 항상 있을 것입니다.

하지만 걱정하지 마세요, 자신만의 연산자를 추가하는 것은 매우 쉽습니다:

```typ
#let arcsinh = math.op("arcsinh")

$
arcsinh x
$
```

### 연산자에 대한 한계

연산자(적절한 간격이 있는 정자체 텍스트)를 만들 때 _디스플레이 모드_에 대한 한계를 동시에 설정할 수 있습니다:

```typ
$
op("liminf")_a, op("liminf", limits: #true)_a
$
```

이것은 대략 다음과 같습니다.

```typ
$
limits(op("liminf"))_a
$
```

모든 것을 결합하여 새 연산자를 만들 수 있습니다:

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
