# 글꼴
## 수학 글꼴 설정
**중요:** 수학에 설정하려는 글꼴에는 필요한 수학 기호가 _포함되어야_ 합니다. 수학이 포함된 특수 글꼴이어야 합니다. 그렇지 않으면 _오류_가 발생할 가능성이 매우 높습니다(글꼴을 디버깅하려면 `fallback: false`를 설정하고 `typst fonts`를 확인하는 것을 잊지 마세요).

```typ
#show math.equation: set text(font: "Fira Math", fallback: false)

$
emptyset \

integral_a^b sum (A + B)/C dif x \
$
```