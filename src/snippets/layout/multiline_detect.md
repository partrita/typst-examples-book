# 여러 줄 감지 (Multiline detection)

그림 캡션(또는 다른 요소)이 _한 줄보다 많은지_ 감지합니다.

캡션이 여러 줄인 경우 왼쪽 정렬로 설정합니다.

<div class="warning">
 수동 줄 바꿈(manual linebreaks)에서는 제대로 작동하지 않을 수 있습니다.
</div>

`````typ
#show figure.caption: it => {
  layout(size => context [
    #let text-size = measure(
      ..size,
      it.supplement + it.separator + it.body,
    )

    #let my-align

    #if text-size.width < size.width {
      my-align = center
    } else {
      my-align = left
    }

    #align(my-align, it)
  ])
}

#figure(caption: lorem(6))[
    ```rust
    pub fn main() {
        println!("Hello, world!");
    }
    ```
]

#figure(caption: lorem(20))[
    ```rust
    pub fn main() {
        println!("Hello, world!");
    }
    ```
]
`````
