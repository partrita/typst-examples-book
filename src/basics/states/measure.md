# 측정 및 레이아웃 (Measure, Layout)
<div class="warning">이 섹션은 오래되었습니다. 여전히 유용할 수 있지만, 참조 문서를 통해 새로운 컨텍스트 시스템을 공부하는 것을 강력히 추천합니다.</div>

## 스타일과 측정 (Style & Measure)

> 스타일 [공식 문서](https://typst.app/docs/reference/foundations/style/)

> 측정 [공식 문서](https://typst.app/docs/reference/layout/measure/)

`measure`는 _요소의 크기_ 를 반환합니다. 이 명령은 `place`를 사용하여 사용자 정의 레이아웃을 만들 때 매우 유용합니다.

하지만 한 가지 주의할 점이 있습니다. 요소의 크기는 해당 요소에 적용된 스타일에 따라 달라집니다.

```typ
#let content = [안녕!]
#content
#set text(14pt)
#content
```

따라서 텍스트의 일부에 큰 글꼴 크기를 설정한 경우, 요소의 크기를 측정하려면 _요소가 어디에 위치하는지_ 알아야 합니다. 이를 모르면 어떤 스타일을 적용해야 할지 알 수 없습니다.

네, 맞습니다. 우리에게는 `context`가 필요합니다.

```typ
#let thing(body) = context {
  let size = measure(body)
  ["#body" 의 너비는 #size.width 입니다.]
}

#thing[이봐요] \
#thing[환영합니다]
```

# 레이아웃 (Layout)

레이아웃은 `measure`와 비슷하지만, 현재 범위의 **부모 크기** 를 반환합니다.

요소를 블록(block)에 넣는다면 블록의 크기가 될 것이고, 페이지에 바로 넣는다면 페이지의 크기가 될 것입니다.

기술적인 이유로 `context`를 직접 사용할 수는 없으며, 매우 유사한 방식을 사용해야 합니다 (사실 `context`가 여기서 파생된 방식입니다):

```typ
/// 부모 크기를 받아서 무언가를 렌더링하는 블랙박스입니다.
#layout(size => {
  let half = 50% * size.width
  [페이지의 절반 너비는 #half 입니다.]
})
```

`layout`과 `measure`를 결합하여 부모 크기에 의존하는 요소의 너비를 구하는 것은 매우 유용할 수 있습니다:

```typ
#let text = lorem(30)
#layout(size => context [
  #let (height,) = measure(
    block(width: size.width, text)
  )
  이 텍스트의 높이는 현재 페이지 너비에서 #height 입니다: \
  #text
])
```
