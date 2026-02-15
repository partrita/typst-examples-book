# 첨자 (Scripts)

> 첨자 및 극한 설정에 대해서는 [Typst 기초 섹션](../../basics/math/limits.md)을 참조하세요.

## 아래첨자에 사용되는 모든 문자를 직립체(upright)로 만들기

```typ
// 저자: emilyyyylime

$f_a, f_b, f^a, f_italic("word")$
#show math.attach: it => {
  import math: *
  if it.b != none and it.b.func() != upright[].func() and it.b.has("text") and it.b.text.len() == 1 {
    let args = it.fields()
    let _ = args.remove("base")
    let _ = args.remove("b")
    attach(it.base, b: upright(it.b), ..args)
  } else {
    it
  }
}

$f_a, f_b, f^a, f_italic("word")$
```
