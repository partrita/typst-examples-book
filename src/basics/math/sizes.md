# 위치 및 크기

우리는 이미 디스플레이 및 인라인 수학에 대해 이야기했습니다.
정렬 및 간격뿐만 아니라 크기 및 스타일도 다릅니다:

```typ
인라인: $a/(b + 1/c), sum_(n=0)^3 x_n$

$
a/(b + 1/c), sum_(n=0)^3 x_n
$
```

현재 환경의 크기와 스타일은 수학 크기로 설명됩니다. [참조](https://typst.app/docs/reference/math/sizes)를 참조하세요.

네 가지 크기가 있습니다:

- 디스플레이 수학 크기 (`display`)
- 인라인 수학 크기 (`inline`)
- 스크립트 수학 크기 (`script`)
- 하위/상위 스크립트 수학 크기 (`sscript`)

분수, 스크립트 또는 지수에서 사용될 때마다 "레벨이 낮아져" 더 작아지고 더 "조잡해집니다". `sscript`는 더 이상 축소되지 않습니다:

```typ
$
"display:" 1/("inline:" a + 1/("script:" b + 1/("sscript:" c + 1/("sscript:" d + 1/("sscript:" e + 1/f)))))
$
```

## 수동으로 크기 설정

해당 명령을 사용하기만 하면 됩니다:

```typ
인라인: $sum_0^oo e^x^a$\
한계가 있는 인라인: $limits(sum)_0^oo e^x^a$\
인라인이지만 실제 디스플레이처럼: $display(sum_0^oo e^x^a)$
```
