# 개요

# 개요

> [공식 참조](https://typst.app/docs/reference/model/outline/)에서 많은 개요 예제를 이미 사용할 수 있습니다.

## 목차

```typ
#outline()

= 서론
#lorem(5)

= 이전 연구
#lorem(10)
```

## 그림 개요

```typ
#outline(
  title: [그림 목록],
  target: figure.where(kind: table),
)

#figure(
  table(
    columns: 4,
    [t], [1], [2], [3],
    [y], [0.3], [0.7], [0.5],
  ),
  caption: [실험 결과],
)
```

거기서 임의의 선택자를 사용할 수 있으므로, 어떤 미친 짓이든 할 수 있습니다.

<!--TODO: 레이블과 선택자 조합의 미친 예제-->

## 낮은 수준의 제목 무시

```typ
#set heading(numbering: "1.")
#outline(depth: 2)

= 예
최상위 섹션.

== 여전히
하위 섹션.

=== 아니요
포함되지 않음.
```

## 들여쓰기 설정

```typ
#set heading(numbering: "1.a.")

#outline(
  title: [목차 (자동)],
  indent: auto,
)

#outline(
  title: [목차 (길이)],
  indent: 2em,
)

#set outline.entry(fill: "→")
#outline(
  title: [목차 (함수)],
)

= ACME Corp. 소개
== 역사
=== 기원
#lorem(10)

== 제품
#lorem(10)
```

## 기본 점 바꾸기

```typ
#set outline.entry(fill: line(length: 100%))
#outline(indent: 2em)

= 첫 번째 수준
== 두 번째 수준
```

## 다른 개요 수준을 다르게 보이게 만들기

```typ
#set heading(numbering: "1.")

#show outline.entry.where(
  level: 1
): it => {
  v(12pt, weak: true)
  strong(it)
}

#outline(indent: auto)

= 서론
= 배경
== 역사
== 최신 기술
= 분석
== 설정
```

## 개요를 위한 길고 짧은 캡션

```typ
// 저자: laurmaedje
// 템플릿이나 문서 시작 부분에 이것을 넣으세요.
#let in-outline = state("in-outline", false)
#show outline: it => {
  in-outline.update(true)
  it
  in-outline.update(false)
}

#let flex-caption(long, short) = context if in-outline.get() { short } else { long }

// 그리고 이것은 문서에 있습니다.
#outline(title: [그림], target: figure)

#figure(
  rect(),
  caption: flex-caption(
    [이것은 문서의 긴 캡션 텍스트입니다.],
    [이것은 짧습니다],
  )
)
```

## 인용 및 각주 무시

각주를 제목으로 만들면 개요에 번호가 표시되는 문제를 해결하는 방법입니다:

```typ

= 제목 #footnote[각주]

텍스트

#outline() // 나쁨 :(

#pagebreak()
#{
  set footnote.entry(
    separator: none
  )
  show footnote.entry: hide
  show ref: none
  show footnote: none

  outline()
}
```