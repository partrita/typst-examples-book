# 기초
## 변수 I
_변수_부터 시작해 봅시다.

개념은 매우 간단합니다, 재사용할 수 있는 어떤 값입니다:
```typ
#let author = "John Doe"

이것은 #author 가 쓴 책입니다. #author 는 멋진 사람입니다.

#quote(block: true, attribution: author)[
  <어떤 인용문>
]
```

## 변수 II
변수에는 _모든_ Typst 값을 저장할 수 있습니다:

```typ
#let block_text = block(stroke: red, inset: 1em)[텍스트]

#block_text

#figure(caption: "블록", block_text)
```

## 함수
[고급 스타일링](../tutorial/advanced_styling.md) 챕터에서 이미 일부 "사용자 정의" 함수를 보았습니다.

함수는 어떤 값을 받아서
어떤 값을 출력하는 값입니다:

```typ
// 이것은 이전에 본 구문입니다
#let f = (name) => "안녕하세요, " + name

#f("세상!")
```

### 대체 구문
동일한 내용을 더 짧게 작성할 수 있습니다:

```typ
// 다음 구문은 동일합니다
#let f = (name) => "안녕하세요, " + name
#let f(name) = "안녕하세요, " + name

#f("세상!")
```
