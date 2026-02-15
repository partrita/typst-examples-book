# 단어 수 세기 (Counting words)

## Wordometr

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count

이 문서에는 총 #total-words 개의 단어가 있습니다.

#word-count(total => [
  이 블록의 단어 수는 #total.words 개이고, 
  글자 수는 #total.characters 개입니다.
])
```

### 요소 제외하기
이름(예: `"caption"`), 함수(예: `figure.caption`), where-선택자(예: `raw.where(block: true)`), 또는 `레이블`(예: `<no-wc>`)을 사용하여 단어 계산에서 특정 요소를 제외할 수 있습니다.

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count.with(exclude: (heading.where(level: 1), strike))

= 이 제목은 수치에 포함되지 않습니다
== 하지만 저는 포함됩니다!

이 문서에는 #strike[(저를 제외하고)] 총 #total-words 개의 단어가 있습니다.

#word-count(total => [
  레이블을 사용하여 요소를 제외할 수도 있습니다.
  #[이 문장을 제외하고 #total-words 개였습니다!] <no-wc>
], exclude: <no-wc>)
```
