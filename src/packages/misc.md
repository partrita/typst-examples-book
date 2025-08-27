# 기타

hydra ()
outrageous (개요 스타일링, 정렬된 반복 점이 있는 곧 출시될 릴리스)

# 문자열 서식 지정

## `oxifmt`, 범용 문자열 포맷터

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#strfmt("나는 {}. 나는 차가 {num}대 있어. 나는 {0}이야. {}는 {{멋져}}.", "John", "Carl", num: 10) \
#strfmt("{0:?}, {test:+012e}, {1:-<#8x}", "hi", -74, test: 569.4) \
#strfmt("{:_>+11.5}", 59.4) \
#strfmt("Dict: {:!<10?}", (a: 5))
```

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#strfmt("첫 번째: {}, 두 번째: {}, 네 번째: {3}, 바나나: {banana} (괄호: {{이스케이프됨}})", 1, 2.1, 3, label("four"), banana: "Banana!!")\
#strfmt("값은: {:?} | 레이블도: {:?}", "something", label("label"))\
#strfmt("값: {:?}, {1:?}, {stuff:?}", (test: 500), ("a", 5.1), stuff: [a])\
#strfmt("왼쪽5 {:_<5}, 오른쪽6 {:*>6}, 가운데10 {centered: ^10?}, 왼쪽3 {tleft:_<3}", "xx", 539, tleft: "okay", centered: [a])\
```

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#repr(strfmt("왼쪽으로 채워진 7자리 숫자: {:07} {:07} {:07} {3:07}", 123, -344, 44224059, 45.32))\
#strfmt("일부 숫자: {:+} {:+08}; 채우기 및 정렬 포함: {:_<+8}; 음수 (작동 안 함): {neg:+}", 123, 456, 4444, neg: -435)
#strfmt("진수 (10, 2, 8, 16(l), 16(U):) {0} {0:b} {0:o} {0:x} {0:X} | 접두사 및 수정자 포함: {0:#b} {0:+#09o} {0:_>+#9X}", 124)
#strfmt("{0:.8} {0:.2$} {0:.potato$}", 1.234, 0, 2, potato: 5)
#strfmt("{0:e} {0:E} {0:+.9e} | {1:e} | {2:.4E}", 124.2312, 50, -0.02)
#strfmt("{0} {0:.6} {0:.5e}", 1.432, fmt-decimal-separator: ",")
```

## `name-it`, 정수를 텍스트로

```typ
#import "@preview/name-it:0.1.0": name-it

- #name-it(2418345)
```

## `nth`, N번째 요소

```typ
#import "@preview/nth:0.2.0": nth
#nth(3), #nth(5), #nth(2421)
```
