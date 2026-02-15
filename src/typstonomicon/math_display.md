# 모든 수식을 디스플레이 모드로 설정

<div class="warning">
    수학 블록과 약간의 충돌이 발생할 수 있습니다.
</div>

```typ
// 저자: eric1102
#show math.equation: it => {
  if it.body.fields().at("size", default: none) != "display" {
    return math.display(it)
  }
  it
}

인라인 수식: $sum_(n=0)^oo e^(x^2 - n/x^2)$\
새로운 줄의 다른 텍스트.


$
sum_(n=0)^oo e^(x^2 - n/x^2)
$
```
