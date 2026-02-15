# 표와 그리드 (Tables and grids)

문서에서 표를 사용할 계획이 없다면 표에 대해 반드시 알 필요는 없지만, 그리드(grid)는 _문서 레이아웃_에 매우 유용할 수 있습니다. 나중에 책에서 두 가지 모두를 사용할 것입니다.

공식 문서의 예제를 복사하는 데 시간을 낭비하지 맙시다. 그냥 가볍게 훑어만 보세요, 알겠죠?

## 기본 스니펫

### 전개 (Spreading)

전개 연산자([여기](../scripting/arguments.md) 참조)는 특히 표에서 유용할 수 있습니다:

```typ
#set text(size: 9pt)

#let yield_cells(n) = {
  for i in range(0, n + 1) {
    for j in range(0, n + 1) {
      let product = if i * j != 0 {
        // 더 예쁜 외관을 위해 수식 사용
        if j <= i { $#{ j * i }$ } 
        else {
          // 표의 윗부분
          text(gray.darken(50%), str(i * j))
        }
      } else {
        if i == j {
          // 오른쪽 상단 모서리 
          $times$
        } else {
          // 둘 중 하나가 0이면 상단/좌측에 위치함
          $#{i + j}$
        }
      }
      // 이것은 배열이며, for 루프는 이들을 
      // 하나의 커다란 셀 배열로 병합합니다.
      (
        table.cell(
          fill: if i == j and j == 0 { orange } // 오른쪽 상단 모서리
          else if i == j { yellow } // 대각선
          else if i * j == 0 { blue.lighten(50%) }, // 곱하는 수
          product,),
      )
    }
  }
}

#let n = 10
#table(
  columns: (0.6cm,) * (n + 1), rows: (0.6cm,) * (n + 1), align: center + horizon, inset: 3pt, ..yield_cells(n),
)
```

### 표의 행 강조하기

```typ
#table(
  columns: 2,
  fill: (x, y) => if y == 2 { highlight.fill },
  [A], [B],
  [C], [D],
  [E], [F],
  [G], [H],
)
```

개별 셀의 경우 다음과 같이 사용합니다:

```typ
#table(
  columns: 2,
  [A], [B],
  table.cell(fill: yellow)[C], table.cell(fill: yellow)[D],
  [E], [F],
  [G], [H],
)
```

### 표 나누기

표는 페이지 사이에서 자동으로 나뉩니다.
```typ
#set page(height: 8em)
#(
table(
  columns: 5,
  [Aligner], [publication], [Indexing], [Pairwise alignment], [Max. read length  (bp)],
  [BWA], [2009], [BWT-FM], [Semi-Global], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [Hashing], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [Hashing], [NW], [36]
  )
)
```

하지만 다른 요소 내부에서 표를 나눌 수 있게 하려면, 해당 요소도 나눌 수 있게 만들어야 합니다:

```typ
#set page(height: 8em)
// 이것이 없으면 표가 여러 페이지에 걸쳐 나뉘지 못합니다.
#show figure: set block(breakable: true)
#figure(
table(
  columns: 5,
  [Aligner], [publication], [Indexing], [Pairwise alignment], [Max. read length  (bp)],
  [BWA], [2009], [BWT-FM], [Semi-Global], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [Hashing], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [Hashing], [NW], [36]
  )
)
```
