# 조건문 및 루프

## 조건문
> [공식 문서](https://typst.app/docs/reference/scripting/#conditionals) 참조.

Typst에서는 `if-else` 문을 사용할 수 있습니다.
이것은 인수 유형이나 다른 여러 가지에 따라 동작을 변경하기 위해 함수 본문 내에서 특히 유용합니다.

```typ
#if 1 < 2 [
  이것은 표시됩니다
] else [
  이것은 표시되지 않습니다.
]
```

물론 `else`는 불필요합니다:

```typ
#let a = 3

#if a < 4 {
  a = 5
}

#a
```

`else if` 문(Python에서는 `elif`로 알려짐)을 사용할 수도 있습니다:

```typ
#let a = 5

#if a < 4 {
  a = 5
} else if a < 6 {
  a = -3
}

#a
```

### 불리언

`if, else if, else`는 스위치로 _불리언 값만_ 허용합니다.
[타입 섹션](./types.md#boolean-bool)에서 설명한 대로 불리언을 결합할 수 있습니다:

```typ
#let a = 5

#if (a > 1 and a <= 4) or a == 5 [
    `a`가 조건과 일치합니다
]
```

### Set-if

Typst는 매우 유용한 지시문인 `set if`를 지원하며, 조건이 적용되면 set 규칙을 사용합니다. 이것은 전체 문서 또는 함수 내에서 조건부 스타일링에 매우 유용할 수 있습니다:

```typ
#let draft = true

// 여기서 어떤 조건 연산이든 할 수 있습니다
#set page(columns: 2, width: 20em, height: 10em) if not draft

// 그리고 show 규칙 내에서도 사용할 수 있습니다
#show "TODO": set text(red, size: 2em) if draft

TODO: 실제 텍스트 작성

#lorem(50)
```

## 루프

> [공식 문서](https://typst.app/docs/reference/scripting/#loops) 참조.

루프에는 `while`과 `for`의 두 종류가 있습니다. While은 조건이 충족되는 동안 본문을 반복합니다:

```typ
#let a = 3

#while a < 100 {
    a *= 2
    str(a)
    " "
}
```

`for`는 시퀀스의 모든 요소를 반복합니다. 시퀀스는 `array`, `string`
또는 `dictionary`(`for`는 _키-값 쌍_을 반복함)일 수 있습니다.

```typ
#for c in "ABC" [
  #c는 글자입니다.
]
```

`a`에서 `b`까지의 모든 숫자를 반복하려면 `range(a, b+1)`를 사용하세요:

```typ
#let s = 0

#for i in range(3, 6) {
    s += i
    [숫자 #i가 합계에 추가되었습니다. 이제 합계는 #s입니다.]
}
```

범위는 끝을 포함하지 않으므로 이것은 다음과 같습니다

```typ
#let s = 0

#for i in (3, 4, 5) {
    s += i
    [숫자 #i가 합계에 추가되었습니다. 이제 합계는 #s입니다.]
}
```

```typ
#let people = (Alice: 3, Bob: 5)

#for (name, value) in people [
    #name는 #value개의 사과를 가지고 있습니다.
]
```

### Break 및 continue

루프 내에서 `break` 및 `continue` 명령을 사용할 수 있습니다. `break`는 루프를 중단하고 밖으로 나갑니다. `continue`는 다음 루프 반복으로 이동합니다.

이 예제에서 차이점을 확인하세요:

```typ
#for letter in "abc nope" {
  if letter == " " {
    // 공백이 있으면 중지
    break
  }

  letter
}
```

```typ
#for letter in "abc nope" {
  if letter == " " {
    // 공백 건너뛰기
    continue
  }

  letter
}
```
