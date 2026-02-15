# 코드 포맷팅 (Code formatting)

## 인라인 강조 (Inline highlighting)

```typ
#let r = raw.with(lang: "r")

다음과 같이 사용할 수 있습니다: #r("x <- c(10, 42)")
```

## 탭 크기 (Tab size)

```````typ
#set raw(tab-size: 8)
```tsv
Year	Month	Day
2000	2	3
2001	2	1
2002	3	10
```
```````

## 테마 (Theme)

[공식 참조 문서](https://typst.app/docs/reference/text/raw/#parameters-theme)를 확인하세요.

## 코드 합자(Ligatures) 활성화

```typ
#show raw: set text(ligatures: true, font: "Cascadia Code")

이제 코드가 `x <- a`와 같이 표시됩니다.
```

## 고급 포맷팅

[패키지](../packages/code.md) 섹션을 참조하세요.
