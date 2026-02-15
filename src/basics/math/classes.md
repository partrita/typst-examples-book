# 클래스 (Classes)

> [공식 문서](https://typst.app/docs/reference/math/class/)를 참조하세요.

각 수학 기호는 고유한 "클래스", 즉 동작 방식을 가지고 있습니다. 이것이 기호들이 서로 다르게 배치되는 주요 이유 중 하나입니다.

## 클래스 종류

```typ
$
a b c\
a class("normal", b) c\
a class("punctuation", b) c\
a class("opening", b) c\
a lr(b c]) c\
a lr(class("opening", b) c ]) c\ // 수직으로 이동된 것에 주목하세요.
a class("closing", b) c\
a class("fence", b) c\
a class("large", b) c\
a class("relation", b) c\
a class("unary", b) c\
a class("binary", b) c\
a class("vary", b) c\
$
```

## 기호의 클래스 설정하기

```typ
기본값:

$square circle square$

`#h(0)` 사용:

$square #h(0pt) circle #h(0pt) square$

`math.class` 사용:

#show math.circle: math.class.with("normal")
$square circle square$
```
