# 페이지 설정 (Page setup)

> [공식 페이지 설정 가이드](https://typst.app/docs/guides/page-setup-guide/)를 참조하세요.


```typ
#set page(
  width: 3cm,
  margin: (x: 0cm),
)

#for i in range(3) {
  box(square(width: 1cm))
}
```

```typ
#set page(columns: 2, height: 4.8cm)
기후 변화는 우리 시대의 가장 시급한 문제 중 
하나로, 전 세계의 지역 사회, 생태계 및 
경제를 황폐화할 잠재력을 가지고 있습니다. 
우리는 탄소 배출을 줄이고 급격히 변화하는 
기후의 영향을 완화하기 위해 긴급한 조치를 
취해야 한다는 것이 분명합니다.
```

```typ
#set page(fill: rgb("444352"))
#set text(fill: rgb("fdfdfd"))
*다크 모드가 활성화되었습니다.*
```

```typ
#set par(justify: true)
#set page(
  margin: (top: 32pt, bottom: 20pt),
  header: [
    #set text(8pt)
    #smallcaps[Typst Academcy]
    #h(1fr) _연습 문제 시트 3_
  ],
)

#lorem(19)
```

```typ
#set page(foreground: text(24pt)[🥸])

리뷰어 2는 우리의 접근 방식을 이해하지 
못했다는 이유로 우리 논문에 
"약한 거절(Weak Reject)"을 표시했습니다...
```
