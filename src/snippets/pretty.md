# 예쁜 것들
## 텍스트 왼쪽에 막대 설정
(인용 서식이라고도 함)

```typ
#let line-block = rect.with(fill: luma(240), stroke: (left: 0.25em))

+ #lorem(10) \
  #line-block[
    *해결책:* #lorem(10)

    $ a_(n+1)x^n = 2... $
  ]
```

## 상자 상단의 텍스트
```typ
// 저자: gaiajack
#let todo(body) = block(
  above: 2em, stroke: 0.5pt + red,
  width: 100%, inset: 14pt
)[
  #set text(font: "Noto Sans", fill: red)
  #place(
    top + left,
    dy: -6pt - 14pt, // 블록의 인셋 고려
    dx: 6pt - 14pt,
    block(fill: white, inset: 2pt)[*DRAFT*]
  )
  #body
]

#todo(lorem(100))
```

## 책 장식

```typ
// 저자: thevec

#let parSepOrnament = [\ \
  #h(1fr) $#line(start:(0em,-.15em), end:(12em,-.15em), stroke: (cap: "round", paint:gradient.linear(white,black,white))) #move(dx:.5em,dy:0em,"🙠")#text(15pt)[🙣] #h(0.4em) #move(dy:-0.25em,text(12pt)[✢]) #h(0.4em) #text(15pt)[🙡]#move(dx:-.5em,dy:0em,"🙢") #line(start:(0em,-.15em), end:(12em,-.15em), stroke: (cap: "round", paint:gradient.linear(white,black,white)))$ #h(1fr)
 \\];

#lorem(30)
#parSepOrnament
#lorem(30)
```