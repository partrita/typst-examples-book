# 페이지 번호 매기기

## 각 장(Chapter)별 별도의 페이지 번호 매기기

```typ
/// 저자: tinger

// 필요한 경우 번호 없는 타이틀 페이지
// ...

// 전면부 (Front-matter)
#set page(numbering: "I")
#counter(page).update(1)
#lorem(50)
// ...

// 페이지 카운터 앵커
#metadata(()) <front-matter>

// 본문 (Main document body)
#set page(numbering: "1")
#lorem(50)
#counter(page).update(1)
// ...

// 후면부 (Back-matter)
#set page(numbering: "I")
// 페이지 나누기를 고려해야 하며, +1 또는 -1만큼 오프셋이 필요할 수 있습니다.
#context counter(page).update(counter(page).at(<front-matter>).first())
#lorem(50)
// ...
```
