# 특수 문서 (Special documents)
## 서명란 (Signature places)
```typ
#block(width: 150pt)[
  #line(length: 100%)
  #align(center)[서명]
]
```

## 프레젠테이션
[polylux](../../packages/)를 참조하세요.


## 서식 (Forms)
### 자리가 있는 서식
```typ
#grid(
  columns: 2,
  rows: 4,
  gutter: 1em,

  [학생 이름:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [지도 교수:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [ID 번호:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [학교:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
)
```

### 대화형 (Interactive)
> 프레젠테이션용 대화형 서식이 추가될 예정입니다! 현재 @tinger가 집중적으로 작업 중입니다.
