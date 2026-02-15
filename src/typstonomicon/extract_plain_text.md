# 일반 텍스트 추출
```typ
// 원저자: ntjess
#let stringify-by-func(it) = {
  let func = it.func()
  return if func in (parbreak, pagebreak, linebreak) {
    "\n"
  } else if func == smartquote {
    if it.double { "\"" } else { "'" } // "
  } else if it.fields() == (:) {
    // 필드가 없는 요소는 특별히 표현되거나(미리 처리됨) 텍스트가 없음
    ""
  } else {
    panic("타입 `" + repr(func) + "`을(를) 처리하는 방법을 모르겠습니다.")
  }
}

#let plain-text(it) = {
  return if type(it) == str {
    it
  } else if it == [ ] {
    " "
  } else if it.has("children") {
    it.children.map(plain-text).join()
  } else if it.has("body") {
    plain-text(it.body)
  } else if it.has("text") {
    if type(it.text) == str {
      it.text
    } else {
      plain-text(it.text)
    }
  } else {
    // 다른 텍스트가 아닌 요소를 무시하려면 이 부분을 제거하세요
    stringify-by-func(it)
  }
}

#plain-text(`raw 인라인 텍스트`)

#plain-text(highlight[강조된 텍스트])

#plain-text[목록
  - 일부
  - 요소를
  - 포함함

  + 그리고
  + 번호 매기기도
  + 포함함
]

#plain-text(underline[밑줄])

#plain-text($sin(x + y)$)

#for el in (
  circle,
  rect,
  ellipse,
  block,
  box,
  par,
  raw.with(block: true),
  raw.with(block: false),
  heading,
) {
  plain-text(el(repr(el)))
  linebreak()
}

// 일부 빈 요소들
#plain-text(circle())
#plain-text(line())

#for spacer in (linebreak, pagebreak, parbreak) {
  plain-text(spacer())
}
```
