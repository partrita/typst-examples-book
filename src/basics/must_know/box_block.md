# 박스와 블록 (Boxing & Blocking)
```typ
박스(box)를 사용하여 무엇이든
텍스트 안으로 감쌀 수 있습니다: #box(image("../tiger.jpg", height: 2em)).

블록(block)은 항상 "별도의 단락"이 됩니다.
텍스트 안에 들어가지 않습니다: #block(image("../tiger.jpg", height: 2em))
```

둘 다 비슷하고 유용한 속성을 가지고 있습니다:
```typ
#box(stroke: red, inset: 1em)[박스 텍스트]
#block(stroke: red, inset: 1em)[블록 텍스트]
```

## `rect`
`block`처럼 작동하지만 유용한 기본 여백(inset)과 테두리(stroke)를 가진 `rect`도 있습니다:
```typ
#rect[블록 텍스트]
```

## 그림 (Figures)

문서에 _그림(figure)_을 추가하려는 경우 `figure` 함수를 사용하세요. 거기서 박스나 블록을 사용하려고 하지 마세요.

그림은 중앙에 배치된 이미지(아마도 캡션 포함), 표, 심지어 코드와 같은 것들입니다.


```typ
@tiger 는 호랑이를 보여줍니다. 호랑이는
동물입니다.

#figure(
  image("../tiger.jpg", width: 80%),
  caption: [호랑이.],
) <tiger>
```

사실, 원하는 무엇이든 그 안에 넣을 수 있습니다:

```typ
당신에게 편지를 쓰라고 하더군요. 여기 있습니다:

#figure(
  text(size: 5em)[나],
  caption: [나 멋지지 않나요?],
) 
```
