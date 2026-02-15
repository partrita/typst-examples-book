# 상태 (States)

<div class="warning">이 섹션은 완전하지 않을 수 있으며 최신 Typst 버전에 맞춰 충분히 업데이트되지 않았을 수 있습니다. 모든 기여를 환영합니다!</div>

실용적인 내용을 시작하기 전에, 일반적인 상태(state)의 개념을 이해하는 것이 중요합니다.

여기 왜 상태가 _필요한지_에 대한 좋은 설명이 있습니다: [상태에 관한 공식 참조 문서](https://typst.app/docs/reference/introspection/state/). 먼저 읽어보시는 것을 강력히 추천합니다.

다음과 같이 작성하는 대신:
```typ -norender
#let x = 0
#let compute(expr) = {
  // eval은 문자열을 Typst 코드로 해석하여
  // 새로운 x 값을 계산합니다.
  x = eval(
    expr.replace("x", str(x))
  )
  [새로운 값은 #x 입니다.]
}

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")
```

**이 코드는 컴파일되지 않습니다:** 함수 외부의 변수는 읽기 전용이며 수정할 수 없습니다.

대신 다음과 같이 작성해야 합니다:

```typ
#let s = state("x", 0)
#let compute(expr) = [
  // 이 함수로 x의 현재 상태를 업데이트합니다.
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  // 그리고 이를 표시합니다.
  새로운 값은 #context s.get() 입니다.
]

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")

계산은 문서에 _위치한 순서_대로 이루어집니다. 따라서 계산을 먼저 만들었지만 문서의 나중에 배치한다면... 직접 확인해 보세요:

#let more = [
  #compute("x * 2") \
  #compute("x - 5")
]

#compute("10") \
#compute("x + 3") \
#more
```
## 컨텍스트의 마법 (Context magic)

그렇다면 이 마법 같은 `context s.get()`은 무엇을 의미할까요?

> [참조 문서의 컨텍스트(Context)](https://typst.app/docs/reference/context/)

요약하자면, 코드(또는 마크업)의 어느 부분이 _외부 상태에 의존할 수 있는지_를 지정합니다. 이 컨텍스트 표현식은 하나의 객체로 묶여 레이아웃 단계에서 평가됩니다.

즉, "일반" 코드에서는 `context` 내부에 무엇이 있는지 들여다볼 수 없습니다. 이것은 _문서에 배치된 후에만_ 그 내용을 알 수 있는 블랙박스와 같습니다.

`context` 기능에 대해서는 나중에 더 자세히 다루겠습니다.

## 상태 연산
### 새로운 상태 생성
```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y

상태는 #context x.get() 입니다. \ // 다음과 동일합니다.
#context [상태는 #y.get() 입니다.] \ // 다음과 동일합니다.
#context {"상태는 " + str(y.get()) + " 입니다."}
```

### 업데이트 (Update)

업데이트는 하나의 지침인 _콘텐츠_입니다. 이 지침은 컴파일러에게 문서의 이 위치에서 상태가 _업데이트되어야 함_을 알려줍니다.

```typ
#let x = state("x", 0)
#context x.get() \
#let _ = x.update(3)
// 아무 일도 일어나지 않습니다. `update`를 문서 흐름에 넣지 않았기 때문입니다.
#context x.get()

#repr(x.update(3)) // 해당 콘텐츠가 어떻게 보이는지 확인해 보세요. \

#context x.update(3)
#context x.get() // 드디어 업데이트되었습니다!
```

여기서 _`context`의 중요한 특징_ 중 하나를 볼 수 있습니다: 컨텍스트는 외부의 상태를 "볼" 수 있지만, 컨텍스트 내부에서 상태가 어떻게 변하는지는 볼 수 없습니다.

```typ
#let x = state("x", 0)

#context {
  x.update(3)
  str(x.get())
}
```

### ID 충돌

_요약: **절대로 상태 ID가 충돌하게 하지 마세요.**_

<div class="warning">
상태는 ID로 식별되며, ID가 같으면 코드가 제대로 작동하지 않습니다.
</div>

따라서 여러 번 사용되는 함수나 루프를 작성할 때는 _주의_해야 합니다!

```typ
#let f(x) = {
  // 새로운 상태를 반환하지만...
  // ...ID가 같습니다!
  // 따라서 항상 동일한 상태가 됩니다!
  let y = state("x", 0)
  y.update(y => y + x)
  context y.get()
}

#let a = f(2)
#let b = f(3)

#a, #b \
#raw(repr(a) + "\n" + repr(b))
```

하지만 다음과 같은 경우는 괜찮아 _보일 수_ 있습니다:

```typ
// 코드에서의 위치가 다릅니다!
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y
```

그러나 사실은 _괜찮지 않습니다_:

```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#context [#x.get(); #y.get()]

#x.update(3)

#context [#x.get(); #y.get()]
```
