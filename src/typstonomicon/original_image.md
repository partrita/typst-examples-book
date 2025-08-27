# 원본 크기의 이미지
이 함수는 이미지가 "자연스럽게" 가진 크기로 이미지를 렌더링합니다.

**참고: v0.11부터**, Typst는 너비와 높이가 `auto`일 때 기본 이미지 크기를 사용하려고 시도합니다. 이미지가 맞지 않는 경우에만 컨테이너의 크기를 사용합니다. 따라서 이 코드는 레거시에 가깝지만 여전히 유용할 수 있습니다.

이것은 measure가 개념적으로 이미지를 무한한 크기의 페이지에 배치한 다음 이미지가 무한히 커지는 대신 픽셀당 1pt로 기본 설정되기 때문에 작동합니다.

```typ
// 저자: laurmaedje
#let natural-image(..args) = style(styles => {
  let (width, height) = measure(image(..args), styles)
  image(..args, width: width, height: height)
})

#image("../tiger.jpg")
#natural-image("../tiger.jpg")
```
