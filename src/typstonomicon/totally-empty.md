# 번호 없는 빈 페이지

## 홀수 페이지에서 시작하는 장(Chapter) 앞의 빈 페이지

<div class="warning">
  이 스니펫은 0.12.0 버전에서 작동하지 않습니다. 수정을 도와주실 분이 있다면 정말 감사하겠습니다.
</div>

`````typ -norender
// 저자: janekfleper

#set page(height: 20em)

#let find-labels(name) = {
  return query(name).map(label => label.location().page())
}

#let page-header = context {
  let empty-pages = find-labels(<empty-page>)
  let new-chapters = find-labels(<new-chapter>)
  if new-chapters.len() > 0 {
    if new-chapters.contains(here().page()) [
      _이 페이지에서 새로운 장이 시작됩니다_
      #return
    ]

    // 다음 <new-chapter> 레이블의 인덱스를 가져옵니다
    let new-chapter-index = new-chapters.position(page => page > here().page())
    if new-chapter-index != none {
      let empty-page = empty-pages.at(new-chapter-index)
      if empty-page < here().page() [
        _다음 장을 홀수 페이지에서 시작하기 위한 빈 페이지입니다_
        #return
      ]
    }
  }

  [그리고 이것은 일반적인 헤더입니다]
  line(length: 100%)
}

#let page-footer = context {
  // chapter-heading()의 페이지 나누기가 <empty-page> 레이블 뒤에 삽입되므로,
  // 선택자는 관련 레이블을 찾기 위해 현재 페이지 "이전"을 살펴봐야 합니다.
  let empty-page-labels = query(selector(<empty-page>).before(here()))
  if empty-page-labels.len() > 0 {
    let empty-page = empty-page-labels.last().location().page()
    // 가장 최근의 <new-chapter> 레이블을 되돌아봅니다.
    let new-chapter = query(selector(<new-chapter>).before(here())).last().location().page()
    // 현재 페이지에 <new-chapter> 레이블이 없고, (empty-page + 1 == 현재 페이지)인지 확인합니다.
    if (new-chapter != here().page()) and (empty-page + 1 == here().page()) [
      _페이지 번호를 생략해야 하는 빈 페이지입니다_
      #return
    ]
  }

  let page-display = counter(page).display(here().page-numbering())
  h(1fr) + page-display + h(1fr)
}

#show heading.where(level: 1): it => [
  #[] <empty-page>
  #pagebreak(to: "even", weak: true)
  #[] <new-chapter>
  #pagebreak(to: "odd", weak: true)
  #it.body
  #v(2em)
]


#show outline.entry.where(level: 1): it => {
  // 대상 페이지에 대한 마지막 <empty-page> 레이블을 찾기 위해 레이블 쿼리 결과를 뒤집습니다.
  // array.position() 메서드는 항상 첫 번째 항목을 반환하기 때문입니다.
  let empty-pages = find-labels(<empty-page>).rev()
  let new-chapters = query(<new-chapter>).rev()
  let empty-page-index = empty-pages.position(page => page == int(it.page.text))
  let new-chapter = new-chapters.at(empty-page-index)
  link(new-chapter.location())[#it.body #box(width: 1fr)[#it.fill] #new-chapter.location().page()]
}

#set page(header: page-header, footer: page-footer, numbering: "1")

#outline()

= 설명

```
이 쿼리들은 해당 태그가 어디에 있는지 밝혀줍니다. 실제 빈 페이지는 항상 레이블 <empty-page>의 위치 + 1에 있습니다. 실제로 페이지 나누기에 의해 빈 페이지가 삽입되면, 두 레이블은 제목 페이지와 그 이전 페이지를 덮게 됩니다. 빈 페이지가 삽입되지 않은 경우, 두 레이블은 동일한 페이지를 가리키게 되며 이 역시 문제가 되지 않습니다. 심지어 그때도 <new-chapter> 레이블을 먼저 확인하여 더 높은 우선순위를 줄 수 있습니다.

첫 번째 <empty-page> 레이블은 항상 1페이지에 있으며 첫 번째 장 이전의 (존재하지 않는) 빈 페이지를 가리키므로 무시해도 됩니다.

레이블 <empty-page>가 있는 페이지들: #context find-labels(<empty-page>)
레이블 <new-chapter>가 있는 페이지들: #context find-labels(<new-chapter>)
```

= 제목
#lorem(190)

= 또 다른 제목
#lorem(100)

= 마지막 제목
#lorem(400)
`````
