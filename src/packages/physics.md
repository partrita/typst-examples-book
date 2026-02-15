# 물리학 (Physics)

## `physica`

> Physica(라틴어로 _자연과학_)는 자연과학에서 복잡하고 반복적인 수학 표현식을 단순화하는 유틸리티를 제공합니다.

> [매뉴얼](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)은 이 패키지가 어떻게 도움이 될 수 있는지에 대한 전체 데모 세트를 제공합니다.

### 수리 물리학

[packages/math.md](./math.md#일반적인-표기법) 페이지에 수학적 기능에 대한 더 많은 예제가 있습니다. 다음은 물리학 분야에서 특히 흥미로울 수 있는 미리보기입니다:
* 미적분학: 미분, 상미분 및 편미분
  * 선택적 함수 이름,
  * 선택적 차수 번호 또는 차수 번호 배열,
  * 사용자 정의 "d" 기호 및 곱 결합자 (예: 외적),
  * 재정의 가능한 총 차수 계산,
* 벡터 및 벡터장: div, grad, curl,
* 테일러 전개,
* 디랙 브라-켓(Dirac braket) 표기법,
* 추상 인덱스 표기법이 있는 텐서,
* 행렬 전치 및 대거(켤레 전치).
* 특수 행렬: 행렬식, (반)대각, 항등, 영, 야코비안, 헤시안 등. <!-- TODO physica:0.9.2에서 회전 및 그람 행렬 추가 예정 -->

일부 예시:

```typ
#import "@preview/physica:0.9.1": *
#show: super-T-as-transpose // 범위를 제한하려면 #[...] 안에 넣으세요...
#show: super-plus-as-dagger // ...또는 scripts()를 사용하여 수동으로 재정의하세요.

$ dd(x,y,2) quad dv(f,x,d:Delta)      quad pdv(,x,y,[2i+1,2+i]) quad
  vb(a) va(a) vu(a_i)  quad mat(laplacian, div; grad, curl)     quad
  tensor(T,+a,-b,+c)   quad ket(phi)  quad A^+ e^scripts(+) A^T integral^T $
```

### 동위원소 (Isotopes)

```typ
#import "@preview/physica:0.9.1": isotope

// a: 질량수 A
// z: 원자 번호 Z
$
isotope(I, a:127), quad isotope("Fe", z:26), quad
isotope("Tl",a:207,z:81) --> isotope("Pb",a:207,z:82) + isotope(e,a:0,z:-1)
$
```

### 디랙 상수 (Reduced Planck constant, hbar)

기본 글꼴에서 Typst 내장 기호인 `planck.reduce`는 약간 어색해 보입니다. 기호의 통칭인 "h-바"와 달리 글자 "h"에 가로 막대 대신 사선이 그어져 있기 때문입니다. 이 패키지는 친숙한 형태의 기호를 렌더링할 수 있는 `hbar`를 제공합니다. 비교:

```typ
#import "@preview/physica:0.9.1": hbar

$ E = planck.reduce omega => E = hbar omega, wide
  frac(planck.reduce^2, 2m) => frac(hbar^2, 2m), wide
  (pi G^2) / (planck.reduce c^4) => (pi G^2) / (hbar c^4), wide
  e^(frac(i(p x - E t), planck.reduce)) => e^(frac(i(p x - E t), hbar)) $
```

## `quill`: 양자 회로 다이어그램

> [문서](https://github.com/Mc-Zen/quill/tree/main)를 참조하세요.

```typ
#import "@preview/quill:0.2.0": *
#quantum-circuit(
  lstick($|0〉$), gate($H$), ctrl(1), rstick($(|00〉+|11〉)/√2$, n: 2), [\ ],
  lstick($|0〉$), 1, targ(), 1
)
```

```typ
#import "@preview/quill:0.2.0": *

#let ancillas = (setwire(0), 5, lstick($|0〉$), setwire(1), targ(), 2, [\ ],
setwire(0), 5, lstick($|0〉$), setwire(1), 1, targ(), 1)

#quantum-circuit(
  scale-factor: 80%,
  lstick($|ψ〉$), 1, 10pt, ctrl(3), ctrl(6), $H$, 1, 15pt, 
    ctrl(1), ctrl(2), 1, [\ ],
  ..ancillas, [\ ],
  lstick($|0〉$), 1, targ(), 1, $H$, 1, ctrl(1), ctrl(2), 
    1, [\ ],
  ..ancillas, [\ ],
  lstick($|0〉$), 2, targ(),  $H$, 1, ctrl(1), ctrl(2), 
    1, [\ ],
  ..ancillas
)
```

```typ
#import "@preview/quill:0.2.0": *

#quantum-circuit(
  lstick($|psi〉$),  ctrl(1), gate($H$), 1, ctrl(2), meter(), [\ ],
  lstick($|beta_00〉$, n: 2), targ(), 1, ctrl(1), 1, meter(), [\ ],
  3, gate($X$), gate($Z$),  midstick($|psi〉$)
)
```
