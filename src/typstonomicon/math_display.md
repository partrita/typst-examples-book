# 모든 수학을 디스플레이 수학으로 만들기

<div class="warning">
    수학 블록과 약간 충돌할 수 있습니다.
</div>

```typ
// 저자: eric1102
#show math.equation: it => {
  if it.body.fields().at("size", default: none) != "display" {
    return math.display(it)
  }
  it
}

인라인 수학: $sum_(n=0)^oo e^(x^2 - n/x^2)$\ 
새 줄에 다른 텍스트.


$
sum_(n=0)^oo e^(x^2 - n/x^2)
$
```
