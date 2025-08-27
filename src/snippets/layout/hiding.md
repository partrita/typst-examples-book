# 숨기기

```typ
// 저자: GeorgeMuscat
#let redact(text, fill: black, height: 1em) = {
  box(rect(fill: fill, height: height)[#hide(text)])
}

예:
  - 수정되지 않은 텍스트
  - 수정된 #redact("text")
```