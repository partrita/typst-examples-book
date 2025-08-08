# 상태

<div class="warning">이 섹션은 최신 Typst 버전에 대해 완전히 완전하거나 업데이트되지 않았을 수 있습니다. 어떤 기여든 매우 환영합니다!.</div>

실용적인 것을 시작하기 전에, 일반적으로 상태를 이해하는 것이 중요합니다.

왜 우리가 그것들을 _필요_로 하는지에 대한 좋은 설명이 있습니다: [상태에 대한 공식 참조](https://typst.app/docs/reference/introspection/state/). 먼저 읽어보는 것을 강력히 권장합니다.

그래서 대신
```typ -norender
#let x = 0
#let compute(expr) = {
  // eval은 문자열을 Typst 코드로 평가합니다
  // 새 x 값을 계산하기 위해
  x = eval(
    expr.replace("x", str(x))
  )
  [새 값은 #x입니다.]
}

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")
```

**이것은 컴파일되지 않습니다:** 함수 외부의 변수는 읽기 전용이며 수정할 수 없습니다.

대신, 다음과 같이 작성해야 합니다.

```typ
#let s = state("x", 0)
#let compute(expr) = [
  // 이 함수로 x 현재 상태를 업데이트합니다
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  // 그리고 그것을 표시합니다
  새 값은 #context s.get()입니다.
]

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")

계산은 문서에서 _위치_한 순서대로 수행됩니다. 따라서 먼저 계산을 만들고 나중에 문서에 넣으면... 직접 확인하세요:

#let more = [
  #compute("x * 2") \
  #compute("x - 5")
]

#compute("10") \
#compute("x + 3") \
#more
```
## 컨텍스트 마법

그렇다면 이 마법의 `context s.get()`은 무엇을 의미할까요?

> [참조의 컨텍스트](https://typst.app/docs/reference/context/)

요약하자면, 코드(또는 마크업)의 어느 부분이 _외부 상태에 의존_할 수 있는지를 지정합니다. 이 컨텍스트 표현식은 하나의 객체로 묶여 레이아웃 단계에서 평가됩니다.

이는 "일반" 코드에서 `context` 내부에 있는 것을 보는 것이 불가능하다는 것을 의미합니다. 이것은 _문서에 넣은 후에만_ 알 수 있는 블랙박스입니다.

`context` 기능에 대해서는 나중에 논의할 것입니다.

## 상태 연산
### 새 상태 만들기
```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y

상태는 #context x.get() \ // 다음과 같음
#context [상태는 #y.get()입니다] \ // 다음과 같음
#context {"상태는" + str(y.get())}
```

### 업데이트

업데이트는 지침인 _콘텐츠_입니다. 이 지침은 컴파일러에게 문서의 이 위치에서 상태가 _업데이트되어야 함_을 알려줍니다.

```typ
#let x = state("x", 0)
#context x.get() \
#let _ = x.update(3)
// 아무 일도 일어나지 않음, `update`를 문서 흐름에 넣지 않음
#context x.get()

#repr(x.update(3)) // 이것이 그 콘텐츠가 어떻게 보이는지 \

#context x.update(3)
#context x.get() // 드디어!
```

여기서 우리는 _중요한 `context` 특성_ 중 하나를 볼 수 있습니다: 외부의 상태는 "보지만", 내부에서 어떻게 변하는지는 볼 수 없습니다:

```typ
#let x = state("x", 0)

#context {
  x.update(3)
  str(x.get())
}
```

### ID 충돌

_요약; **충돌하는 상태를 절대 허용하지 마세요.**_

<div class="warning">
상태는 ID로 설명되며, ID가 같으면 코드가 깨집니다.
</div>

따라서 여러 번 사용되는 함수나 루프를 작성하는 경우, _주의하세요_!

```typ
#let f(x) = {
  // 새 상태 반환…
  // …하지만 ID가 같습니다!
  // 그래서 항상 같은 상태가 될 것입니다!
  let y = state("x", 0)
  y.update(y => y + x)
  context y.get()
}

#let a = f(2)
#let b = f(3)

#a, #b \
#raw(repr(a) + "\n" + repr(b))
```

그러나 이것은 괜찮아 _보일 수 있습니다_:

```typ
// 코드의 위치가 다릅니다!
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y
```

하지만 사실, 그렇지 _않습니다_:

```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#context [#x.get(); #y.get()]

#x.update(3)

#context [#x.get(); #y.get()]
```
