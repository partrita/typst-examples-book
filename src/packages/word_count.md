# 단어 세기

## Wordometr

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count

이 문서에는 총 #total-words 단어가 있습니다.

#word-count(total => [
  이 블록의 단어 수는 #total.words 단어이고
  #total.characters 글자가 있습니다.
])
```

### 요소 제외
이름(예: `"caption"`), 함수(예: `figure.caption`), where-selector(예: `raw.where(block: true)`) 또는 `label`(예: `<no-wc>`)로 요소를 제외할 수 있습니다.

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count.with(exclude: (heading.where(level: 1), strike))

= 이 제목은 세지 않습니다
== 하지만 저는 셉니다!

이 문서에는 #strike[(나를 제외하고)] 총 #total-words 단어가 있습니다.

#word-count(total => [
  레이블로도 요소를 제외할 수 있습니다.
  #[이 문장을 제외하고 #total-words 단어였습니다!] <no-wc>
], exclude: <no-wc>)
```
