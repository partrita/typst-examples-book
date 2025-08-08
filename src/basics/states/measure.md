# 측정, 레이아웃
<div class="warning">이 섹션은 오래되었습니다. 여전히 유용할 수 있지만, 새로운 컨텍스트 시스템(참조 사용)을 공부하는 것이 좋습니다.</div>

## 스타일 및 측정

> 스타일 [문서](https://typst.app/docs/reference/foundations/style/).

> 측정 [문서](https://typst.app/docs/reference/layout/measure/).

`measure`는 _요소 크기_를 반환합니다. 이 명령은 `place`로 사용자 정의 레이아웃을 수행할 때 매우 유용합니다.

그러나 함정이 있습니다. 요소 크기는 이 요소에 적용된 스타일에 따라 다릅니다.

```typ
#let content = [안녕하세요!]
#content
#set text(14pt)
#content
```

따라서 텍스트의 일부에 큰 텍스트 크기를 설정하면 요소의 크기를 측정하기 위해,
_요소가 어디에 있는지 알아야 합니다_. 그것을 알지 못하면 어떤 스타일을 적용해야 하는지 알 수 없습니다.

네, 맞습니다. `context`가 필요합니다.

```typ
#let thing(body) = context {
  let size = measure(body)
  [너비 "#body"는 #size.width입니다]
}

#thing[Hey] \
#thing[Welcome]
```

# 레이아웃

레이아웃은 `measure`와 유사하지만 현재 범위의 **부모 크기**를 반환합니다.

블록에 요소를 넣으면 블록 크기가 됩니다. 페이지에 바로 넣으면 페이지 크기가 됩니다.

그러나 몇 가지 기술적인 이유로 `context`를 사용할 수 없으며 매우 유사한 체계를 사용해야 합니다(사실 `context`가 나온 체계입니다).

```typ
/// 부모 크기를 받아 무언가를 렌더링하는 블랙박스입니다:
#layout(size => {
  let half = 50% * size.width
  [페이지의 절반은 #half 너비입니다.]
})
```

`layout`과 `measure`를 결합하여 부모 크기에 따라 달라지는 것들의 너비를 얻는 것이 매우 유용할 수 있습니다:

```typ
#let text = lorem(30)
#layout(size => context [
  #let (height,) = measure(
    block(width: size.width, text)
  )
  이 텍스트는 현재 페이지 너비에서 #height 높이입니다: \
  #text
])
```
