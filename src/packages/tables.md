# 표

## Tada: 데이터 조작

```typ
#import "@preview/tada:0.2.0"

#let column-data = (
  name: ("빵", "우유", "계란"),
  price: (1.25, 2.50, 1.50),
  quantity: (2, 1, 3),
)
#let record-data = (
  (name: "빵", price: 1.25, quantity: 2),
  (name: "우유", price: 2.50, quantity: 1),
  (name: "계란", price: 1.50, quantity: 3),
)
#let row-data = (
  ("빵", 1.25, 2),
  ("우유", 2.50, 1),
  ("계란", 1.50, 3),
)

#import tada: TableData, to-tablex
#let td = TableData(data: column-data)
// 다음과 동일:
#let td2 = tada.from-records(record-data)
// 다음과 같지 않음(필드 이름을 알 수 없으므로):
#let td3 = tada.from-rows(row-data)

#to-tablex(td)
#to-tablex(td2)
#to-tablex(td3)
```

## Tablem: 마크다운 표

> [여기](https://github.com/OrangeX4/typst-tablem)에서 문서 참조

Typst에서 마크다운 표를 렌더링합니다.

```typ
#import "@preview/tablem:0.2.0": tablem

#tablem[
  | *이름* | *위치* | *키* | *점수* |
  | ------ | ---------- | -------- | ------- |
  | John   | Second St. | 180 cm   |  5      |
  | Wally  | Third Av.  | 160 cm   |  10     |
]
```

### 사용자 정의 렌더링

```typ
#import "@preview/tablex:0.0.6": tablex, hlinex
#import "@preview/tablem:0.1.0": tablem

#let three-line-table = tablem.with(
  render: (columns: auto, ..args) => {
    tablex(
      columns: columns,
      auto-lines: false,
      align: center + horizon,
      hlinex(y: 0),
      hlinex(y: 1),
      ..args,
      hlinex(),
    )
  }
)

#three-line-table[
  | *이름* | *위치* | *키* | *점수* |
  | ------ | ---------- | -------- | ------- |
  | John   | Second St. | 180 cm   |  5      |
  | Wally  | Third Av.  | 160 cm   |  10     |
]
```
