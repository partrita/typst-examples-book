# 특수 기호

> _중요:_ 저는 특수 기호에 익숙하지 않으므로, 추가나 수정 제안을 주시면 감사하겠습니다.

Typst는 _유니코드_를 훌륭하게 지원합니다. 이는 _특수 기호_도 지원한다는 의미입니다. 이것들은 조판에 매우 유용할 수 있습니다.

대부분의 경우, 이러한 기호를 직접 자주 사용해서는 안 됩니다. 가능하다면, show 규칙과 함께 사용하세요 (예를 들어, 모든 `-th`를 줄 바꿈 없는 하이픈인 `\u{2011}th`로 바꾸기).

## 줄 바꿈 없는 기호

줄 바꿈 없는 기호는 단어/구가 분리되지 않도록 보장할 수 있습니다. Typst는 그것들을 전체로 배치하려고 시도할 것입니다.

### 줄 바꿈 없는 공백

> _중요:_ 이것은 공백 기호이므로, 복사-붙여넣기는 도움이 되지 않습니다.
> Typst는 그것을 소스 코드가 편집기에서 더 보기 좋게 하기 위해 사용한 일반적인 공백 기호로 볼 것입니다. 다시 말해, 그것을 _기본 공백으로_ 해석할 것입니다.

이것은 자주 사용해서는 안 되는 기호이지만(대신 Typst 상자를 사용하세요), 줄 바꿈 없는 기호가 어떻게 작동하는지 보여주는 좋은 예입니다:

```typ
#set page(width: 9em)

// Cruel과 world가 분리되었습니다.
// 이것이 나눌 수 없는 구문이라고 상상해 보세요, 어떻게 해야 할까요?
Hello cruel world

// 특수 공백으로 연결해 봅시다!

// 일반 공백은 허용되지 않으므로, 세미콜론을 사용하거나...
Hello cruel#sym.space.nobreak;world

// ...괄호를 사용하거나...
Hello cruel#(sym.space.nobreak)world

// ...유니코드 코드를 사용하세요
Hello cruel\u{00a0}world

// 음, 같은 효과를 얻으려면 상자를 사용하는 것을 추천합니다:
Hello #box[cruel world]
```

### 줄 바꿈 없는 하이픈

```typ
#set page(width: 8em)

This is an $i$-th element.

This is an $i$\u{2011}th element.

// 가장 좋은 방법은 다음과 같습니다
#show "-th": "\u{2011}th"

This is an $i$-th element.
```

## 연결자와 구분자

### 단어 연결자

초기에는, 단어 연결자는 이 위치에서 줄 바꿈이 일어나지 않아야 함을 나타냅니다. 또한 너비가 0인 기호(보이지 않음)이므로, 공백 제거용으로 사용할 수 있습니다:

```typ
#set page(width: 9em)
#set text(hyphenate: true)

Thisisawordthathastobreak

// 조심하세요, 이제 줄 바꿈이 전혀 없습니다!
Thisi#sym.wj;sawordthathastobreak

// `physica` 패키지의 코드
// 여기서 단어 연결자는 추가 공백을 피하기 위해 사용됩니다
#let just-hbar = move(dy: -0.08em, strike(offset: -0.55em, extent: -0.05em, sym.planck))
#let hbar = (sym.wj, just-hbar, sym.wj).join()

$ a #just-hbar b, a hbar b$
```

### 너비 없는 공백

단어 연결자와 유사하지만, 이것은 _공백_입니다. 단어 분리를 막지 않습니다. 반대로, 하이픈 없이 단어를 분리합니다!

```typ
#set page(width: 9em)
#set text(hyphenate: true)

// 안에 공백이 있습니다!
Thisisa#sym.zws;word

// 조심하세요, 이제 하이픈이 전혀 없습니다!
Thisisawo#sym.zws;rdthathastobreak
```
