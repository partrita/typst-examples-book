# 조건문 및 반복문 (Conditions & loops)

## 조건문 (Conditions)
> [공식 문서](https://typst.app/docs/reference/scripting/#conditionals)를 참조하세요.

Typst에서는 `if-else`문을 사용할 수 있습니다.
이는 특히 함수 본문 내부에서 인수 타입이나 다른 여러 상황에 따라 동작을 변경할 때 유용합니다.

```typ
#if 1 < 2 [
  이 내용이 보입니다.
] else [
  이 내용은 보이지 않습니다.
]
```

물론 `else`는 필수가 아닙니다:

```typ
#let a = 3

#if a < 4 {
  a = 5
}

#a
```

`else if`문도 사용할 수 있습니다:

```typ
#let a = 5

#if a < 4 {
  a = 5
} else if a < 6 {
  a = -3
}

#a
```

### 불리언 (Booleans)

`if, else if, else`는 스위치 값으로 _오직 불리언(boolean)_ 값만 받습니다.
[타입 섹션](./types.md#불리언-boolean-bool)에서 설명한 대로 불리언을 결합할 수 있습니다:

```typ
#let a = 5

#if (a > 1 and a <= 4) or a == 5 [
    `a`가 조건에 부합합니다.
]
```

### Set-if

Typst는 매우 유용한 명령인 `set if`를 지원합니다. 조건이 충족될 때만 set 규칙을 적용합니다. 이는 문서 전체나 함수 내부의 조건부 스타일링에 매우 유용할 수 있습니다:

```typ
#let draft = true

// 여기서 바로 조건 연산을 수행할 수 있습니다.
#set page(columns: 2, width: 20em, height: 10em) if not draft

// show 규칙 내부에서도 사용할 수 있습니다.
#show "TODO": set text(red, size: 2em) if draft

TODO: 실제 텍스트를 작성하세요.

#lorem(50)
```

## 반복문 (Loops)

> [공식 문서](https://typst.app/docs/reference/scripting/#loops)를 참조하세요.

반복문에는 `while`과 `for` 두 가지 종류가 있습니다. `while`은 조건이 충족되는 동안 본문을 반복합니다:

```typ
#let a = 3

#while a < 100 {
    a *= 2
    str(a)
    " "
}
```

`for`는 시퀀스의 모든 요소를 순회합니다. 시퀀스는 `array`, `string` 또는 `dictionary`(`for`는 딕셔너리의 _키-값 쌍_을 순회함)가 될 수 있습니다.

```typ
#for c in "ABC" [
  #c 는 글자입니다.
]
```

`a`부터 `b`까지의 모든 숫자를 순회하려면 `range(a, b+1)`을 사용하세요:

```typ
#let s = 0

#for i in range(3, 6) {
    s += i
    [숫자 #i 가 합계에 더해졌습니다. 현재 합계는 #s 입니다.]
}
```

`range`는 마지막 숫자를 제외하므로 위 코드는 다음과 동일합니다:

```typ
#let s = 0

#for i in (3, 4, 5) {
    s += i
    [숫자 #i 가 합계에 더해졌습니다. 현재 합계는 #s 입니다.]
}
```

```typ
#let people = (Alice: 3, Bob: 5)

#for (name, value) in people [
    #name 은 #value 개의 사과를 가지고 있습니다.
]
```

### Break 및 continue

반복문 내부에서 `break`와 `continue` 명령을 사용할 수 있습니다. `break`는 반복문을 중단하고 밖으로 나갑니다. `continue`는 다음 반복 회차로 건너뜁니다.

다음 예제에서 차이점을 확인해 보세요:

```typ
#for letter in "abc nope" {
  if letter == " " {
    // 공백이 있으면 중단
    break
  }

  letter
}
```

```typ
#for letter in "abc nope" {
  if letter == " " {
    // 공백은 건너뜀
    continue
  }

  letter
}
```
