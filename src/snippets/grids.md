# 그리드(Grids)

## 비율 그리드

길이가 변하는 선이 있는 표의 경우, _그리드 안의 그리드_를 사용해 볼 수 있습니다.

<div class="warning">
<a href="https://typst.app/docs/reference/model/table/#definitions-cell-colspan">cell.colspan 및 rowspan</a>이 가능한 곳에는 사용하지 마세요.
</div>

```typ
// author: jimpjorps

#grid(
  columns: (1fr,),
  grid(
    columns: (1fr,)*2, inset: 5pt, stroke: 1pt, [안녕], [세상]
  ),
  grid(
    columns: (1fr,)*3, inset: 5pt, stroke: 1pt, [foo], [bar], [baz]
  ),
  grid.cell(inset: 5pt, stroke: 1pt)[abcxyz]
)
```

## 같은 값을 가진 인접 셀 자동 병합

이 예제는 가로로 인접한 셀에 대해 작동하지만, 세로(열)로 확장하는 것도 어렵지 않습니다.

```typ
// author: tebine
#let merge(children, n-cols) = {
  let rows = children.chunks(n-cols)
  let new-children = ()
  for r in rows {
    // 첫 번째 그룹은 인덱스 0에서 시작
    let i = 0 
    // 다음 그룹 검색
    while i < r.len() {
      // 그룹은 하나의 셀로 시작
      let c = r.at(i).body
      let n = 1
      for j in range(i+1, r.len()) {
        let c-next = r.at(j).body
        if c-next == c {
          // 그룹에 셀 추가
          n += 1
        } else {
          break
        }
      }
      // 그룹 종료
      new-children.push(table.cell(colspan: n, c))
      i += n
    }
  }
  return new-children
}
#show table: it => {
  let merged = merge(it.children, it.columns.len())
  if it.children.len() == merged.len() { // 재귀를 피하기 위한 트릭
    return it
  }
  table(columns: it.columns.len(), ..merged)
}
#table(columns: 2,
  [1], [2],
  [3], [3],
  [4], [5],
)
```

## 기울어진 테두리가 있는 기울어진 열 헤더

```typ
// author: tebine
#let slanted(it, alpha: 45deg, len: 2.5cm) = layout(size => {
  let width = size.width
  let b = box(inset: 5pt, rotate(-alpha, reflow: true, it))
  let b-size = measure(b)
  let l = line(angle: -alpha, length: len)
  let l-width = len * calc.cos(alpha)
  let l-height = len * calc.sin(alpha)
  place(bottom+left, l)
  place(bottom+left, l, dx: width)
  place(bottom+left, line(length: width), dx: l-width, dy: -l-height)
  place(bottom+left, dx: width/2, b)
  box(height: l-height) // 높이를 설정하기 위한 보이지 않는 상자
})

#table(
  columns: 2,
  align: center,
  table.header(
    table.cell(stroke: none, inset: 0pt, slanted[*AAA*]),
    table.cell(stroke: none, inset: 0pt, slanted[*BBBBBB*]),
  ),
  [aaaaa], [bbbbbb], [c], [d],
)
```
