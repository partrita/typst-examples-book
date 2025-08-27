# 표와 그리드

문서에서 표를 사용할 계획이 없다면 표를 아는 것이 그다지 필요하지 않지만, 그리드는 _문서 레이아웃_에 매우 유용할 수 있습니다. 나중에 책에서 두 가지 모두를 사용할 것입니다.

공식 문서에서 예제를 복사하는 데 신경 쓰지 맙시다. 그냥 훑어보기만 하세요, 알겠죠?

## 기본 스니펫

### 펼치기

펼치기 연산자([여기](../scripting/arguments.md) 참조)는 표에 특히 유용할 수 있습니다:

```typ
#set text(size: 9pt)

#let yield_cells(n) = {
  for i in range(0, n + 1) {
    for j in range(0, n + 1) {
      let product = if i * j != 0 {
        // 더 나은 모양을 위해 수학을 사용합니다
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
          // 둘 중 하나가 0이면, 우리는 상단/왼쪽에 있습니다
          $#{i + j}$
        }
      }
      // 이것은 배열이며, for 루프는 셀들을 하나의 큰 배열로 병합합니다
      (
        table.cell(
          fill: if i == j and j == 0 { orange } // 오른쪽 상단 모서리
          else if i == j { yellow } // 대각선
          else if i * j == 0 { blue.lighten(50%) }, // 승수
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

### 표 행 강조하기

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

개별 셀의 경우, 다음을 사용하세요

```typ
#table(
  columns: 2,
  [A], [B],
  table.cell(fill: yellow)[C], table.cell(fill: yellow)[D],
  [E], [F],
  [G], [H],
)
```

### 표 분할하기

표는 페이지 간에 자동으로 분할됩니다.
```typ
#set page(height: 8em)
#(
table(
  columns: 5,
  [정렬기], [출판], [인덱싱], [쌍별 정렬], [최대 읽기 길이 (bp)],
  [BWA], [2009], [BWT-FM], [세미-글로벌], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [해싱], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [해싱], [NW], [36]
  )
)
```

그러나 다른 요소 내부에서 분할 가능하게 만들려면 해당 요소도 분할 가능하게 만들어야 합니다:

```typ
#set page(height: 8em)
// 이것이 없으면 표가 여러 페이지에 걸쳐 분할되지 않습니다
#show figure: set block(breakable: true)
#figure(
table(
  columns: 5,
  [정렬기], [출판], [인덱싱], [쌍별 정렬], [최대 읽기 길이 (bp)],
  [BWA], [2009], [BWT-FM], [세미-글로벌], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [해싱], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [해싱], [NW], [36]
  )
)
```
