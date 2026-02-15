# 스크립팅 (Scripting)
## 배열 평탄화 해제 (Unflatten arrays)

```typ
// author: PgSuper
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

## 구분 기호를 포함하여 문자열 분할

```typ
#",this, is a a a a; a. test? string!".matches(regex("(\b[\P{Punct}\s]+\b|\p{Punct})")).map(x => x.captures).join()
```

## 배열의 모든 값과 일치하는 선택자 생성

이 스니펫은 배열 내부의 값 중 하나라도 일치하는 선택자(show 규칙에서 사용됨)를 생성합니다.
여기서는 몇 개의 raw 라인을 강조 표시하는 데 사용되지만, 어떤 종류의 선택자에도 쉽게 적용할 수 있습니다.

````typ
// author: Blokyk
#let lines = (2, 3, 5)
#let lines-selectors = lines.map(lineno => raw.line.where(number: lineno))
#let lines-combined-selector = lines-selectors.fold(
  // 기본적으로 첫 번째 선택자로 시작
  // 가능한 경우 아무것도 일치하지 않는 선택자를 사용할 수도 있음
  lines-selectors.at(0),
  selector.or // 모든 선택자의 OR 생성 (대안: (acc, sel) => acc.or(sel))
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

## 딕셔너리에서 show (또는 show-set) 규칙 합성

이 스니펫은 키를 선택자로, 값을 설정할 매개변수로 사용하여 딕셔너리 내부의 모든 요소에 show-set 규칙을 적용합니다.
이 예제에서는 대응 딕셔너리를 기반으로 사용자 정의 그림 종류에 사용자 정의 보충(supplement)을 제공하는 데 사용됩니다.

```typ
// author: laurmaedje
#let kind_supp_dict = (
  algo: "Pseudo-code",
  ex: "Example",
  prob: "Problem",
)

// 전체 (나머지) 문서에 이 규칙 적용
#show: it => {
  kind_supp_dict
    .pairs() // 키-값 쌍의 배열 가져오기
    .fold( // 문서 앞에 show-set 규칙을 쌓을 것입니다
      it, // 기본 문서로 시작
      (acc, (kind, supp)) => {
        // 나머지의 맨 위에 현재 kind-supp 조합 추가
        show figure.where(kind: kind): set figure(supplement: supp)
        acc
      }
    )
}
#figure(
    kind: "algo",
    caption: [내 코드],
    ```Algorithm there```
)
```

또한, 이것은 작성한 위치에 적용되므로, 이 show-set 규칙들은 규칙을 작성한 같은 장소에 추가된 것처럼 보일 것입니다.
즉, 다른 show-set 규칙과 마찬가지로 나중에 덮어쓸 수 있습니다.
