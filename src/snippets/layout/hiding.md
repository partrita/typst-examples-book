# 무언가 숨기기 (Hiding things)

```typ
// 저자: GeorgeMuscat
#let redact(text, fill: black, height: 1em) = {
  box(rect(fill: fill, height: height)[#hide(text)])
}

예시:
  - 가려지지 않은 텍스트
  - 가려진 #redact("텍스트")
```
