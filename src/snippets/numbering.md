# 번호 매기기
## 번호 없는 개별 제목
```typ
#let numless(it) = {set heading(numbering: none); it }

= 제목
#numless[=번호 없는 제목]
```

## "깨끗한" 번호 매기기
```typ
// 원저자: tromboneher

// 여러 체계에 따라 섹션 번호를 매기되, 이전 선행 요소는 생략합니다.
// 예를 들어, 번호 매기기 패턴 "A.I.1."이 다음과 같이 생성되는 경우:
//
// A. 이야기의 일부
//   A.I. 한 챕터
//   A.II. 다른 챕터
//     A.II.1. 한 섹션
//       A.II.1.a. 하위 섹션
//       A.II.1.b. 다른 하위 섹션
//     A.II.2. 다른 섹션
// B. 이야기의 다른 부분
//   B.I. 두 번째 부분의 한 챕터
//   B.II. 두 번째 부분의 다른 챕터
//
// clean_numbering("A.", "I.", "1.a.")는 다음과 같이 생성됩니다:
//
// A. 이야기의 일부
//   I. 한 챕터
//   II. 다른 챕터
//     1. 한 섹션
//       1.a. 하위 섹션
//       1.b. 다른 하위 섹션
//     2. 다른 섹션
// B. 이야기의 다른 부분
//   I. 두 번째 부분의 한 챕터
//   II. 두 번째 부분의 다른 챕터
//
#let clean_numbering(..schemes) = {
  (..nums) => {
    let (section, ..subsections) = nums.pos()
    let (section_scheme, ..subschemes) = schemes.pos()

    if subsections.len() == 0 {
      numbering(section_scheme, section)
    } else if subschemes.len() == 0 {
      numbering(section_scheme, ..nums.pos())
    }
    else {
      clean_numbering(..subschemes)(..subsections)
    }
  }
}

#set heading(numbering: clean_numbering("A.", "I.", "1.a."))

= 부분
== 챕터
== 다른 챕터
=== 섹션
==== 하위 섹션
==== 다른 하위 섹션
= 이야기의 다른 부분
== 두 번째 부분의 한 챕터
== 두 번째 부분의 다른 챕터
```

## 수학 번호 매기기
[여기](./math/numbering.md)를 참조하세요.

## 각 단락 번호 매기기

<div class="warning">
  Typst의 0.12 버전부터는 이것이 좋은 기본 솔루션으로 대체되어야 합니다.
<div>

```typ
// 원저자: roehlichA
// 열거형의 법적 서식
#show enum: it => context {
  // 마지막 제목을 검색하여 어느 수준에서 단계별로 진행해야 하는지 알 수 있습니다.
  let headings = query(selector(heading).before(here()))
  let last = headings.at(-1)

  // 출력 항목 결합
  let output = ()
  for item in it.children {
    output.push([
      #context{
        counter(heading).step(level: last.level + 1)
      }
      #context {
        counter(heading).display() 
      }
    ])
    output.push([
      #text(item.body)
      #parbreak()
    ])
  }

  // 그리드에 표시
  grid(
    columns: (auto, 1fr),
    column-gutter: 1em,
    row-gutter: 1em,
    ..output
  )

}

#set heading(numbering: "1.")

= 일부 제목
+ 단락
= 기타
+ 여기 단락 앞에는 참조할 수 있도록 번호가 붙습니다.
+ _#lorem(100)_
+ _#lorem(100)_

== 하위 제목
+ 단락은 하위 제목에서도 올바르게 번호가 매겨집니다.
+ _#lorem(50)_
+ _#lorem(50)_
```
