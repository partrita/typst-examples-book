# Try & Catch
```typ
// 저자: laurmaedje
// 이미지를 렌더링하거나 존재하지 않으면 자리 표시자를 렌더링합니다.
// 집에서 시도하지 마세요, 얘들아!
#let maybe-image(path, ..args) = context {
  let path-label = label(path)
   let first-time = query((context {}).func()).len() == 0
   if first-time or query(path-label).len() > 0 {
    [#image(path, ..args)#path-label]
  } else {
    rect(width: 50%, height: 5em, fill: luma(235), stroke: 1pt)[
      #set align(center + horizon)
      #raw(path)를 찾을 수 없습니다.
    ]
  }
}

#maybe-image("../tiger.jpg")
#maybe-image("../tiger1.jpg")
```