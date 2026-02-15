# 무언가를 다른 무언가와 가로 정렬하기
```typ
// 저자: tabiasgeehuman
#let inline-with(select, content) = context {
  let target = query(
    selector(select)
  ).last().location().position().x
  let current = here().position().x

  box(inset: (x: target - current + 0.3em), content)
}

#let inline-label(name) = [#line(length: 0%) #name]

#inline-with(selector(<start-c>))[= 공통 값]
#align(left, box[$
    #inline-label(<start-c>) "원"(0) =& 0 \
    lim_(x -> 1) "원"(0) =& 0
$])
```
