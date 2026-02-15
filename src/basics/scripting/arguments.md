# 고급 인수 (Advanced arguments)
## 리스트에서 인수 전개하기 (Spreading arguments from list)

전개 연산자(spreading operator)를 사용하면 값의 리스트를 함수의 인수로 "풀어 놓을(unpack)" 수 있습니다:

```typ
#let func(a, b, c, d, e) = [#a #b #c #d #e]
#func(..(([안녕],) * 5))
```

이것은 표(table)에서 매우 유용할 수 있습니다:

```typ
#let a = ("안녕", "b", "c")

#table(columns: 3,
  [테스트], [x], [안녕],
  ..a
)
```

## 키 인수 (Key arguments)

동일한 아이디어가 키 인수에도 적용됩니다:

```typ
#let text-params = (fill: blue, size: 0.8em)

일부 #text(..text-params)[텍스트].
```

# 임의의 인수 관리하기

Typst에서는 원하는 만큼 임의의 위치 인수와 키 인수를 받을 수 있습니다.

이 경우 함수에는 위치 인수와 명명된 인수를 저장하는 특수한 `arguments` 객체가 주어집니다.

> [참조](https://typst.app/docs/reference/foundations/arguments/) 링크

```typ
#let f(..args) = [
  #args.pos()\
  #args.named()
]

#f(1, "a", width: 50%, block: false)
```

이들을 다른 인수와 결합할 수 있습니다. 전개 연산자는 나머지 모든 인수를 "먹어 치울" 것입니다:

```typ
#let format(title, ..authors) = {
  let by = authors
    .pos()
    .join(", ", last: " 및 ")

  [*#title* \ _작성자: #by;_]
}

#format("ArtosFlow", "Jane", "Joe")
```

## 선택적 인수 (Optional argument)

_현재 Typst에서 선택적 위치 인수를 만드는 유일한 방법은 `arguments` 객체를 사용하는 것입니다:_

TODO
