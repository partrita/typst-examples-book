# 글꼴 (Fonts)
## 수학 글꼴 설정
**중요:** 수학 글꼴로 설정하려는 글꼴은 필요한 수학 기호를 _포함하고 있어야_ 합니다. 그것은 수학이 포함된 특수 글꼴이어야 합니다. 그렇지 않으면 _오류_가 발생할 가능성이 매우 높습니다(`fallback: false`로 설정하고 `typst fonts`를 확인하여 글꼴을 디버그하세요).

```typ
#show math.equation: set text(font: "Fira Math", fallback: false)

$
emptyset \

integral_a^b sum (A + B)/C dif x \
$
```
