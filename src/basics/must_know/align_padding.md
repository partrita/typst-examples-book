# 정렬 및 패딩 (Align & Padding)

텍스트나 요소의 배치와 내부 여백을 조절하는 기본 도구들입니다.

## 정렬 (Align)
`align` 함수를 사용하여 요소를 부모 컨테이너 내에서 정렬합니다.

```typ
#align(center)[이 텍스트는 중앙에 배치됩니다.]

#align(right + bottom)[
  오른쪽 아래에 배치되는 내용입니다.
]
```

- **가로 정렬**: `left`, `center`, `right`
- **세로 정렬**: `top`, `horizon`, `bottom`
- **조합**: `right + top`과 같이 조합하여 사용 가능합니다.

## 패딩 (Padding)
`pad` 함수는 요소의 주변에 공백을 추가합니다.

```typ
#set rect(stroke: 1pt)
#rect[패딩이 없는 상자]
#pad(left: 2em)[#rect[왼쪽에 2em 패딩이 추가된 상자]]

#pad(x: 1em, y: 0.5em)[가로 1em, 세로 0.5em 패딩]
```

## 박스의 내부 여백 (Inset)
`box`나 `block`, `rect` 등은 내부 여백인 `inset` 속성을 가집니다. `pad`는 요소 *바깥*에 공백을 주고, `inset`은 요소 *안쪽*에 공백을 줍니다.

```typ
#rect(inset: 10pt)[내부 여백이 10pt인 상자]
```
