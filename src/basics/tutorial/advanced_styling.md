# 고급 스타일링

## `show` 규칙

```typ
고급 스타일링에는 또 다른 규칙인 _`show` 규칙_이 포함됩니다.

이제 소스 코드와 출력을 비교해 보세요.

#show "조심하세요": strong[놀아요]

이것은 매우 강력한 기능이며, 때로는 지나치게 강력할 수도 있습니다.
조심해서 사용하세요.

#show "인질로 잡혀 있어요": text(green)[전 괜찮아요]

잠깐, 뭐라고요? "조심하세요!"라고 했지 "놀아요!"라고 하지 않았는데요.

도와주세요, 인질로 잡혀 있어요.
```

## 이제 조금 더 진지하게

```typ
Show 규칙은 _선택자(selector)_와 그 선택자에 적용할 내용을
받는 강력한 기능입니다. 그 후 선택자가 가리키는
모든 요소를 찾아 규칙을 적용합니다.

다음과 같이 매우 유용하게 사용할 수 있습니다:

#show emph: set text(blue)

이제 무언가를 _강조(emphasize)_하고 싶을 때,
그것은 _강조_됨과 동시에 _파란색_이 됩니다.
멋지지 않나요?
```

## 구문에 대하여

```typ
때때로 show 규칙은 혼란스러울 수 있습니다. 매우 다양해 보일 수 있지만, 사실 모두 거의 동일합니다!

// 실제로 이것은 다음과 같습니다.
// redify = text.with(red)
// `with`는 해당 인수가 이미 설정된 새로운 함수를 생성합니다.
#let redify(string) = text(red, string)

// 그리고 이것은 다음과 같습니다.
// framify = rect.with(stroke: orange)
#let framify(object) = rect(object, stroke: orange)

// 이후의 모든 텍스트에 대해 기본 텍스트 색상을 파란색으로 설정합니다.
#show: set text(blue)

파란색 텍스트.

// 모든 것을 프레임으로 감쌉니다.
#show: framify

프레임이 씌워진 텍스트.

// 위와 동일하며, 단지 framify를 호출하는 새로운 함수를 생성할 뿐입니다.
#show: a => framify(a)

이중 프레임.

// `the`에 함수를 적용합니다.
#show "the": redify
// 모든 제목에 대해 텍스트 색상을 보라색으로 설정합니다.
#show heading: set text(purple)

= 결론

이 모든 규칙은 기본적으로 동일한 일을 수행하고 있습니다!
```

## 블록 (Blocks)

가장 중요한 용도 중 하나는 블록을 사용하여 모든 간격을 설정할 수 있다는 것입니다. 텍스트가 포함된 모든 요소에 텍스트 설정을 할 수 있는 것처럼, 모든 _블록 요소_는 블록 설정을 포함합니다:

```typ
텍스트 이전
= 제목
텍스트 이후

#show heading: set block(spacing: 0.5em)

텍스트 이전
= 제목
텍스트 이후
```

## 선택자 (Selector)

```typ
show 규칙은 _선택자_를 받을 수 있습니다.

선택자 유형에는 다음과 같은 것들이 있습니다:

- 요소 함수 (element functions)
- 문자열 (strings)
- 정규 표현식 (regular expressions)
- 필드 필터 (field filters)

마지막 사례의 예시를 보겠습니다:

#show heading.where(level: 1): set align(center)

= 제목
== 작은 제목

물론 수동으로 정렬을 설정할 수도 있으므로,
반드시 show 규칙을 사용할 필요는 없습니다
(하지만 매우 편리합니다!):

#align(center)[== 중앙 정렬된 작은 제목]
```

## 사용자 정의 서식

```typ
이제 사용자 정의 함수를 작성해 보겠습니다.
아주 쉽습니다. 직접 확인해 보세요:

// "it"은 제목(heading)입니다. 이를 가져와서 중괄호 안의 내용을 출력합니다.
#show heading: it => {
  // 중앙 정렬
  set align(center)
  // 크기와 굵기 설정
  set text(12pt, weight: "regular")
  // 블록과 박스에 대한 자세한 내용은
  // 해당 장을 참조하세요.
  block(smallcaps(it.body))
}

= Smallcaps 제목

```

## 간격 설정

TODO: 일반적인 요소에 대한 블록 간격 설명

## "논문 스타일"로 서식 지정하기

```typ
#set page(
  // 헤더는 상단의 작은 부분입니다.
  header: align(
    right + horizon,
    [여기에 헤더 내용]
  ),
  height: 12cm
)

#align(center, text(17pt)[
  *중요한 제목*
])

#grid(
  columns: (1fr, 1fr),
  align(center)[
    저자 성함 \
    소속 기관 \
    #link("mailto:some@mail.edu")
  ],
  align(center)[
    다른 저자 성함 \
    다른 소속 기관 \
    #link("mailto:another@mail.edu")
  ]
)

이제 텍스트를 두 열로 나누어 보겠습니다:

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

// 이제 단어들로 채워보겠습니다:

= 제목
== 작은 제목
#lorem(10)
== 두 번째 소단원
#lorem(10)
= 두 번째 제목
#lorem(40)

== 두 번째 소단원
#lorem(40)
```
