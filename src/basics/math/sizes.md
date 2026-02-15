# 위치 및 크기 (Location and sizes)

우리는 이미 디스플레이 수식과 인라인 수식에 대해 이야기했습니다.
이들은 정렬과 간격뿐만 아니라 크기와 스타일에서도 차이가 납니다:

```typ
인라인: $a/(b + 1/c), sum_(n=0)^3 x_n$

$
a/(b + 1/c), sum_(n=0)^3 x_n
$
```

현재 환경의 크기와 스타일은 수학 크기(Math Size)로 설명됩니다. [참조](https://typst.app/docs/reference/math/sizes)를 확인하세요.

네 가지 크기가 있습니다:

- 디스플레이 수식 크기 (`display`)
- 인라인 수식 크기 (`inline`)
- 스크립트 수식 크기 (`script`)
- 하위/상위 스크립트 수식 크기 (`sscript`)

분수, 스크립트 또는 지수에서 항목이 사용될 때마다 "몇 단계 아래"로 이동하여 더 작아집니다. `sscript`는 그 이상 줄어들지 않습니다:

```typ
$
"display:" 1/("inline:" a + 1/("script:" b + 1/("sscript:" c + 1/("sscript:" d + 1/("sscript:" e + 1/f)))))
$
```

## 수동으로 크기 설정하기

해당 명령어를 사용하면 됩니다:

```typ
인라인: $sum_0^oo e^x^a$\
극한이 있는 인라인: $limits(sum)_0^oo e^x^a$\
인라인이지만 디스플레이처럼 표시: $display(sum_0^oo e^x^a)$
```
