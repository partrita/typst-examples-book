# 기초 (Basics)
## 변수 I
_변수(variables)_부터 시작해 보겠습니다.

변수의 개념은 매우 간단합니다. 재사용할 수 있는 어떤 값일 뿐입니다:
```typ
#let author = "홍길동"

이것은 #author 가 쓴 책입니다. #author 는 정말 멋진 사람입니다.

#quote(block: true, attribution: author)[
  \<어떤 인용문\>
]
```

## 변수 II
변수에는 _어떤_ Typst 값이라도 저장할 수 있습니다:

```typ
#let block_text = block(stroke: red, inset: 1em)[텍스트]

#block_text

#figure(caption: "블록", block_text)
```

## 함수 (Functions)
우리는 이미 [고급 스타일링](../tutorial/advanced_styling.md) 장에서 몇 가지 "사용자 정의" 함수를 보았습니다.

함수는 어떤 값을 받아서 어떤 값을 출력하는 값입니다:

```typ
// 이것은 앞서 보았던 구문입니다.
#let f = (name) => "안녕, " + name

#f("세상아!")
```

### 대안 구문
같은 내용을 더 짧게 쓸 수 있습니다:

```typ
// 다음 구문들은 동일합니다.
#let f = (name) => "안녕, " + name
#let f(name) = "안녕, " + name

#f("세상아!")
```
