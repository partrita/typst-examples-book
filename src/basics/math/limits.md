# 극한 설정 (Setting limits)

가끔 기본적으로 기호가 붙는 방식을 바꾸고 싶을 때가 있습니다.

## 극한 (Limits)
예를 들어, 많은 국가에서 정적분을 작성할 때 적분 기호 아래와 위에 극한을 씁니다.
이를 설정하려면 `limits` 함수를 사용하세요:

```typ
$
integral_a^b\
limits(integral)_a^b
$
```

`show` 규칙을 사용하여 이를 기본값으로 설정할 수 있습니다:

```typ
#show math.integral: math.limits

$
integral_a^b
$

이것은 인라인 수식입니다: $integral_a^b$
```

## 디스플레이 모드 전용

이 설정은 인라인 수식에도 영향을 준다는 점에 유의하세요. 디스플레이 수식에만 극한을 활성화하려면 `limits(inline: false)`를 사용하세요:

```typ
#show math.integral: math.limits.with(inline: false)

$
integral_a^b
$

이것은 인라인 수식입니다: $integral_a^b$.
```

물론, 다시 아래쪽 첨자로 옮기는 것도 가능합니다:

```typ
$
sum_a^b, scripts(sum)_a^b
$
```


## 연산 (Operations)

동일한 방식이 연산에도 적용됩니다. 기본적으로 연산 기호의 아래와 위에 붙습니다:

```typ
$a =_"보조정리 1에 의해" b, a scripts(=)_+ b$
```
