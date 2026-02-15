# 중첩된 목록에서 들여쓰기 제거

```typ
// author: fenjalien
#show enum.item: it => {
  if repr(it.body.func()) == "sequence" {
    let children = it.body.children
    let index = children.position(x => x.func() == enum.item)
    if index != none {
      enum.item({
        children.slice(0, index).join()
        set enum(indent: -1.2em) // 무한 재귀 show 규칙을 중지한다는 점에 유의하세요
        children.slice(index).join()
      })
    } else {
      it
    }
  } else {
    it
  }
}

arst
+ A
+ b
+ c
  + d
+ e
  + f
+ g
+ h
+ i
+ 
```
