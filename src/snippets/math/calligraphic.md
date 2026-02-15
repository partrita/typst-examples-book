# 서체(Calligraphic) 글자

```typ
#let scr(it) = math.class("normal", box({
  show math.equation: set text(stylistic-set: 1)
  $cal(it)$
}))


$ scr(A) scr(B) + scr(C), -scr(D) $
```

안타깝게도 현재 수학에서 `stylistic-set`을 그대로 사용하면 간격이 맞지 않는 문제가 발생합니다. 수학 엔진은 기본 글꼴인지 여부에 따라 문자의 간격을 결정하기 때문입니다. 하지만 단순히 "normal"로 설정하는 것만으로는 충분하지 않은데, 그렇게 하면 크기가 줄어들 수 있기 때문입니다. 그래서 이 스니펫은 다소 복잡한 방식(hacky)으로 구현되었습니다(아마도 Typstonomicon에 위치해야 할 수도 있지만, 내용이 충분히 길지는 않습니다).
