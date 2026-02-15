# 번호 매기기
## 번호 없는 개별 제목
```typ
#let numless(it) = {set heading(numbering: none); it }

= 제목
#numless[= 번호 없는 제목]
```

## "클린(Clean)" 번호 매기기
```typ
// 원저자: tromboneher

// 이전의 상위 요소를 생략하고 섹션 번호를 매깁니다.
// 예를 들어, 번호 매기기 패턴 "A.I.1."이 다음과 같이 생성된다면:
//
// A. 이야기의 한 부분
//   A.I. 장(Chapter)
//   A.II. 다른 장
//     A.II.1. 섹션
//       A.II.1.a. 서브섹션
//       A.II.1.b. 다른 서브섹션
//     A.II.2. 다른 섹션
// B. 이야기의 다른 부분
//   B.I. 두 번째 부분의 장
//   B.II. 두 번째 부분의 다른 장
//
// clean_numbering("A.", "I.", "1.a.")은 다음과 같이 생성됩니다:
//
// A. 이야기의 한 부분
//   I. 장
//   II. 다른 장
//     1. 섹션
//       1.a. 서브섹션
//       1.b. 다른 서브섹션
//     2. 다른 섹션
// B. 이야기의 다른 부분
//   I. 두 번째 부분의 장
//   II. 두 번째 부분의 다른 장
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

= 부(Part)
== 장(Chapter)
== 다른 장
=== 섹션
==== 서브섹션
==== 다른 서브섹션
= 이야기의 다른 부분
== 두 번째 부분의 장
== 두 번째 부분의 다른 장
```

## 수학 번호 매기기
[여기](./math/numbering.md)를 참조하세요.

## 각 단락에 번호 매기기

<div class="warning">
  Typst 0.12 버전부터는 이 기능을 네이티브 솔루션으로 대체해야 합니다.
<div>

```typ
// 원저자: roehlichA
// 열거형의 법률적 서식
#show enum: it => context {
  // 어떤 수준에서 단계를 밟을지 알기 위해 마지막 제목을 가져옵니다
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

= 어떤 제목
+ 단락
= 기타
+ 여기의 단락 앞에는 번호가 붙어 있어 직접 참조할 수 있습니다.
+ _#lorem(100)_
+ _#lorem(100)_

== 서브섹션
+ 단락은 서브섹션에서도 올바르게 번호가 매겨집니다.
+ _#lorem(50)_
+ _#lorem(50)_
```
