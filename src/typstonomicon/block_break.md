# 깨진 블록의 중단점

### 테이블 헤더 및 푸터로 구현

데모 프로젝트 보기(더 많은 주석, 일부는 제거함) [여기](https://typst.app/project/r-yQHF952iFnPme9BWbRu3).

```typ
/// 저자: wrzian

// 기본 카운터 및 지그재그 함수
#let counter-family(id) = {
  let parent = counter(id)
  let parent-step() = parent.step()
  let get-child() = counter(id + str(parent.get().at(0)))
  return (parent-step, get-child)
}

// 재미있는 지그재그 라인!
#let zig-zag(fill: black, rough-width: 6pt, height: 4pt, thick: 1pt, angle: 0deg) = {
  layout((size) => {
    // 레이아웃을 사용하여 크기를 가져오고 수평 거리를 측정합니다.
    // 그런 다음 수학을 사용하여 지그재그당 너비를 구합니다.
    let count = int(calc.round(size.width / rough-width))
    // `h(-thick)`로 조인하므로 추가 두께를 추가해야 합니다.
    let width = thick + (size.width - thick) / count
    // 하나의 지그와 하나의 재그:
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

// split-box 테두리에 대한 사용자 정의 가능한 옵션:
#let default-border = (
  // 시작 및 끝 줄
  above: line(length: 100%),
  below: line(length: 100%),
  // 여러 페이지에 걸쳐 상자 사이에 넣을 줄
  btwn-above: line(length: 100%, stroke: (dash:"dotted")),
  btwn-below: line(length: 100%, stroke: (dash:"dotted")),
  // 왼쪽/오른쪽 줄
  // 이것들은 `grid.vline()`을 *반드시* 사용해야 합니다. 그렇지 않으면 오류가 발생합니다.
  // 줄을 제거하려면 `grid.vline(stroke: none)`으로 설정하세요.
  // 아마도 rowspan으로 더 잘 구성할 수 있겠지만, 저는 게으릅니다.
  left: grid.vline(),
  right: grid.vline(),
)

// 여러 페이지/열에 걸쳐 있고 열 나누기 위아래에 사용자 정의 테두리가 있는 콘텐츠 상자를 만듭니다.
#let split-box(
  // 테두리 사전을 설정합니다. 옵션은 위의 `default-border`를 참조하세요.
  border: default-border,
  // 콘텐츠를 배치할 셀, 이것은 `grid.cell`로 확인되어야 합니다.
  cell: grid.cell.with(inset: 5pt),
  // 마지막 위치 인수 또는 인수는 실제 콘텐츠입니다.
  // 추가 명명된 인수는 호출될 때 기본 그리드로 전송됩니다.
  // 이것은 채우기, 정렬 등에 유용합니다.
  ..args
) = {
  // 자세한 내용은 `utils.typ`를 참조하세요.
  let (parent-step, get-child) = counter-family("split-box-unique-counter-string")
  parent-step() // 부모 카운터를 한 번 배치합니다.
  // 헤더가 페이지에 배치될 때마다 추적합니다.
  // 그런 다음 첫 번째 배치(헤더용)인지 마지막(푸터용)인지 확인합니다.
  // 그렇지 않은 경우 테두리 선의 '사이' 형식을 사용합니다.
  let border-above = context {
    let header-count = get-child()
    header-count.step()
    context if header-count.get() == (1,) { border.above } else { border.btwn-above }
  }
  let border-below = context {
    let header-count = get-child()
    if header-count.get() == header-count.final() { border.below } else { border.btwn-below }
  }
  // 그리드를 배치합니다!
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

// 그리고 여기 재미있는 예제가 있습니다:

#let fun-border = (
  // 그라데이션!
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

// 그리고 좀 더 온순한 친구들:

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

### 헤더, 푸터 및 상태를 통한 구현

<div class="warning">
  제한 사항: <strong>단일 열 레이아웃 및 단일 나누기에서만 작동합니다</strong>.
</div>

```typ
#let countBoundaries(loc, fromHeader) = {
  let startSelector = selector(label("boundary-start"))
  let endSelector = selector(label("boundary-end"))

  if fromHeader {
    // 페이지 상단에서 아래로 계산
    startSelector = startSelector.after(loc)
    endSelector = endSelector.after(loc)
  } else {
    // 페이지 하단에서 위로 계산
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
      // 이 헤더를 여는 장식으로 장식합니다.
      [블록 나누기 상단: $-->$]
    }
  },
  footer: context {
    let boundaryCount = countBoundaries(here(), false)

    if boundaryCount.start > boundaryCount.end {
      // 이 푸터를 닫는 장식으로 장식합니다.
      [블록 나누기 끝: $<--$]
    }
  }
)

#let breakable-block(body) = block({
  [
    #metadata("boundary") <boundary-start>
  ]
  stack(
    // 나눌 수 있는 목록 콘텐츠는 여기에 들어갑니다.
    body
  )
  [
    #metadata("boundary") <boundary-end>
  ]
})

#set page(height: 10em)

#breakable-block[
    #([무언가 \ ]*10)
]
```