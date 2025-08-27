# 박싱 및 블로킹
```typ
상자를 사용하여 무엇이든
텍스트로 감쌀 수 있습니다: #box(image("../tiger.jpg", height: 2em)).

블록은 항상 "별도의 단락"이 됩니다.
텍스트에 맞지 않습니다: #block(image("../tiger.jpg", height: 2em))
```

둘 다 비슷한 유용한 속성을 가지고 있습니다:
```typ
#box(stroke: red, inset: 1em)[상자 텍스트]
#block(stroke: red, inset: 1em)[블록 텍스트]
```

## `rect`
`block`처럼 작동하지만 유용한 기본 안쪽 여백과 획이 있는 `rect`도 있습니다:
```typ
#rect[블록 텍스트]
```

## 그림

문서에 _그림_을 추가하려면 `figure` 함수를 사용하세요. 상자나 블록을 사용하려고 하지 마세요.

그림은 가운데 정렬된 이미지(캡션이 있을 수 있음), 표, 심지어 코드와 같은 것입니다.


```typ
@tiger는 호랑이를 보여줍니다. 호랑이는
동물입니다.

#figure(
  image("../tiger.jpg", width: 80%),
  caption: [호랑이.],
) <tiger>
```

사실, 원하는 것은 무엇이든 넣을 수 있습니다:

```typ
그들은 저에게 당신에게 편지를 쓰라고 했습니다. 여기 있습니다:

#figure(
  text(size: 5em)[나],
  caption: [나 멋지지, 그렇지?],
)
```
