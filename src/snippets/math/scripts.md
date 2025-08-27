# 스크립트

> 스크립트 및 제한 설정은 [Typst 기본 섹션](../../basics/math/limits.md)을 참조하세요.

## 아래 첨자에 사용될 때 모든 문자를 정자로 만들기

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
