# 가짜 이탤릭 및 텍스트 그림자

## 기울이기

```typ
// 저자: Enivex
#set page(width: 21cm, height: 3cm)
#set text(size:25pt)
#let skew(angle,vscale: 1,body) = {
  let (a,b,c,d)= (1,vscale*calc.tan(angle),0,vscale)
  let E = (a + d)/2
  let F = (a - d)/2
  let G = (b + c)/2
  let H = (c - b)/2
  let Q = calc.sqrt(E*E + H*H)
  let R = calc.sqrt(F*F + G*G)
  let sx = Q + R
  let sy = Q - R
  let a1 = calc.atan2(F,G)
  let a2 = calc.atan2(E,H)
  let theta = (a2 - a1) /2
  let phi = (a2 + a1)/2

  set rotate(origin: bottom+center)
  set scale(origin: bottom+center)

  rotate(phi,scale(x: sx*100%, y: sy*100%,rotate(theta,body)))
}

#let fake-italic(body) = skew(-12deg,body)
#fake-italic[이것은 가짜 이탤릭 텍스트입니다]

#let shadowed(body) = box(place(skew(-50deg, vscale: 0.8, text(fill:luma(200),body)))+place(body))
#shadowed[이것은 그림자가 있는 멋진 텍스트입니다]
```
