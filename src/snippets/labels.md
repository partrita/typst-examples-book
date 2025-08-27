# 레이블
## 레이블의 챕터 가져오기
```typ
#let ref-heading(label) = context {
  let elems = query(label)
  if elems.len() != 1 {
    panic("found multiple elements")
  }
  let element = elems.first()
  if element.func() != heading {
    panic("label must target heading")
  }
  link(label, element.body)
}

= 디자인 <design>
#lorem(20)

= 구현
#ref-heading(<design>)에서 논의했듯이...
```

## 누락된 참조 허용

```typ
// 저자: Enivex
#set heading(numbering: "1.")

#let myref(label) = context {
    if query(label).len() != 0 {
        ref(label)
    } else {
        // 누락된 참조
        text(fill: red)[???]
    }
}

= 두 번째 <test2>

#myref(<test>)

#myref(<test2>)
```