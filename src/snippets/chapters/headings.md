# 제목 (Headings)

제목의 번호 매기기 스타일과 외관을 커스터마이징하는 방법입니다.

## 제목 스타일 변경
`show` 규칙을 사용하여 제목의 폰트, 색상, 크기 등을 일괄적으로 변경할 수 있습니다.

```typ
#show heading.where(level: 1): set text(blue, size: 1.5em)
#show heading.where(level: 2): set text(gray)

= 1단계 제목 (파란색)
== 2단계 제목 (회색)
```

## 제목 뒤에 선 긋기
장(Chapter) 제목 아래에 선을 추가하는 흔한 스타일입니다.

```typ
#show heading.where(level: 1): it => [
  #it
  #v(0.3em)
  #line(length: 100%, stroke: 0.5pt)
  #v(1em)
]

= 첫 번째 장
```

## 번호 매기기 커스텀
번호 뒤에 특정 기호를 붙이거나 형식을 바꿀 수 있습니다.

```typ
#set heading(numbering: "1.1)")

= 도입
== 배경
```

특정 수준부터 번호를 매기지 않으려면 `numbering: none`을 사용합니다.
