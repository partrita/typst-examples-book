# 단어 수

<div class="warning">이 챕터는 이제 더 이상 사용되지 않습니다. 곧 제거될 예정입니다.</div>

## 권장 해결책

`wordometr` [패키지](https://github.com/Jollywatt/typst-wordometer)를 사용하세요:

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count

이 문서에는 총 #total-words 단어가 있습니다.

#word-count(total => [
  이 블록의 단어 수는 #total.words 단어이고
  #total.characters 글자가 있습니다.
])
```

## 문서의 _모든_ 단어 수 세기
```typ
// 원저자: laurmaedje
#let words = counter("words")
#show regex("\p{L}+"): it => it + words.step()

== 제목
#lorem(50)

=== 강력한 챕터
#strong(lorem(25))

// 주석은 무시합니다.

#align(right)[(#context words.display() 단어)]
```

## 일부 요소만 세고 다른 요소는 무시하기

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

== 제목 (세지 않아야 함)
#lorem(50)

=== 강력한 챕터
#strong(lorem(25)) // 이것도 셉니다!
```

## 블록의 단어 수 세기
```typ
// 원저자: laurmaedje
#let count(it) = {
  let words = state("words", 0)
  words.update(n => n + it.text.split().len())
  [#it #h(1fr) #text(10pt)[(#context words.get() 단어)]]
}

#show regex("\p{L}+"): count

#lorem(10)
```

## 블록의 단어 수 세기 (다른 구현)
```typ
// 원저자: laurmaedje
#let count(it) = {
  let words = state("words", 0)
  show regex("\p{L}+"): it => {
    words.step()
    it
  }
  [#it #h(1fr) #text(10pt)[(#context words.get() 단어)]]
}

#count(lorem(10))
```
