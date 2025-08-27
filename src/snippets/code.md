# 코드 서식

## 인라인 하이라이팅

```typ
#let r = raw.with(lang: "r")

이것은 다음과 같이 사용할 수 있습니다: #r("x <- c(10, 42)")
```

## 탭 크기

```````typ
#set raw(tab-size: 8)
```tsv
Year	Month	Day
2000	2	3
2001	2	1
2002	3	10
```
```````

## 테마

[참조](https://typst.app/docs/reference/text/raw/#parameters-theme)를 참조하세요.

## 코드에 합자 활성화

```typ
#show raw: set text(ligatures: true, font: "Cascadia Code")

그러면 코드는 `x <- a`가 됩니다.
```

## 고급 서식

[패키지](../packages/code.md) 섹션을 참조하세요.