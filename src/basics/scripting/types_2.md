# 타입, 파트 II
Typst에서 대부분의 것들은 **불변**합니다. 내용을 변경할 수 없으며, 기존 내용을 사용하여 새 내용을 만들 수만 있습니다(예: 덧셈 사용).

불변성은 Typst가 _가능한 한 순수한 언어_가 되려고 하기 때문에 매우 중요합니다. 함수는 어떤 값을 반환하는 것 외에는 아무것도 하지 않습니다.

그러나 이러한 타입에 의해 순수성이 부분적으로 "깨집니다". 이것들은 *매우 유용*하며, 추가하지 않으면 Typst가 훨씬 더 고통스러워질 것입니다.

그러나 이것들을 사용하면 복잡성이 추가됩니다.

## 배열 (`array`)
> [참조 링크](https://typst.app/docs/reference/foundations/array/).

인덱스와 함께 데이터를 저장하는 가변 객체입니다.

### 인덱스로 작업하기
```typ
#let values = (1, 7, 4, -3, 2)

// 인덱스 0의 값 가져오기
#values.at(0) \
// 0의 값을 3으로 설정
#(values.at(0) = 3)
// 음수 인덱스 => 뒤에서부터 시작
#values.at(-1) \
// 짝수인 것의 인덱스 추가
#values.find(calc.even)
```

### 반복 메소드
```typ
#let values = (1, 7, 4, -3, 2)

// 홀수만 남기기
#values.filter(calc.odd) \
// 목록 값의 절대값으로 새 목록 만들기
#values.map(calc.abs) \
// 뒤집기
#values.rev() \
// 배열의 배열을 평평한 배열로 변환
#(1, (2, 3)).flatten() \
// 문자열 배열을 문자열로 결합
#(("A", "B", "C")
 .join(", ", last: " and "))
```

### 목록 연산
```typ
// 목록의 합:
#((1, 2, 3) + (4, 5, 6))

// 목록 곱:
#((1, 2, 3) * 4)
```

### 빈 목록
```typ
#() \ // 이것은 빈 목록입니다
#(1,) \  // 이것은 하나의 요소가 있는 목록입니다
나쁨: #(1) // 이것은 목록이 아니라 그냥 요소입니다!
```

## 사전 (`dict`)
> [참조 링크](https://typst.app/docs/reference/foundations/dictionary/).

사전은 문자열 "키"와 해당 키와 연관된 값을 저장하는 객체입니다.
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

### 빈 사전
```typ
이것은 빈 목록입니다: #() \
이것은 빈 사전입니다: #(:)
```
