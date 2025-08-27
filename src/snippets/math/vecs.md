# 벡터 및 행렬

벡터 및 행렬에서 간격이 반드시 균일하거나 다른 벡터 및 행렬에서 동일하지 않다는 것을 쉽게 알 수 있습니다:

```typ
$ 
mat(0, 1, -1; -1, 0, 1; 1, -1, 0) vec(a/b, a/b, a/b) = vec(c, d, e)
$ 
```
`gap`이 요소 중심 사이의 거리가 아니라 요소 _사이의 간격_을 참조하기 때문에 발생합니다.

이 문제를 해결하려면 이 스니펫을 사용할 수 있습니다:

```typ
// 고정 높이 벡터
#let fvec(..children, delim: "(", gap: 1.5em) = { // 여기서 기본 간격 변경
  context math.vec(
      delim: delim,
      gap: 0em,
      ..for el in children.pos() {
        (({
          box(
            width: measure(el).width,
            height: gap, place(horizon, el)
          )
        },))
      }
    )
}

// 고정 높이 행렬
// row-gap, column-gap 및 gap도 허용합니다.
#let fmat(..rows, delim: "(", augment: none) = {
  let args = rows.named()
  let (gap, row-gap, column-gap) = (none,) * 3;

  if "gap" in args {
    gap = args.at("gap")
    row-gap = args.at("row-gap", default: gap)
    column-gap = rows.named().at("column-gap", default: gap)
  }
  else {
    // 여기서 기본 수직 변경
    row-gap = args.at("row-gap", default: 1.5em) 
    // 그리고 여기서 수평 변경
    column-gap = rows.named().at("column-gap", default: 0.5em)
  }

  context math.mat(
      delim: delim,
      row-gap: 0em,
      column-gap: column-gap,
      ..for row in rows.pos() {
        (for el in row {
          (({
          box(
            width: measure(el).width,
            height: row-gap, place(horizon, el)
          )
        },),)
        }, )
      }
    )
}

$ 
"이전:"& vec(((a/b))/c, a/b, c) = vec(1, 1, 1)
"이후:"& fvec(((a/b))/c, a/b, c) = fvec(1, 1, 1)

"이전:"& mat(a, b; c, d) vec(e, dot) = vec(c/d, e/f)
"이후:"& fmat(a, b; c, d) fvec(e, dot) = fvec(c/d, e/f)
$ 
```

```