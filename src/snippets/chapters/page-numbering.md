# 페이지 번호 매기기

## 각 챕터에 대한 별도의 페이지 번호 매기기

```typ
/// 저자: tinger

// 필요한 경우 번호 없는 제목 페이지
// ...

// 앞부분
#set page(numbering: "I")
#counter(page).update(1)
#lorem(50)
// ...

// 페이지 카운터 앵커
#metadata(()) <front-matter>

// 주 문서 본문
#set page(numbering: "1")
#lorem(50)
#counter(page).update(1)
// ...

// 뒷부분
#set page(numbering: "I")
// 페이지 나누기를 고려해야 하며, +1 또는 -1로 오프셋해야 할 수 있습니다.
#context counter(page).update(counter(page).at(<front-matter>).first())
#lorem(50)
// ...
```