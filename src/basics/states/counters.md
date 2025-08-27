# 카운터
<div class="warning">이 섹션은 최신 Typst 버전에 대해 완전히 완전하거나 업데이트되지 않았을 수 있습니다. 어떤 기여든 매우 환영합니다!.</div>

카운터는 어떤 타입의 요소를 _세는_ 특별한 상태입니다.
상태와 마찬가지로, 식별자 문자열로 자신만의 카운터를 만들 수 있습니다.

_중요:_ 요소의 카운터를 시작하려면, _번호 매기기를 설정해야 합니다_.

## 상태 메소드
카운터는 상태이므로, 상태가 할 수 있는 모든 것을 할 수 있습니다. 특히, `context`에 대한 모든 것이 여전히 적용됩니다.

```typ
#set heading(numbering: "1.")

= 배경
#counter(heading).update(3)
#counter(heading).update(n => n * 2)

== 분석
현재 제목 번호: #context counter(heading).get().

임의의 번호 매기기 패턴으로 아름답게 렌더링할 수 있는 특수 메소드로 표시할 수도 있습니다: #context counter(heading).display("I: 1.").

또는 현재 표시 스타일 사용: #context counter(heading).display()

현재 설정된 스타일에 따라 다릅니다:

#set heading(numbering: ":1:1:")
#context counter(heading).display()
```

자, 여기 몇 가지 예제가 더 있습니다. 매우 간단하므로, 주석이 필요 없기를 바랍니다. `:)`

```typ
#let mine = counter("mycounter")
#context mine.display()

#mine.step()
#context mine.display()

#mine.update(c => c * 3)
#context mine.display()
```

카운터는 또한 _현재 값과 최종 값 모두_를 즉시 표시하는 것을 지원하며, 이를 위해서는 `both: true` 옵션이 필요합니다:

```typ
#set heading(numbering: "1.")

= 서론
여기에 텍스트.

#context counter(heading).display(both: true) \
#context counter(heading).display("1 of 1", both: true) \
#context counter(heading).display(
  (num, max) => [#num of #max],
   both: true
)

= 배경
현재 값은: #context counter(heading).display()
```

## 단계

매우 쉽습니다. 카운터의 경우 `step`을 사용하여 값을 증가시킬 수 있습니다. `update`와 동일하게 작동합니다.
```typ
#set heading(numbering: "1.")

= 서론
#context counter(heading).step()

= 분석
3.1을 건너뜁시다.
#context counter(heading).step(level: 2)

== 분석
#context counter(heading).display()에서.
```

## 함수에서 카운터를 사용할 수 있습니다:
```typ
#let c = counter("theorem")
#let theorem(it) = block[
  #c.step()
  *정리 #context c.display():*
  #it
]

#theorem[$1 = 1$]
#theorem[$2 < 3$]
```
