# 클래스

> [공식 문서](https://typst.app/docs/reference/math/class/) 참조

각 수학 기호에는 고유한 "클래스", 즉 동작 방식이 있습니다. 이것이 다르게 레이아웃되는 주된 이유 중 하나입니다.

## 클래스

```typ
$
a b c\
a class("normal", b) c\
a class("punctuation", b) c\
a class("opening", b) c\
a lr(b c]) c\
a lr(class("opening", b) c ]) c\ // 수직으로 이동된 것을 확인하세요
a class("closing", b) c\
a class("fence", b) c\
a class("large", b) c\
a class("relation", b) c\
a class("unary", b) c\
a class("binary", b) c\
a class("vary", b) c\
$
```

## 기호에 대한 클래스 설정

```typ
기본값:

$square circle square$

`#h(0)` 사용:

$square #h(0pt) circle #h(0pt) square$

`math.class` 사용:

#show math.circle: math.class.with("normal")
$square circle square$
```
