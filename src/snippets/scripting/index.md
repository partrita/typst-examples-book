# 스크립팅
## 배열 평탄화 해제

```typ
// 저자: PgSuper
#let unflatten(arr, n) = {
  let columns = range(0, n).map(_ => ())
  for (i, x) in arr.enumerate() {
    columns.at(calc.rem(i, n)).push(x)
  }
  array.zip(..columns)
}

#unflatten((1, 2, 3, 4, 5, 6), 2)
#unflatten((1, 2, 3, 4, 5, 6), 3)
```

## 약어 만들기
```typ
#let full-name = "Federal University of Ceará"

#let letts = {
  full-name
    .split()
    .map(word => word.at(0)) // 대문자만 필터링
    .filter(l => upper(l) == l)
    .join()
}
#letts
```

## 구분 기호를 검색하여 문자열 분할

```typ
#",this, is a a a a; a. test? string!".matches(regex("(\b[\P{Punct}\s]+\b|\p{Punct})")).map(x => x.captures).join()
```

## 배열의 모든 값과 일치하는 선택기 만들기

이 스니펫은 배열 내부의 모든 값과 일치하는 선택기(그런 다음 표시 규칙에서 사용됨)를 만듭니다. 여기서는 몇 개의 원시 줄을 강조 표시하는 데 사용되지만 모든 종류의 선택기에 쉽게 적용할 수 있습니다.

````typ
// 저자: Blokyk
#let lines = (2, 3, 5)
#let lines-selectors = lines.map(lineno => raw.line.where(number: lineno))
#let lines-combined-selector = lines-selectors.fold(
  // 기본적으로 첫 번째 선택기로 시작
  // 가능한 경우 아무것도 일치하지 않는 선택기를 사용할 수도 있습니다.
  lines-selectors.at(0),
  selector.or // 모든 선택기의 OR 만들기 (또는: (acc, sel) => acc.or(sel))
)

#show lines-combined-selector: highlight

```py
def foo(x, y):
  if x == y:
    return False
  z = x + y
  return z * x - z * y >= z
```
````

## 사전에서 표시(또는 표시-설정) 규칙 합성

이 스니펫은 사전을 사용하여 키를 선택기로 사용하고 값을 설정할 매개변수로 사용하여 사전 내부의 모든 요소에 표시-설정 규칙을 적용합니다. 이 예에서는 대응 사전을 기반으로 사용자 정의 그림 종류에 사용자 정의 보충 자료를 제공하는 데 사용됩니다.

```typ
// 저자: laurmaedje
#let kind_supp_dict = (
  algo: "의사 코드",
  ex: "예제",
  prob: "문제",
)

// 이 규칙을 전체 (나머지) 문서에 적용합니다.
#show: it => {
  kind_supp_dict
    .pairs() // 키-값 쌍의 배열 가져오기
    .fold( // 문서 앞에 표시-설정 규칙을 쌓을 것입니다.
      it, // 기본 문서로 시작
      (acc, (kind, supp)) => {
        // 나머지 위에 현재 종류-보충 조합을 추가합니다.
        show figure.where(kind: kind): set figure(supplement: supp)
        acc
      }
    )
}
#figure(
    kind: "algo",
    caption: [내 코드],
    ```거기에 알고리즘```
)
```

추가로, 이것은
작성한 위치에 적용되므로 이러한 표시-설정 규칙은
작성한 것과 동일한 위치에 추가된 것처럼 나타납니다. 즉, 다른 표시-설정 규칙과 마찬가지로 나중에 재정의할 수 있습니다.