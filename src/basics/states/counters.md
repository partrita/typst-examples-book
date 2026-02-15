# 카운터 (Counters)
<div class="warning">이 섹션은 완전하지 않을 수 있으며 최신 Typst 버전에 맞춰 충분히 업데이트되지 않았을 수 있습니다. 모든 기여를 환영합니다!</div>

카운터는 특정 유형의 요소의 개수를 _세는_ 특수한 상태입니다.
상태와 마찬가지로 식별자 문자열을 사용하여 직접 만들 수 있습니다.

_중요:_ 요소의 카운터를 활성화하려면 해당 요소에 _번호 매기기(numbering)를 설정_해야 합니다.

## 상태 메서드
카운터는 상태의 일종이므로 상태가 할 수 있는 모든 것을 할 수 있습니다. 특히 `context`와 관련된 모든 사항이 그대로 적용됩니다.

```typ
#set heading(numbering: "1.")

= 배경
#counter(heading).update(3)
#counter(heading).update(n => n * 2)

== 분석
현재 제목 번호: #context counter(heading).get()

패턴을 사용해 예쁘게 렌더링할 수도 있습니다: #context counter(heading).display("I: 1.")

또는 현재 설정된 스타일을 사용합니다: #context counter(heading).display()

이는 현재 설정된 스타일에 따라 달라집니다:

#set heading(numbering: ":1:1:")
#context counter(heading).display()
```

몇 가지 예제를 더 보겠습니다. 매우 간단하므로 별도의 설명은 필요 없을 것 같네요. `:)`

```typ
#let mine = counter("mycounter")
#context mine.display()

#mine.step()
#context mine.display()

#mine.update(c => c * 3)
#context mine.display()
```

카운터는 기본적으로 _현재 값과 최종 값을 모두_ 표시하는 기능을 지원합니다. `both: true` 옵션이 필요합니다:

```typ
#set heading(numbering: "1.")

= 서론
내용이 들어갑니다.

#context counter(heading).display(both: true) \
#context counter(heading).display("1 / 1", both: true) \
#context counter(heading).display(
  (num, max) => [#num / #max],
   both: true
)

= 배경
현재 값은 다음과 같습니다: #context counter(heading).display()
```

## Step

매우 쉽습니다. 카운터의 경우 `step`을 사용하여 값을 증가시킬 수 있습니다. `update`와 동일한 방식으로 작동합니다.
```typ
#set heading(numbering: "1.")

= 서론
#context counter(heading).step()

= 분석
3.1은 건너뜁시다.
#context counter(heading).step(level: 2)

== 분석
현재 위치: #context counter(heading).display()
```

## 함수에서 카운터 사용하기:
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
