## 여러 표시 규칙

때로는 매우 유사해 보이는 여러 규칙을 적용해야 할 필요가 있습니다. 또는 코드에서 생성해야 합니다. 이것을 다루는 방법 중 하나, 가장 저주받은 방법은 다음과 같습니다:

```typ
#let rules = (math.sum, math.product, math.root)

#let apply-rules(rules, it) = {
  if rules.len() == 0 {
    return it
  }
  show rules.pop(): math.display
  apply-rules(rules, it)
}

$product/sum root(3, x)/2$

#show: apply-rules.with(rules)

$product/sum root(3, x)/2$
```

재귀 문제는 기본적으로 동일한 아이디어로 `fold`의 힘으로 피할 수 있습니다:

```typ
// 저자: Eric
#let kind_supp = (code: "Listing", algo: "Algorithme")
#show: it => kind_supp.pairs().fold(it, (acc, (kind, supp)) => {
  show figure.where(kind: kind): set figure(supplement: supp)
  acc
})
```

기호의 경우(요소 함수가 필요하지 않은 경우) 정규식을 사용할 수 있습니다. 이것이 더 강력한 방법입니다:

```typ
#show regex("[" + math.product + math.sum + "]"): math.display

$product/sum root(3, x)/2$
```
