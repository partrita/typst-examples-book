# 목록 항목 사이의 선 (Lines between list items)

```typ
/// 저자: frozolotl
#show enum.where(tight: false): it => {
  it.children
    .enumerate()
    .map(((n, item)) => block(below: .6em, above: .6em)[#numbering("1.", n + 1) #item.body])
    .join(line(length: 100%))
}

+ 항목 1

+ 항목 2

+ 항목 3
```

동일한 접근 방식을 사용하여 원하는 대로 열거형(enum) 스타일을 쉽게 조정할 수 있습니다.
