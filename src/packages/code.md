# 코드

## `codly`

> [여기](https://github.com/Dherse/codly)에서 문서 참조

``````typ
#import "@preview/codly:0.1.0": codly-init, codly, disable-codly
#show: codly-init.with()

#codly(languages: (
        typst: (name: "Typst", color: rgb("#41A241"), icon: none),
    ),
    breakable: false
)

```typst
#import "@preview/codly:0.1.0": codly-init
#show: codly-init.with()
```

// 여전히 서식이 지정됨!
```rust
pub fn main() {
    println!("안녕하세요, 세상!");
}
```

#disable-codly()
``````

## Codelst

``````typ
#import "@preview/codelst:2.0.0": sourcecode

#sourcecode[```typ
#show "ArtosFlow": name => box[
  #box(image(
    "logo.svg",
    height: 0.7em,
  ))
  #name
]

이 보고서는
ArtosFlow 프로젝트에 포함되어 있습니다. ArtosFlow는
Artos Institute의 프로젝트입니다.
```]
``````
