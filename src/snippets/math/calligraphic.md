# 캘리그래피 문자

```typ
#let scr(it) = math.class("normal", box({
  show math.equation: set text(stylistic-set: 1)
  $cal(it)$
}))


$ scr(A) scr(B) + scr(C), -scr(D) $
```

안타깝게도 현재 수학에 대한 `stylistic-set`만으로는 간격이 좋지 않습니다. 수학 엔진은 문자가 기본 글꼴인지 여부에 따라 올바르게 간격을 두어야 하는지 감지합니다. 그러나 단순히 "normal"로 만드는 것만으로는 충분하지 않습니다. 그러면 축소될 수 있기 때문입니다. 이것이 스니펫이 이처럼 해키한 이유입니다(아마도 Typstonomicon에 있어야 하지만 그렇게 크지는 않습니다).
