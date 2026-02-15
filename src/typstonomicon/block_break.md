# 끊어진 블록의 중단점 (Breakpoints on broken blocks)

### 테이블 헤더 및 푸터를 사용한 구현

[여기](https://typst.app/project/r-yQHF952iFnPme9BWbRu3)에서 데모 프로젝트를 확인하세요(더 많은 주석이 있으며, 일부는 제거했습니다).

```typ
/// author: isuffix

// 기본 카운터 및 지그재그 함수
#let counter-family(id) = {
  let parent = counter(id)
  let parent-step() = parent.step()
  let get-child() = counter(id + str(parent.get().at(0)))
  return (parent-step, get-child)
}

// 재미있는 지그재그 선!
#let zig-zag(fill: black, rough-width: 6pt, height: 4pt, thick: 1pt, angle: 0deg) = {
  layout((size) => {
    // layout을 사용하여 크기를 얻고 수평 거리를 측정
    // 그 다음 수학을 사용하여 지그재그 당 너비 구함
    let count = int(calc.round(size.width / rough-width))
    // `h(-thick)`으로 결합하므로 추가 두께를 더해야 함
    let width = thick + (size.width - thick) / count
    // 지그(Zig)와 재그(Zag):
    let zig-and-zag = {
      let line-stroke = stroke(thickness: thick, cap: "round", paint: fill)
      let top-left = (thick/2, thick/2)
      let bottom-mid = (width/2, height - thick/2)
      let top-right = (width - thick/2, thick/2)
      let zig = line(stroke: line-stroke, start: top-left, end: bottom-mid)
      let zag = line(stroke: line-stroke, start: bottom-mid, end: top-right)
      box(place(zig) + place(zag), width: width, height: height, clip: true)
    }
    let zig-zags = ((zig-and-zag,) * count).join(h(-thick))
    rotate(zig-zags, angle)
  })
}

// ---- split-box 정의 ---- //

// 사용자 정의 가능한 split-box 테두리 옵션:
#let default-border = (
  // 시작 및 끝 선
  above: line(length: 100%),
  below: line(length: 100%),
  // 여러 페이지에 걸쳐 상자 사이에 넣을 선
  btwn-above: line(length: 100%, stroke: (dash:"dotted")),
  btwn-below: line(length: 100%, stroke: (dash:"dotted")),
  // 왼쪽/오른쪽 선
  // 이들은 *반드시* `grid.vline()`을 사용해야 하며, 그렇지 않으면 오류가 발생합니다.
  // 선을 제거하려면 `grid.vline(stroke: none)`으로 설정하세요.
  // rowspan으로 더 잘 구성할 수도 있겠지만, 귀찮네요.
  left: grid.vline(),
  right: grid.vline(),
)

// 여러 페이지/열에 걸치고
// 열 중단 위아래에 사용자 정의 테두리가 있는 상자 생성
#let split-box(
  // 테두리 딕셔너리 설정, 옵션은 위의 `default-border` 참조
  border: default-border,
  // 콘텐츠를 배치할 셀, `grid.cell`로 해석되어야 함
  cell: grid.cell.with(inset: 5pt),
  // 마지막 위치 인수(들)은 실제 콘텐츠입니다.
  // 추가 명명된 인수는 호출 시 기본 그리드로 전송됩니다.
  // fill, align 등에 유용합니다.
  ..args
) = {
  // 더 많은 정보는 `utils.typ` 참조.
  let (parent-step, get-child) = counter-family("split-box-unique-counter-string")
  parent-step() // 부모 카운터를 한 번 배치.
  // 헤더가 페이지에 배치될 때마다 추적.
  // 그런 다음 첫 번째 배치(헤더)인지 마지막(푸터)인지 확인.
  // 그렇지 않다면 테두리 선의 'between' 형태를 사용.
  let border-above = context {
    let header-count = get-child()
    header-count.step()
    context if header-count.get() == (1,) { border.above } else { border.btwn-above }
  }
  let border-below = context {
    let header-count = get-child()
    if header-count.get() == header-count.final() { border.below } else { border.btwn-below }
  }
  // 그리드 배치!
  grid(
    ..args.named(),
    columns: 3,
    border.left,
    grid.header(border-above , repeat: true),
    ..args.pos().map(cell),
    grid.footer(border-below, repeat: true),
    border.right,
  )
}

// ---- 예제 ---- //

#set page(width: 7.2in, height: 3in, columns: 6)

// 짜잔!
#split-box[
  #lorem(20)
]

// 재미있는 예제:

#let fun-border = (
  // 그라디언트!
  above: line(length: 100%, stroke: 2pt + gradient.linear(..color.map.rainbow)),
  below: line(length: 100%, stroke: 2pt + gradient.linear(..color.map.rainbow, angle: 180deg)),
  // 지그재그!
  btwn-above: move(dy: +2pt, zig-zag(fill: blue, angle: 3deg)),
  btwn-below: move(dy: -2pt, zig-zag(fill: orange, angle: 177deg)),
  left: grid.vline(stroke: (cap: "round", paint: purple)),
  right: grid.vline(stroke: (cap: "round", paint: purple)),
)

#split-box(border: fun-border)[
  #lorem(25)
]

// 그리고 좀 더 얌전한 친구들:

#split-box(border: (
  above: move(dy: -0.5pt, line(length: 100%)),
  below: move(dy: +0.5pt, line(length: 100%)),
  // 지그재그!
  btwn-above: move(dy: -1.1pt, zig-zag()),
  btwn-below: move(dy: +1.1pt, zig-zag(angle: 180deg)),
  left: grid.vline(stroke: (cap: "round")),
  right: grid.vline(stroke: (cap: "round")),
))[
  #lorem(10)
]

#split-box(
  border: (
    above: line(length: 100%, stroke: luma(50%)),
    below: line(length: 100%, stroke: luma(50%)),
    btwn-above: line(length: 100%, stroke: (dash: "dashed", paint: luma(50%))),
    btwn-below: line(length: 100%, stroke: (dash: "dashed", paint: luma(50%))),
    left: grid.vline(stroke: none),
    right: grid.vline(stroke: none),
  ),
  cell: grid.cell.with(inset: 5pt, fill: color.yellow.saturate(-85%))
)[
  #lorem(20)
]

```

### 헤더, 푸터 및 상태(stated)를 통한 구현

<div class="warning">
  제한 사항: <strong>단일 열 레이아웃과 한 번의 중단에서만 작동합니다</strong>.
</div>

```typ
#let countBoundaries(loc, fromHeader) = {
  let startSelector = selector(label("boundary-start"))
  let endSelector = selector(label("boundary-end"))

  if fromHeader {
    // 페이지 상단에서 카운트 다운
    startSelector = startSelector.after(loc)
    endSelector = endSelector.after(loc)
  } else {
    // 페이지 하단에서 카운트 업
    startSelector = startSelector.before(loc)
    endSelector = endSelector.before(loc)
  }

  let startMarkers = query(startSelector)
  let endMarkers = query(endSelector)
  let currentPage = loc.position().page

  let pageStartMarkers = startMarkers.filter(elem =>
    elem.location().position().page == currentPage)

  let pageEndMarkers = endMarkers.filter(elem =>
    elem.location().position().page == currentPage)

  (start: pageStartMarkers.len(), end: pageEndMarkers.len())
}

#set page(
  margin: 2em,
  // ... 다른 페이지 설정 ...
  header: context {
    let boundaryCount = countBoundaries(here(), true)

    if boundaryCount.end > boundaryCount.start {
      // 이 헤더를 여는 장식으로 꾸미기
      [Block break top: $-->$]
    }
  },
  footer: context {
    let boundaryCount = countBoundaries(here(), false)

    if boundaryCount.start > boundaryCount.end {
      // 이 푸터를 닫는 장식으로 꾸미기
      [Block break end: $<--$]
    }
  }
)

#let breakable-block(body) = block({
  [
    #metadata("boundary") <boundary-start>
  ]
  stack(
    // 분리 가능한 목록 콘텐츠가 여기에 들어감
    body
  )
  [
    #metadata("boundary") <boundary-end>
  ]
})

#set page(height: 10em)

#breakable-block[
    #([Something \ ]*10)
]
```
