# 0레벨 챕터 만들기

```typ
// 저자: tinger

#let chapter = figure.with(
  kind: "chapter",
  // 제목과 동일
  numbering: none,
  // 이것은 제목처럼 자동으로 번역하기 위해 auto를 사용할 수 없습니다. auto는 그림에 대해 다른 의미를 가집니다.
  supplement: "Chapter",
  // 개요에 포함되려면 빈 캡션이 필요합니다.
  caption: [],
)

// 요소 함수를 에뮬레이트하기 위해 표시 규칙 만들기
#show figure.where(kind: "chapter"): it => {
  set text(22pt)
  counter(heading).update(0)
  if it.numbering != none { strong(it.counter.display(it.numbering)) } + [ ] + strong(it.body)
}

// outline(indent: it => ...)에서 요소에 액세스할 수 없으므로 개요 대신 여기서 들여쓰기를 해야 합니다.
#show outline.entry: it => {
  if it.element.func() == figure {
    // 여기서 챕터 인쇄를 구성하고 있으며, 약간의 조정을 통해 기본 표시 구현을 효과적으로 다시 만듭니다.
    let res = link(it.element.location(), 
      // 위에서 표시 규칙의 일부를 다시 한 번 다시 만들어야 합니다.
      if it.element.numbering != none {
        numbering(it.element.numbering, ..it.element.counter.at(it.element.location()))
      } + [ ] + it.element.body
    )

    if it.fill != none {
      res += [ ] + box(width: 1fr, it.fill) + [ ] 
    } else {
      res += h(1fr)
    }

    res += link(it.element.location(), it.page())
    strong(res)
  } else {
    // 여기서 들여쓰기를 하고 있습니다.
    h(1em * it.level) + it
  }
}

// 기본 개요에 대한 새 대상 선택기
#let chapters-and-headings = figure.where(kind: "chapter", outlined: true).or(heading.where(outlined: true))

//
// 실제 문서 서문의 시작
//

#set heading(numbering: "1.")

// set을 사용할 수 없으므로 기본 인수로 다시 할당합니다.
#let chapter = chapter.with(numbering: "I")

// 챕터에 대한 "표시 규칙"의 예
// .with()를 사용한 후에는 더 이상 요소가 아니므로 챕터를 사용할 수 없습니다.
#show figure.where(kind: "chapter"): set text(red)

//
// 실제 문서의 시작
//

// 보시다시피 이것들은 제목과 같은 요소가 아니므로 설정이 조금 더 어렵습니다.
// 챕터가 제목이 아니기 때문에 번호 매기기에 챕터가 포함되지 않지만 제목에 대한 표시 규칙을 사용할 수 있습니다.

#outline(target: chapters-and-headings)

#chapter[챕터]
= 챕터 제목
== 하위 제목

#chapter[다시 챕터]
= 챕터 제목
= 챕터 제목
== 하위 제목
=== 하위 하위 제목
== 하위 제목

#chapter[또 다시 챕터]
```