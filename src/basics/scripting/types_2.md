# 타입, 파트 II (Types, part II)
Typst에서 대부분의 것들은 **불변(immutable)**입니다. 콘텐츠를 직접 변경할 수 없으며, 기존 콘텐츠를 사용하여 새로운 콘텐츠를 만들 수 있을 뿐입니다(예: 덧셈 사용).

불변성은 Typst가 _가능한 한 순수 언어(pure language)_가 되고자 하기 때문에 매우 중요합니다. 함수는 값을 반환하는 것 외에 외부의 어떤 것도 바꾸지 않습니다.

하지만 이러한 타입들에 의해 순수성이 부분적으로 "깨집니다". 이들은 *매우 유용*하며, 이들이 없다면 Typst 작업은 매우 고통스러울 것입니다.

단, 이들을 사용하면 복잡성이 늘어납니다.

## 배열 (`array`)
> [참조](https://typst.app/docs/reference/foundations/array/) 링크

인덱스로 데이터를 저장하는 가변(mutable) 객체입니다.

### 인덱스 다루기
```typ
#let values = (1, 7, 4, -3, 2)

// 인덱스 0의 값 가져오기
#values.at(0) \
// 인덱스 0의 값을 3으로 설정
#(values.at(0) = 3)
// 음수 인덱스 => 뒤에서부터 시작
#values.at(-1) \
// 짝수인 항목의 인덱스 찾기
#values.find(calc.even)
```

### 반복 메서드
```typ
#let values = (1, 7, 4, -3, 2)

// 홀수만 남기기
#values.filter(calc.odd) \
// 리스트 값들의 절대값으로 새로운 리스트 생성
#values.map(calc.abs) \
// 뒤집기
#values.rev() \
// 배열의 배열을 평탄한 배열로 변환
#(1, (2, 3)).flatten() \
// 문자열 배열을 하나의 문자열로 결합
#(("A", "B", "C")
 .join(", ", last: " 및 "))
```

### 리스트 연산
```typ
// 리스트 덧셈:
#((1, 2, 3) + (4, 5, 6))

// 리스트 곱셈:
#((1, 2, 3) * 4)
```

### 빈 리스트
```typ
#() \ // 빈 리스트입니다.
#(1,) \  // 요소가 하나인 리스트입니다.
잘못됨: #(1) // 이것은 리스트가 아니라 그냥 하나의 요소입니다!
```

## 딕셔너리 (`dict`)
> [참조](https://typst.app/docs/reference/foundations/dictionary/) 링크

딕셔너리는 문자열 "키(key)"와 그 키에 연관된 값을 저장하는 객체입니다.
```typ
#let dict = (
  name: "Typst",
  born: 2019,
)

#dict.name \
#(dict.launch = 20)
#dict.len() \
#dict.keys() \
#dict.values() \
#dict.at("born") \
#dict.insert("city", "Berlin ")
#("name" in dict)
```

### 빈 딕셔너리
```typ
이것은 빈 리스트입니다: #() \
이것은 빈 딕셔너리입니다: #(:)
```
