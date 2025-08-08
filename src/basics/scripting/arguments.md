# 고급 인수
## 목록에서 인수 펼치기

펼치기 연산자를 사용하면 값 목록을 함수 인수로 "풀" 수 있습니다:

```typ
#let func(a, b, c, d, e) = [#a #b #c #d #e]
#func(..(([hi],) * 5))
```

이것은 표에서 매우 유용할 수 있습니다:

```typ
#let a = ("hi", "b", "c")

#table(columns: 3,
  [test], [x], [hello],
  ..a
)
```

## 키 인수

키 인수에서도 동일한 아이디어가 작동합니다:

```typ
#let text-params = (fill: blue, size: 0.8em)

일부 #text(..text-params)[텍스트].
```

# 임의의 인수 관리하기

Typst를 사용하면 원하는 만큼 임의의 위치 및 키 인수를 사용할 수 있습니다.

이 경우 함수에는 위치 및 명명된 인수를 저장하는 특수 `arguments` 객체가 제공됩니다.

> [참조](https://typst.app/docs/reference/foundations/arguments/) 링크

```typ
#let f(..args) = [
  #args.pos()\
  #args.named()
]

#f(1, "a", width: 50%, block: false)
```

다른 인수와 결합할 수 있습니다. 펼치기 연산자는 나머지 모든 인수를 "먹습니다":

```typ
#let format(title, ..authors) = {
  let by = authors
    .pos()
    .join(", ", last: " and ")

  [*#title* \ _#by 가 씀;_]
}

#format("ArtosFlow", "Jane", "Joe")
```

## 선택적 인수

_현재 Typst에서 선택적 위치 인수를 만드는 유일한 방법은 `arguments` 객체를 사용하는 것입니다:_

TODO
