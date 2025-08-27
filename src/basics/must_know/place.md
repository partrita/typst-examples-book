# 배치, 이동, 크기 조절 및 숨기기

이 섹션은 레이아웃으로 임의의 작업을 수행하고,
사용자 정의 요소를 만들고 현재 Typst의 한계를 해결하려는 경우 **매우 중요한 섹션**입니다.

TODO: 작업 중, 텍스트 및 더 나은 예제 추가

# Place

_레이아웃을 무시_하고, 부모 및 현재 위치에 상대적으로 객체를 배치합니다.
배치된 객체는 레이아웃에 영향을 미치지 _않습니다_.

> [참조](https://typst.app/docs/reference/layout/place/) 링크

```typ
#set page(height: 60pt)
안녕하세요, 세상!

#place(
  top + right, // 페이지 오른쪽 상단에 배치
  square(
    width: 20pt,
    stroke: 2pt + blue
  ),
)
```

### place를 사용한 기본 플로팅

```typ
#set page(height: 150pt)
#let note(where, body) = place(
  center + where,
  float: true,
  clearance: 6pt,
  rect(body),
)

#lorem(10)
#note(bottom)[하단 1]
#note(bottom)[하단 2]
#lorem(40)
#note(top)[상단]
#lorem(10)
```

### dx, dy
의도한 위치에 상대적으로 `(dx, dy)`로 위치를 수동으로 변경합니다.

```typ
#set page(height: 100pt)
#for i in range(16) {
  let amount = i * 4pt
  place(center, dx: amount - 32pt, dy: amount)[A]
}
```

# Move
> [참조](https://typst.app/docs/reference/layout/move/) 링크

```typ
#rect(inset: 0pt, move(
  dx: 6pt, dy: 6pt,
  rect(
    inset: 8pt,
    fill: white,
    stroke: black,
    [아브라카다브라]
  )
))
```

# Scale

레이아웃에 영향을 주지 않고 콘텐츠 크기를 조절합니다.

> [참조](https://typst.app/docs/reference/layout/scale/) 링크

```typ
#scale(x: -100%)[이것은 미러링되었습니다.]
```

```typ
A#box(scale(75%)[A])A \
B#box(scale(75%, origin: bottom + left)[B])B
```

# Hide

콘텐츠를 표시하지 않고 빈 공간을 남겨 둡니다.

> [참조](https://typst.app/docs/reference/layout/hide/) 링크

```typ
안녕하세요 Jane \
#hide[안녕하세요] Joe
```
