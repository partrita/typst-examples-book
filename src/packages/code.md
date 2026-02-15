# 코드 (Code)

## `codly`

> [문서](https://github.com/Dherse/codly)를 참조하세요.

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
    println!("Hello, world!");
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

이 보고서는 ArtosFlow 프로젝트에
포함되어 있습니다. ArtosFlow는
Artos Institute의 프로젝트입니다.
```]
``````