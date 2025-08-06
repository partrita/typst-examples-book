# 간격 사용하기
대부분의 경우 함수에 간격을 전달하게 됩니다. _크기_만 받는 특별한 함수 필드가 있습니다.
이들은 보통 `width, length, in(out)set, spacing` 등과 같이 불립니다.

CSS에서와 같이, Typst에서 간격을 설정하는 방법 중 하나는 요소의 여백과 안쪽 여백을 설정하는 것입니다.
하지만, `h`(수평 간격)와 `v`(수직 간격) 함수를 사용하여 직접 간격을 삽입할 수도 있습니다.

> 참조 링크: [h](https://typst.app/docs/reference/layout/h/), [v](https://typst.app/docs/reference/layout/v/).

```typ
수평 #h(1cm) 간격.
#v(1cm)
그리고 약간의 수직 간격도!
```

# 절대 길이 단위
> [참조](https://typst.app/docs/reference/layout/length/) 링크

절대 길이(일명 "길이") 단위는 외부 내용과 부모의 크기에 영향을 받지 않습니다.
```typ
#set rect(height: 1em)
#table(
  columns: 2,
  [포인트], rect(width: 72pt),
  [밀리미터], rect(width: 25.4mm),
  [센티미터], rect(width: 2.54cm),
  [인치], rect(width: 1in),
)
```

## 현재 글꼴 크기에 상대적
`1em = 현재 글꼴 크기 1`:

```typ
#set rect(height: 1em)
#table(
  columns: 2,
  [센티미터], rect(width: 2.54cm),
  [글꼴 크기에 상대적], rect(width: 6.5em)
)

두 배 글꼴 크기: #box(stroke: red, baseline: 40%, height: 2em, width: 2em)
```

이것은 매우 편리한 단위이므로 Typst에서 많이 사용됩니다.

## 결합됨

```typ
결합됨: #box(rect(height: 5pt + 1em))

#(5pt + 1em).abs
#(5pt + 1em).em
```


# 비율 길이
> [참조](https://typst.app/docs/reference/layout/ratio/) 링크

`1% = 해당 차원에서 부모 크기의 1%`

```typ
이 줄 너비는 사용 가능한 페이지 크기(여백 제외)의 50%입니다:

#line(length: 50%)

이 줄 너비는 상자 너비의 50%입니다: #box(stroke: red, width: 4em, inset: (y: 0.5em), line(length: 50%))
```

# 상대 길이
> [참조](https://typst.app/docs/reference/layout/relative/) 링크

절대 길이와 비율 길이를 _결합_하여 _상대 길이_로 만들 수 있습니다:

```typ
#rect(width: 100% - 50pt)

#(100% - 50pt).length \
#(100% - 50pt).ratio
```

# 분수 길이
> [참조](https://typst.app/docs/reference/layout/fraction/) 링크

단일 분수 길이는 부모를 채우기 위해 _가능한 최대 크기_를 차지합니다:

```typ
왼쪽 #h(1fr) 오른쪽

#rect(height: 1em)[
  #h(1fr)
]
```

분수를 사용할 수 있는 곳은 많지 않으며, 주로 `h`와 `v`입니다.

## 여러 분수
한 부모 안에 여러 분수를 사용하면,
_숫자에 비례하여_ 남은 공간을 모두 차지합니다:

```typ
왼쪽 #h(1fr) 왼쪽 편 #h(2fr) 오른쪽
```

## 중첩된 레이아웃

분수는 부모에서만 작동하므로, _중첩된 레이아웃에서는 의존하지 마세요_:

```typ
단어: #h(1fr) #box(height: 1em, stroke: red)[
  #h(2fr)
]
```
