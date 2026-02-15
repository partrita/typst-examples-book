# 기타 (Misc)

hydra ()
outrageous (개요 스타일링, 정렬된 반복 점선 기능 포함 예정)

# 문자열 포맷팅

## `oxifmt`: 범용 문자열 포맷터

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#strfmt("저는 {}입니다. 차를 {num}대 가지고 있어요. 저는 {0}입니다. {}는 {{멋져요}}.", "철수", "길동", num: 10) \
#strfmt("{0:?}, {test:+012e}, {1:-<#8x}", "안녕", -74, test: 569.4) \
#strfmt("{:_>+11.5}", 59.4) \
#strfmt("딕셔너리: {:!<10?}", (a: 5))
```

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#strfmt("첫 번째: {}, 두 번째: {}, 네 번째: {3}, 바나나: {banana} (중괄호: {{이스케이프}})", 1, 2.1, 3, label("four"), banana: "바나나!!")\
#strfmt("값은: {:?} | 레이블은 {:?}", "무언가", label("레이블"))\
#strfmt("값들: {:?}, {1:?}, {stuff:?}", (test: 500), ("a", 5.1), stuff: [a])\
#strfmt("좌측5 {:_<5}, 우측6 {:*>6}, 중앙10 {centered: ^10?}, 좌측3 {tleft:_<3}", "xx", 539, tleft: "좋아요", centered: [a])\
```

```typ
#import "@preview/oxifmt:0.2.1": strfmt
#repr(strfmt("좌측 패딩7 숫자: {:07} {:07} {:07} {3:07}", 123, -344, 44224059, 45.32))\
#strfmt("일부 숫자: {:+} {:+08}; 채우기와 정렬 포함: {:_<+8}; 음수 (무시): {neg:+}", 123, 456, 4444, neg: -435)\
#strfmt("진법 (10, 2, 8, 16(소문자), 16(대문자):) {0} {0:b} {0:o} {0:x} {0:X} | 접두사와 수정자 포함: {0:#b} {0:+#09o} {0:_>+#9X}", 124)\
#strfmt("{0:.8} {0:.2$} {0:.potato$}", 1.234, 0, 2, potato: 5)\
#strfmt("{0:e} {0:E} {0:+.9e} | {1:e} | {2:.4E}", 124.2312, 50, -0.02)\
#strfmt("{0} {0:.6} {0:.5e}", 1.432, fmt-decimal-separator: ",")
```

## `name-it`: 숫자를 텍스트로 변환
```typ
#import "@preview/name-it:0.1.0": name-it

- #name-it(2418345)
```

## `nth`: N번째 요소
```typ
#import "@preview/nth:0.2.0": nth
#nth(3), #nth(5), #nth(2421)
```
