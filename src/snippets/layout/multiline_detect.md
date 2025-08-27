# 여러 줄 감지

그림 캡션(다른 요소일 수 있음)에 _한 줄 이상_이 있는지 감지합니다.

캡션이 여러 줄이면 왼쪽 정렬됩니다.

<div class="warning">
 수동 줄 바꿈에서 깨집니다.
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