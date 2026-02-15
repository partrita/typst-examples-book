# 이미지 원래 크기로 표시
이 함수는 이미지가 가진 "자연스러운" 크기 그대로 렌더링합니다.

**참고: v0.11부터** Typst는 너비와 높이가 `auto`인 경우 기본 이미지 크기를 사용하려고 시도합니다. 이미지가 컨테이너에 맞지 않는 경우에만 컨테이너 크기를 사용합니다. 따라서 이 코드는 이제 다소 유산(legacy)에 가깝지만, 여전히 유용할 수 있습니다.

이 코드가 작동하는 이유는 `measure`가 개념적으로 이미지를 무한한 크기의 페이지에 배치하고, 이미지는 스스로 무한히 커지는 대신 기본값인 픽셀당 1pt를 사용하기 때문입니다.

```typ
// 저자: laurmaedje
#let natural-image(..args) = style(styles => {
  let (width, height) = measure(image(..args), styles)
  image(..args, width: width, height: height)
})

#image("../tiger.jpg")
#natural-image("../tiger.jpg")
```
