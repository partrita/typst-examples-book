# 연산
## 분수
```typ
$
p/q, p slash q, p\/q
$
```

### 약간 이동:
```typ
#let mfrac(a, b) = move(a, dy: -0.2em) + "/" + move(b, dy: 0.2em, dx: -0.1em)
$A\/B, #mfrac($A$, $B$)$,
```

### 큰 분수
```typ
#let dfrac(a, b) = $display(frac(#a, #b))$

$(x + y)/(1/x + 1/y) quad (x + y)/(dfrac(1,x) + dfrac(1, y))$
```