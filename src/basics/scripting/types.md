# 타입, 파트 I
Typst의 각 값에는 타입이 있습니다. 지정할 필요는 없지만 중요합니다.

## 콘텐츠 (`content`)
> [참조 링크](https://typst.app/docs/reference/foundations/content/).

이미 보았습니다. 문서에 표시되는 것을 나타내는 타입입니다.
```typ
#let c = [이것은 _콘텐츠_입니다!]

// c의 타입 확인
#(type(c) == content)

#c

// repr은 값의 "내부 표현"을 제공합니다
#repr(c)
```

**중요:** _콘텐츠_는 *무엇이든* 포함할 수 있으므로 _콘텐츠_를 _일반 텍스트_로 변환하는 것은 매우 어렵습니다! 따라서 변수에 콘텐츠를 전달하고 저장할 때 주의하세요.

## 없음 (`none`)
아무것도 없습니다. 다른 언어에서는 `null`로 알려져 있습니다. 표시되지 않으며 빈 콘텐츠로 변환됩니다.
```typ
#none
#repr(none)
```

## 문자열 (`str`)
> [참조 링크](https://typst.app/docs/reference/foundations/str/).

문자열은 서식 없는 일반 텍스트만 포함합니다. 그냥 일부 문자입니다. 이를 통해 문자로 작업할 수 있습니다:
```typ
#let s = "긴 문자열. 이스케이프 문장이 있을 수 있습니다: \n,
 줄 바꿈, 그리고 유니코드 코드도: \u{1251}"
#s \
#type(s) \
`repr`: #repr(s)

#let s = "다른 작은 문자열"
#s.replace("a", sym.alpha) \
#s.split(" ") // 공백으로 분리
```

이 타입의 생성자를 사용하여 다른 타입을 문자열 표현으로 변환할 수 있습니다(예: 숫자를 문자열로 변환):

```typ
#str(5) // 문자열, 문자열로 작업할 수 있음
```

## 불리언 (`bool`)
> [참조 링크](https://typst.app/docs/reference/foundations/bool/).

참/거짓. `if` 및 기타 여러 곳에서 사용됩니다.
```typ
#let b = false
#b \
#repr(b) \
#(true and not true or true) = #((true and (not true)) or true) \
#if (4 > 3) {
  "4는 3보다 큽니다"
}
```

## 정수 (`int`)
> [참조 링크](https://typst.app/docs/reference/foundations/int/).

정수.

숫자는 0 다음에 x, o 또는 b를 붙여 16진수, 8진수 또는 2진수로 지정할 수도 있습니다.

```typ
#let n = 5
#n \
#(n += 1) \
#n \
#calc.pow(2, n) \
#type(n) \
#repr(n)
```

```typ
#(1 + 2) \
#(2 - 5) \
#(3 + 4 < 8)
```

```typ
#0xff \
#0o10 \
#0b1001
```

이 타입의 생성자를 사용하여 값을 정수로 변환할 수 있습니다(예: 문자열을 정수로 변환).

```typ
#int(false) \
#int(true) \
#int(2.7) \
#(int("27") + int("4"))
```

## 부동 소수점 (`float`)
> [참조 링크](https://typst.app/docs/reference/foundations/float/).

정수와 동일하게 작동하지만 부동 소수점 숫자를 저장할 수 있습니다.
그러나 정밀도가 손실될 수 있습니다.

```typ
#let n = 5.0

// 부동 소수점과 정수를 혼합할 수 있으며,
// 암시적으로 변환됩니다
#(n += 1) \
#calc.pow(2, n) \
#(0.2 + 0.1) \
#type(n) 
```

```typ
#3.14 \
#1e4 \
#(10 / 4)
```

이 타입의 생성자를 사용하여 값을 부동 소수점으로 변환할 수 있습니다(예: 문자열을 부동 소수점으로 변환).

```typ
#float(40%) \
#float("2.7") \
#float("1e5")
```
