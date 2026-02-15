# 특수 기호 (Special symbols)

> _중요:_ 저는 특수 기호에 능숙하지 않으므로, 추가나 수정 사항이 있다면 감사히 받겠습니다.

Typst는 _유니코드_ 를 아주 잘 지원합니다. 이는 _특수 기호_ 또한 지원함을 의미합니다. 조판에 매우 유용할 수 있습니다.

대부분의 경우 이러한 기호를 직접 자주 사용할 필요는 없습니다. 가능하다면 show 규칙을 사용하세요(예를 들어, 모든 `-th`를 줄 바꿈 방지 하이픈인 `\u{2011}th`로 교체).

## 줄 바꿈 방지 기호 (Non-breaking symbols)

줄 바꿈 방지 기호는 단어나 어구가 분리되지 않도록 보장합니다. Typst는 이를 하나의 덩어리로 처리하려고 노력할 것입니다.

### 줄 바꿈 방지 공백 (Non-breaking space)

> _중요:_ 이것은 공백 기호이므로 복사해서 붙여넣는 것으로는 효과가 없습니다.
> Typst는 이를 에디터에서 소스 코드를 보기 좋게 만들기 위해 사용한 일반적인 공백 기호로 간주할 것입니다. 즉, _기본 공백_으로 해석합니다.

이 기호는 자주 사용해서는 안 되는 기호이지만(대신 Typst의 박스를 사용하세요), 줄 바꿈 방지 기호가 어떻게 작동하는지 보여주는 좋은 예시입니다:

```typ
#set page(width: 9em)

// Cruel과 world가 분리됩니다.
// 이것이 분리되어서는 안 되는 어구라고 가정해 봅시다. 어떻게 해야 할까요?
Hello cruel world

// 특수 공백으로 연결해 봅시다!

// 일반적인 공백은 허용되지 않으므로 세미콜론을 사용하거나...
Hello cruel#sym.space.nobreak;world

// ...괄호를 사용하거나...
Hello cruel#(sym.space.nobreak)world

// ...유니코드 코드를 사용할 수 있습니다.
Hello cruel\u{00a0}world

// 동일한 효과를 얻기 위해 박스(box)를 사용하는 것을 권장합니다:
Hello #box[cruel world]
```

### 줄 바꿈 방지 하이픈 (Non-breaking hyphen)

```typ
#set page(width: 8em)

이것은 $i$-th 요소입니다.

이것은 $i$\u{2011}th 요소입니다.

// 가장 좋은 방법은 다음과 같습니다.
#show "-th": "\u{2011}th"

이것은 $i$-th 요소입니다.
```

## 커넥터 및 구분 기호 (Connectors and separators)

### 단어 결합자 (Word joiner)

기본적으로 단어 결합자는 이 위치에서 줄 바꿈이 발생하지 않아야 함을 나타냅니다. 또한 너비가 0인 기호(보이지 않음)이므로 공백을 제거하는 용도로 사용할 수 있습니다:

```typ
#set page(width: 9em)
#set text(hyphenate: true)

Thisisawordthathastobreak

// 주의하세요, 이제 줄 바꿈이 전혀 발생하지 않습니다!
Thisi#sym.wj;sawordthathastobreak

// `physica` 패키지의 코드
// 여기서 단어 결합자는 추가 공백을 피하기 위해 사용됩니다.
#let just-hbar = move(dy: -0.08em, strike(offset: -0.55em, extent: -0.05em, sym.planck))
#let hbar = (sym.wj, just-hbar, sym.wj).join()

$ a #just-hbar b, a hbar b$
```

### 너비가 0인 공백 (Zero width space)

단어 결합자와 비슷하지만, 이것은 _공백_ 입니다. 단어 분리를 방지하지는 않습니다. 반대로, 하이픈 없이 단어를 분리합니다!

```typ
#set page(width: 9em)
#set text(hyphenate: true)

// 내부에 공백이 있습니다!
Thisisa#sym.zws;word

// 주의하세요, 이제 하이픈이 전혀 나타나지 않습니다!
Thisisawo#sym.zws;rdthathastobreak
```
