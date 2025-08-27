# 특수 문서
## 서명란
```typ
#block(width: 150pt)[
  #line(length: 100%)
  #align(center)[서명]
]
```

## 프레젠테이션
[polylux](../../packages/)를 참조하세요.


## 양식
### 플레이스홀더가 있는 양식
```typ
#grid(
  columns: 2,
  rows: 4,
  gutter: 1em,

  [학생:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [교사:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [ID:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [학교:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
)
```

### 대화형
> 프레젠테이션 대화형 양식이 곧 제공됩니다! 현재 @tinger가 열심히 작업 중입니다.