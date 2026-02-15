# 벡터 및 행렬

벡터와 행렬마다 간격이 반드시 일정하거나 같지 않다는 것을 쉽게 알 수 있습니다:

```typ
$
mat(0, 1, -1; -1, 0, 1; 1, -1, 0) vec(a/b, a/b, a/b) = vec(c, d, e)
$
```
이는 `gap`이 요소의 중심 간 거리가 아니라 요소 _사이의 간격_을 의미하기 때문에 발생합니다.

이를 해결하려면 이 스니펫을 사용할 수 있습니다:

```typ
// 높이 고정 벡터
#let fvec(..children, delim: "(", gap: 1.5em) = { // 여기서 기본 간격 변경
  context math.vec(
      delim: delim,
      gap: 0em,
      ..for el in children.pos() {
        ({
          box(
            width: measure(el).width,
            height: gap, place(horizon, el)
          )
        },) // 이것은 배열입니다
        // `for`는 이 모든 배열을 병합한 다음, 인수로 전달합니다.
      }
    )
}

// 높이 고정 행렬
// row-gap, column-gap, gap도 허용
#let fmat(..rows, delim: "(", augment: none) = {
  let args = rows.named()
  let (gap, row-gap, column-gap) = (none,)*3;

  if "gap" in args {
    gap = args.at("gap")
    row-gap = args.at("row-gap", default: gap)
    column-gap = args.at("row-gap", default: gap)
  }
  else {
    // 여기서 기본 수직 간격 변경
    row-gap = args.at("row-gap", default: 1.5em) 
    // 그리고 수평 간격은 여기서
    column-gap = rows.named().at("column-gap", default: 0.5em)
  }

  context math.mat(
      delim: delim,
      row-gap: 0em,
      column-gap: column-gap,
      ..for row in rows.pos() {
        (for el in row {
          ({
          box(
            width: measure(el).width,
            height: row-gap, place(horizon, el)
          )
        },)
        }, )
      }
    )
}

$
"Before:"& vec(((a/b))/c, a/b, c) = vec(1, 1, 1)\
"After:"& fvec(((a/b))/c, a/b, c) = fvec(1, 1, 1)\

"Before:"& mat(a, b; c, d) vec(e, dot) = vec(c/d, e/f)\
"After:"& fmat(a, b; c, d) fvec(e, dot) = fvec(c/d, e/f)
$
```
