# 레이블 (Labels)
## 레이블의 장(Chapter) 정보 가져오기
```typ
#let ref-heading(label) = context {
  let elems = query(label)
  if elems.len() != 1 {
    panic("여러 요소가 발견되었습니다")
  }
  let element = elems.first()
  if element.func() != heading {
    panic("레이블이 제목(heading)을 대상으로 해야 합니다")
  }
  link(label, element.body)
}

= 디자인 <design>
#lorem(20)

= 구현
#ref-heading(<design>) 에서 논의했듯이...
```

## 존재하지 않는 참조 허용하기

```typ
// 저자: Enivex
#set heading(numbering: "1.")

#let myref(label) = context {
    if query(label).len() != 0 {
        ref(label)
    } else {
        // 존재하지 않는 참조
        text(fill: red)[???]
    }
}

= 두 번째 <test2>

#myref(<test>)

#myref(<test2>)
```
