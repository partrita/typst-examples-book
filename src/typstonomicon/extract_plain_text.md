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
    // 필드가 없는 요소는 특별히 표현되거나(그리고 이전에 포착됨) 텍스트가 없습니다.
    ""
  } else {
    panic("Not sure how to handle type `" + repr(func) + "`")
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
    // 다른 모든 비텍스트 요소를 무시하려면 이것을 제거하세요.
    stringify-by-func(it)
  }
}

#plain-text(`raw inline text`)

#plain-text(highlight[강조된 텍스트])

#plain-text[목록
  - 포함
  - 일부
  - 요소

  + 그리고
  + 열거됨
  + 너무
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

// 일부 빈 요소
#plain-text(circle())
#plain-text(line())

#for spacer in (linebreak, pagebreak, parbreak) {
  plain-text(spacer())
}
```