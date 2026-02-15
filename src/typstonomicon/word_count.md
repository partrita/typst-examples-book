# 단어 수 세기 (Word count)

<div class="warning">이 장은 이제 더 이상 권장되지 않습니다(deprecated). 곧 제거될 예정입니다.</div>

## 권장되는 해결책

`wordometr` [패키지](https://github.com/Jollywatt/typst-wordometer)를 사용하세요:

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count

이 문서에는 총 #total-words 개의 단어가 있습니다.

#word-count(total => [
  이 블록의 단어 수는 #total.words 개이고, 
  글자 수는 #total.characters 개입니다.
])
```

## 문서의 *모든* 단어 세기
```typ
// 원저자: laurmaedje
#let words = counter("words")
#show regex("\p{L}+"): it => it + words.step()

== 제목
#lorem(50)

=== 강조된 장
#strong(lorem(25))

// 주석은 무시됩니다

#align(right)[(#context words.display() 단어)]
```

## 특정 요소만 세고 나머지는 무시하기

```typ
// 원저자: jollywatt
#let count-words(it) = {
    let fn = repr(it.func())
    if fn == "sequence" { it.children.map(count-words).sum() }
    else if fn == "text" { it.text.split().len() }
    else if fn in ("styled") { count-words(it.child) }
    else if fn in ("highlight", "item", "strong", "link") { count-words(it.body) }
    else if fn in ("footnote", "heading", "equation") { 0 }
    else { 0 }
}

#show: rest => {
    let n = count-words(rest)
    rest + align(right, [(#n 단어)])
}

== 제목 (포함되지 않아야 함)
#lorem(50)

=== 강조된 장
#strong(lorem(25)) // 이것도 세어집니다!
```
