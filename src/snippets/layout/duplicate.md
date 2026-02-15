# 콘텐츠 복제 (Duplicate content)

<div class="warning">
    이 구현은 레이블 및 이와 유사한 요소들과 충돌할 수 있습니다.
    복잡한 사례의 경우 아래의 고급 버전을 참조하세요.
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

## 고급 버전 (Advanced)
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

= 푸 (Foo) <foo>
@foo 와 @foobar 를 참조하세요.

#figure(rect[이것은 이미지입니다], caption: [푸바 (Foobar)], kind: raw) <foobar>

== 바 (Bar)
== 바즈 (Baz)
#link(<foo>)[Foo 방문하려면 클릭]
```
