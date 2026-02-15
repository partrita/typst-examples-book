# 고급 스타일링

## `show` 규칙

```typ
스타일링의 정점에는 **`show` 규칙**이 있습니다. 
소스 코드와 출력 결과를 비교하며 어떻게 작동하는지 확인해 보세요.

#show "조심하세요": strong[놀아요]

이 기능은 매우 강력해서 문서의 내용을 완전히 뒤바꿀 수도 있습니다. 
따라서 신중하게 사용해야 합니다.

#show "인질로 잡혀 있어요": text(green)[전 괜찮아요]

방금 어떤 일이 일어났나요? 소스 코드에는 분명 "조심하세요"라고 적었지만, 
실제 문서에는 "놀아요"라고 출력되었습니다. 

도와주세요, 인질로 잡혀 있어요.
```

## 더 실용적인 활용법

```typ
`show` 규칙은 특정 **선택자(selector)**를 찾아 
원하는 형태나 스타일로 변형하는 기능을 제공합니다.

다음 예제처럼 매우 실용적으로 활용할 수 있습니다.

#show emph: set text(blue)

이제 문서 전체에서 _강조(emphasize)_된 텍스트는 
기울임꼴과 동시에 **파란색** 으로 표시됩니다. 
일일이 색상을 지정할 필요가 없어 매우 편리합니다.
```

## `show` 규칙의 다양한 문법

```typ
`show` 규칙은 겉보기에 복잡해 보일 수 있지만, 근본적인 원리는 모두 같습니다. 

// 아래 예제들은 기본적으로 특정 함수를 입히는 것과 같습니다.
// `with`는 인자가 미리 설정된 새로운 함수를 만듭니다.
#let redify(string) = text(red, string)

// 주황색 테두리를 입히는 함수 정의
#let framify(object) = rect(object, stroke: orange)

// 문서 전체의 기본 글자 색상을 파란색으로 설정
#show: set text(blue)

파란색 글자들.

// 모든 요소를 사각형 프레임으로 감싸기
#show: framify

프레임이 씌워진 텍스트.

// 익명 함수를 사용해 위와 동일한 효과를 낼 수도 있습니다.
#show: a => framify(a)

이중 프레임.

// 특정 단어 "the"에만 빨간색 적용
#show "the": redify
// 모든 제목(heading)의 색상을 보라색으로 설정
#show heading: set text(purple)

= 결론

결국 이 모든 규칙은 '무엇을(선택자)', '어떻게(변형)' 바꿀 것인지를 정의하는 과정입니다.
```

## 블록 (Blocks)

`show` 규칙의 가장 중요한 용도 중 하나는 간격을 조절하는 것입니다. 텍스트 설정을 통해 글자 모양을 바꾸듯, 모든 **블록 요소**에도 스타일을 적용할 수 있습니다.

```typ
텍스트 이전
= 제목
텍스트 이후

#show heading: set block(spacing: 0.5em)

텍스트 이전
= 제목
텍스트 이후
```

## 선택자 (Selector) 활용

```typ
`show` 규칙은 다음과 같은 다양한 선택자를 사용할 수 있습니다.

- 요소 함수 (element functions)
- 문자열 (strings)
- 정규 표현식 (regular expressions)
- 필드 필터 (field filters)

특정 조건에만 스타일을 적용하는 예시를 살펴보겠습니다.

#show heading.where(level: 1): set align(center)

= 1단계 제목 (중앙 정렬됨)
== 2단계 제목 (기본 정렬)

물론 개별 요소에서 직접 설정할 수도 있지만, 
`show` 규칙을 쓰면 일관된 스타일을 유지하기 훨씬 쉽습니다.

#align(center)[== 수동으로 정렬한 제목]
```

## 사용자 정의 서식 만들기

```typ
제목 스타일을 완전히 새롭게 정의하는 함수를 직접 작성해 봅시다.

// "it"은 선택된 제목(heading) 객체입니다.
#show heading: it => {
  // 중앙 정렬 설정
  set align(center)
  // 글자 크기와 굵기 설정
  set text(12pt, weight: "regular")
  
  // 내용을 작은 대문자(smallcaps)로 변환하고 블록으로 감쌉니다.
  block(smallcaps(it.body))
}

= Smallcaps Heading Example
```

## "논문 스타일" 예제

Typst의 강력한 스타일링 기능을 조합하면 복잡한 논문 형식도 금방 만들 수 있습니다.

```typ
#set page(
  // 상단 헤더 설정
  header: align(
    right + horizon,
    [여기에 헤더 내용 입력]
  ),
  height: 12cm
)

#align(center, text(17pt)[
  *문서의 주요 제목*
])

#grid(
  columns: (1fr, 1fr),
  align(center)[
    저자 성함 \
    소속 기관 \
    #link("mailto:some@mail.edu")
  ],
  align(center)[
    공동 저자 \
    공동 소속 기관 \
    #link("mailto:another@mail.edu")
  ]
)

// 본문을 두 단(2 columns)으로 나눕니다.
#show: rest => columns(2, rest)

// 1단계 제목 스타일 정의
#show heading.where(level: 1): it => block(width: 100%)[
  #set align(center)
  #set text(12pt, weight: "regular")
  #smallcaps(it.body)
]

// 2단계 제목 스타일 정의 (이탤릭체 및 마침표 추가)
#show heading.where(level: 2): it => text(
  size: 11pt,
  weight: "regular",
  style: "italic",
  it.body + [.],
)

= 서론
== 소제목 예시
#lorem(15)

== 두 번째 섹션
#lorem(20)

= 본론
#lorem(40)
```
