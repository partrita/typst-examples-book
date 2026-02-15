# 첫 줄 들여쓰기 (First line indent)

[공식 문서](https://typst.app/docs/reference/model/par/#parameters-first-line-indent)

텍스트 서식 지정에서 매우 일반적인 요구 사항 중 하나는 모든 단락의 첫 줄에 들여쓰기를 추가하는 것입니다. 일부 언어나 관습에서는 이를 필크로우(pilcrow, ¶) 또는 "빨간 선"이라고 부르기도 합니다.

기본적으로 Typst는 첫 번째 단락(또는 제목 다음에 오는 단락)을 _제외한_ 모든 단락에 들여쓰기를 적용합니다. 이를 변경하려면 `(all: true)`를 사용하세요:

```typ
#set block(spacing: 1.2em)
#set par(
  first-line-indent: 1.5em,
  spacing: 0.65em,
)

첫 번째 단락은 들여쓰기의 
영향을 받지 않습니다.

하지만 두 번째 단락은 영향을 받습니다.

#line(length: 100%)

#set par(first-line-indent: (
  amount: 1.5em,
  all: true,
))

이제 모든 단락이 첫 줄 
들여쓰기의 영향을 받습니다.

첫 번째 단락조차도요.
```
