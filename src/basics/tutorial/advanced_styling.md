# 고급 스타일링

## `show` 규칙

```typ
고급 스타일링은 또 다른 규칙과 함께 제공됩니다. 바로 _`show` 규칙_입니다.

이제 소스 코드와 출력을 비교해 보세요.

#show "Be careful": strong[Play]

이것은 매우 강력한 기능이며, 때로는 너무 강력하기도 합니다.
조심해서 사용하세요.

#show "it is holding me hostage": text(green)[I'm fine]

잠깐, 뭐라고요? 저는 "조심하세요!"라고 말했지, "놀아!"라고 말하지 않았습니다.

도와주세요, 인질로 잡혀있어요.
```

## 이제 좀 더 진지하게

```typ
Show 규칙은 _선택자_와
그것에 적용할 것을 받는 강력한 기능입니다.
그 후에는 찾을 수 있는 모든 요소에 적용됩니다.

이처럼 매우 유용할 수 있습니다:

#show emph: set text(blue)

이제 무언가를 _강조_하고 싶다면,
그것은 _강조_되면서 _파란색_이 될 것입니다.
멋지지 않나요?
```

## 구문에 대하여

```typ
때때로 show 규칙은 혼란스러울 수 있습니다. 매우 다양해 보일 수 있지만, 사실은 모두 거의 같습니다! 그러니

// 사실, 이것은 다음과 같습니다
// redify = text.with(red)
// `with`는 해당 인수가 이미 설정된 새 함수를 만듭니다
#let redify(string) = text(red, string)

// 그리고 이것은 다음과 같습니다
// framify = rect.with(stroke: orange)
#let framify(object) = rect(object, stroke: orange)

// 다음 모든 텍스트의 기본 색상을 파란색으로 설정합니다
#show: set text(blue)

파란 텍스트.

// 모든 것을 프레임으로 감쌉니다
#show: framify

프레임된 텍스트.

// framify를 호출하는 새 함수를 만드는 것과 같습니다
#show: a => framify(a)

이중 프레임.

// `the`에 함수를 적용합니다
#show "the": redify
// 모든 제목의 텍스트 색상을 보라색으로 설정합니다
#show heading: set text(purple)

= 결론

이 모든 규칙은 기본적으로 같은 일을 합니다!
```

## 블록

가장 중요한 사용법 중 하나는 블록을 사용하여 모든 간격을 설정할 수 있다는 것입니다. 텍스트가 있는 모든 요소에 설정할 수 있는 텍스트가 포함되어 있듯이, 모든 _블록 요소_에는 블록이 포함됩니다:

```typ
이전 텍스트
= 제목
이후 텍스트

#show heading: set block(spacing: 0.5em)

이전 텍스트
= 제목
이후 텍스트
```

## 선택자

```typ
그래서 show 규칙은 _선택자_를 받아들일 수 있습니다.

다양한 선택자 유형이 있습니다.
예를 들어

- 요소 함수
- 문자열
- 정규 표현식
- 필드 필터

후자의 예를 봅시다:

#show heading.where(level: 1): set align(center)

= 제목
== 작은 제목

물론, 수동으로 정렬을 설정할 수 있습니다.
show 규칙을 사용할 필요는 없습니다
(하지만 매우 편리합니다!):

#align(center)[== 가운데 정렬된 작은 제목]
```

## 사용자 정의 서식

```typ
이제 사용자 정의 함수를 작성해 봅시다.
매우 쉽습니다, 직접 보세요:

// "it"은 제목이며, 그것을 가져와 중괄호 안에 있는 것을 출력합니다
#show heading: it => {
  // 가운데 정렬
  set align(center)
  // 크기와 굵기 설정
  set text(12pt, weight: "regular")
  // 블록과 상자에 대한 자세한 내용은
  // 해당 챕터에서 확인하세요
  block(smallcaps(it.body))
}

= 소문자 대문자 제목

```

## 간격 설정

TODO: 일반적인 요소에 대한 블록 간격 설명

## "기사처럼 보이도록" 서식 지정하기

```typ
#set page(
  // 헤더는 상단의 작은 것입니다
  header: align(
    right + horizon,
    [여기에 헤더]
  ),
  height: 12cm
)

#align(center, text(17pt)[
  *중요한 제목*
])

#grid(
  columns: (1fr, 1fr),
  align(center)[
    어떤 저자 \
    어떤 기관 \
    #link("mailto:some@mail.edu")
  ],
  align(center)[
    다른 저자 \
    다른 기관 \
    #link("mailto:another@mail.edu")
  ]
)

이제 텍스트를 두 개의 열로 나눕니다:

#show: rest => columns(2, rest)

#show heading.where(
  level: 1
): it => block(width: 100%)[
  #set align(center)
  #set text(12pt, weight: "regular")
  #smallcaps(it.body)
]

#show heading.where(
  level: 2
): it => text(
  size: 11pt,
  weight: "regular",
  style: "italic",
  it.body + [.],
)

// 이제 단어로 채워 봅시다:

= 제목
== 작은 제목
#lorem(10)
== 두 번째 하위 챕터
#lorem(10)
= 두 번째 제목
#lorem(40)

== 두 번째 하위 챕터
#lorem(40)
```
