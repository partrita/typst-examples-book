# 쿼리 (Query)
<div class="warning">이 섹션은 완전하지 않을 수 있으며 최신 Typst 버전에 맞춰 충분히 업데이트되지 않았을 수 있습니다. 모든 기여를 환영합니다!</div>

> [공식 참조](https://typst.app/docs/reference/introspection/query/) 링크

쿼리(Query)는 _선택자(selector)_ (show 규칙에서 사용한 것과 동일)를 통해 _위치(location)_ (문서 내의 실제 위치를 나타내는 객체, [문서](https://typst.app/docs/reference/introspection/location/) 참조)를 가져올 수 있게 해줍니다.

이를 통해 문서의 일부에서 문서 전체에 대한 정보를 얻는 등 "시간 여행"이 가능해집니다. 이는 Typst의 순수성(purity)을 우회하는 방법입니다.

이것은 현재 Typst에 존재하는 가장 강력한 어둠의 마법 중 하나입니다. 큰 힘에는 큰 책임이 따릅니다.

## 시간 여행 (Time travel)

```typ
#let s = state("x", 0)
#let compute(expr) = [
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  새로운 값은 #context s.get() 입니다.
]

`<here>` 지점에서의 값은 다음과 같습니다:
#context s.at(
  query(<here>)
    .first()
    .location()
)

#compute("10") \
#compute("x + 3") \
*여기.* <here> \
#compute("x * 2") \
#compute("x - 5")
```

## 가장 가까운 장(Chapter) 가져오기
```typ
#set page(header: context {
  let elems = query(
    selector(heading).before(here())
  )
  let academy = smallcaps[
    Typst Academy
  ]
  if elems == () {
    align(right, academy)
  } else {
    let body = elems.last().body
    academy + h(1fr) + emph(body)
  }
})

= 서론
#lorem(23)

= 배경
#lorem(30)

= 분석
#lorem(15)
```
