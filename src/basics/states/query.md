# 쿼리
<div class="warning">이 섹션은 최신 Typst 버전에 대해 완전히 완전하거나 업데이트되지 않았을 수 있습니다. 어떤 기여든 매우 환영합니다!.</div>

> [참조](https://typst.app/docs/reference/introspection/query/) 링크

쿼리는 _선택자_([표시 규칙](#show-rule)에서 사용한 것과 동일한 것)를 사용하여 _위치_([문서의 장소를 말 그대로 나타내는 객체, 여기 문서 참조](https://typst.app/docs/reference/introspection/location/))를 얻을 수 있는 것입니다.

이를 통해 "시간 여행", 문서의 일부에서 문서에 대한 정보 얻기 등이 가능합니다. _이것은 Typst의 순수성을 위반하는 방법입니다._

이것은 현재 _Typst에 존재하는 가장 어두운 마법_ 중 하나입니다. 큰 힘을 주지만, 큰 힘에는 큰 책임이 따릅니다.

## 시간 여행

```typ
#let s = state("x", 0)
#let compute(expr) = [
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  새 값은 #context s.get()입니다.
]

`<here>`의 값은
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

## 가장 가까운 챕터 가져오기
```typ
#set page(header: context {
  let elems = query(
    selector(heading).before(here())
  )
  let academy = smallcaps[
    Typst 아카데미
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
