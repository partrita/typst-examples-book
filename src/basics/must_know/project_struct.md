# 프로젝트 구조
## 큰 문서

문서가 충분히 커지면 탐색하기가 더 어려워집니다. 아직 그 크기에 도달하지 않았다면 이 섹션을 무시해도 됩니다.

이를 관리하기 위해 문서를 _챕터_로 나누는 것을 추천합니다. 이것은 단지 이 문제를 다루는 한 가지 방법일 뿐이지만, 일단 작동 방식을 이해하면 원하는 모든 것을 할 수 있습니다.

두 개의 챕터가 있다고 가정하면, 권장되는 구조는 다음과 같습니다:

```typ
#import "@preview/treet:0.1.1": *

#show list: tree-list
#set par(leading: 0.8em)
#show list: set text(font: "DejaVu Sans Mono", size: 0.8em)
- chapters/
  - chapter_1.typ
  - chapter_2.typ
- main.typ 👁 #text(gray)[← 문서 진입점]
- template.typ
```

<div class="info">
정확한 파일 이름은 사용자가 정할 수 있습니다.
</div>

각 파일에 무엇을 넣을지 봅시다.

### 템플릿

"템플릿" 파일에는 챕터 전반에 걸쳐 사용할 _모든 유용한 함수와 변수_가 들어갑니다. 자신만의 템플릿이 있거나 작성하고 싶다면 여기에 작성할 수 있습니다.

```typ -norender
// template.typ

#let template = doc => {
    set page(header: "나의 슈퍼 문서")
    show "physics": "마법"
    doc
}

#let infoblock = block.with(stroke: blue, fill: blue.lighten(70%))
#let author = "@sitandr"
```

### 메인

전체 컴파일된 문서를 얻으려면 **이 파일을 컴파일해야 합니다**.

```typ -norender
// main.typ

#import "template.typ": *
// 템플릿이 있는 경우
#show: template

= 이것은 문서 제목입니다

// 일부 추가 서식

#show emph: set text(blue)

// 하지만 여기에 함수나 변수를 정의하지 마세요!
// 챕터에서 볼 수 없습니다

// 이제 챕터 자체를 일부 Typst 콘텐츠로
#include("chapters/chapter_1.typ")
#include("chapters/chapter_1.typ")
```

### 챕터

```typ -norender
// chapter_1.typ

#import "../template.typ": *

이것은 _스타일링_과 블록이 있는 콘텐츠일 뿐입니다:

#infoblock[일부 정보].

// 문서에 포함하려는 모든 콘텐츠
```

## 참고

Typst의 모듈은 스스로 만들었거나 가져온 것만 볼 수 있다는 점에 유의하세요. 다른 모든 것은 보이지 않습니다. 그렇기 때문에 모든 함수를 정의하려면 `template.typ` 파일이 필요합니다.

이는 챕터가 _서로를 볼 수 없으며_, 템플릿에 있는 것만 볼 수 있다는 의미입니다.

## 순환 가져오기

**중요:** Typst는 순환 가져오기를 _금지_합니다. 즉, `chapter_1`에서 `chapter_2`를 가져오고 동시에 `chapter_2`에서 `chapter_1`을 가져올 수 없습니다!

하지만 좋은 소식은 변수를 가져올 다른 파일을 언제든지 만들 수 있다는 것입니다.
