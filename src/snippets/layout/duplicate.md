# 콘텐츠 복제

<div class="warning">
    이 구현은 레이블 및 유사한 것들을 망칠 수 있습니다.
    복잡한 경우 아래의 것을 참조하십시오.
</div>
```typ
#set page(paper: "a4", flipped: true)
#show: body => grid(
  columns: (1fr, 1fr),
  column-gutter: 1cm,
  body, body,
)
#lorem(200)
```

## 고급
```typ
/// 저자: frozolotl
#set page(paper: "a4", flipped: true)
#set heading(numbering: "1.1")
#show ref: it => {
  if it.element != none {
    it
  } else {
    let targets = query(it.target)
    if targets.len() == 2 {
      let target = targets.first()
      if target.func() == heading {
        let num = numbering(target.numbering, ..counter(heading).at(target.location()))
        [#target.supplement #num]
      } else if target.func() == figure {
        let num = numbering(target.numbering, ..target.counter.at(target.location()))
        [#target.supplement #num]
      } else {
        it
      }
    } else {
      it
    }
  }
}
#show link: it => context {
  let dest = query(it.dest)
  if dest.len() == 2 {
    link(dest.first().location(), it.body)
  } else {
    it
  }
}
#show: body => context grid(
  columns: (1fr, 1fr),
  column-gutter: 1cm,
  body,
  {
    let reset-counter(kind) = counter(kind).update(counter(kind).get())
    reset-counter(heading)
    reset-counter(figure.where(kind: image))
    reset-counter(figure.where(kind: raw))
    set heading(outlined: false)
    set figure(outlined: false)
    body
  },
)

#outline()

= Foo <foo>
@foo 및 @foobar를 참조하십시오.

#figure(rect[이것은 이미지입니다], caption: [Foobar], kind: raw) <foobar>

== Bar
== Baz
#link(<foo>)[Foo를 방문하려면 클릭하세요]
```
