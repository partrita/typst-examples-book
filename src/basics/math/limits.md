# 한계 설정

때로는 기본 첨부 방식이 어떻게 작동하는지 변경하고 싶을 때가 있습니다.

## 한계
예를 들어, 많은 국가에서는 아래와 위에 한계가 있는 정적분을 작성하는 것이 일반적입니다.
이를 설정하려면 `limits` 함수를 사용합니다:

```typ
$
integral_a^b\
limits(integral)_a^b
$
```

`show` 규칙을 사용하여 기본적으로 설정할 수 있습니다:

```typ
#show math.integral: math.limits

$
integral_a^b
$

이것은 인라인 방정식입니다: $integral_a^b$
```

## 디스플레이 모드만

이것은 인라인 방정식에도 영향을 미칩니다. 디스플레이 수학에만 한계를 활성화하려면 `limits(inline: false)`를 사용하세요:

```typ
#show math.integral: math.limits.with(inline: false)

$
integral_a^b
$

이것은 인라인 방정식입니다: $integral_a^b$.
```

물론, 하단 첨부 파일로 다시 이동할 수 있습니다:

```typ
$
sum_a^b, scripts(sum)_a^b
$
```


## 연산

연산에도 동일한 방식이 적용됩니다. 기본적으로 하단과 상단에 첨부됩니다:

```typ
$a =_"정리 1에 의해" b, a scripts(=)_+ b$
```
