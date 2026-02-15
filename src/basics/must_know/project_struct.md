# 프로젝트 구조
## 대규모 문서

문서가 충분히 커지면 탐색하기 어려워집니다. 아직 그 정도 크기에 도달하지 않았다면 이 섹션을 무시해도 됩니다.

이를 관리하기 위해 문서를 _장(chapters)_으로 나누는 것을 추천합니다. 이것은 작업을 위한 한 가지 방법일 뿐이며, 작동 방식을 이해하면 원하는 대로 할 수 있습니다.

두 개의 장이 있다고 가정하면 추천 구조는 다음과 같습니다:

```typ
#import "@preview/treet:0.1.1": *

#show list: tree-list
#set par(leading: 0.8em)
#show list: set text(font: "Noto Sans CJK KR", size: 0.8em)
- chapters/
  - chapter_1.typ
  - chapter_2.typ
- main.typ 👁 #text(gray)[← 문서 진입점]
- template.typ
```

<div class="info">
정확한 파일 이름은 여러분에게 달려 있습니다.
</div>

각 파일에 무엇을 넣을지 살펴봅시다.

### 템플릿 (Template)

"template" 파일에는 장(chapter) 전체에서 사용할 _모든 유용한 함수와 변수_가 들어갑니다. 자신만의 템플릿이 있거나 템플릿을 작성하고 싶다면 여기에 작성할 수 있습니다.

```typ -norender
// template.typ

#let template = doc => {
    set page(header: "나의 멋진 문서")
    show "physics": "magic"
    doc
}

#let infoblock = block.with(stroke: blue, fill: blue.lighten(70%))
#let author = "@sitandr"
```

### 메인 (Main)

전체 컴파일된 문서를 얻으려면 **이 파일을 컴파일해야 합니다**.

```typ -norender
// main.typ

#import "template.typ": *
// 템플릿이 있다면
#show: template

= 이것은 문서 제목입니다

// 추가 서식

#show emph: set text(blue)

// 하지만 여기에 함수나 변수를 정의하지 마세요!
// 챕터에서는 볼 수 없습니다

// 이제 챕터 자체를 Typst 콘텐츠로 포함합니다
#include("chapters/chapter_1.typ")
#include("chapters/chapter_1.typ")
```

### 챕터 (Chapter)

```typ -norender
// chapter_1.typ

#import "../template.typ": *

_스타일링_ 과 블록이 있는 콘텐츠일 뿐입니다:

#infoblock[일부 정보].

// 문서에 포함하고 싶은 모든 콘텐츠
```

## 참고 사항

Typst의 모듈은 스스로 생성했거나 가져온(import) 것만 볼 수 있다는 점에 유의하세요. 그 외의 것은 보이지 않습니다. 그래서 `template.typ` 파일에 모든 함수를 정의해야 합니다.

즉, 챕터끼리도 _서로 볼 수 없으며_, 템플릿에 있는 것만 볼 수 있습니다.

## 순환 참조 (Cyclic imports)

**중요:** Typst는 순환 참조(cyclic imports)를 _금지_ 합니다. 즉, `chapter_1`에서 `chapter_2`를 가져오면서 동시에 `chapter_2`에서 `chapter_1`을 가져올 수 없습니다!

하지만 좋은 소식은 언제든지 변수를 가져올 다른 파일을 만들 수 있다는 것입니다.
