# Query
<div class="warning">This section is outdated. It may be still useful, but it is strongly recommended to study new context system (using the reference).</div>

> Link [there](https://typst.app/docs/reference/introspection/query/)

Query is a thing that allows you getting location by _selector_ (this is the same thing we used in show rules).

That enables "time travel", getting information about document from its parts and so on. _That is a way to violate Typst's purity._

It is currently one of the _the darkest magics currently existing in Typst_. It gives you great powers, but with great power comes great responsibility.

## Time travel

```typ
#let s = state("x", 0)
#let compute(expr) = [
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  New value is #s.display().
]

Value at `<here>` is
#context s.at(
  query(<here>)
    .first()
    .location()
)

#compute("10") \
#compute("x + 3") \
*Here.* <here> \
#compute("x * 2") \
#compute("x - 5")
```

## Getting nearest chapter
```typ
#set page(header: context {
  let elems = query(
    selector(heading).before(here()),
    here(),
  )
  let academy = smallcaps[
    Typst Academy
  ]
  if elems == () {
    align(right, academy)
  } else {
    let body = elems.last().body
    academy + h(1fr) + emph(body)
  }
})

= Introduction
#lorem(23)

= Background
#lorem(30)

= Analysis
#lorem(15)
```
