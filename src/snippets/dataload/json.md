# JSON

`저자: MuhammadAly11`

JSON 파일에서 JSON 배열을 가져와 사용하는 방법의 예시입니다.

작성하려는 테스트를 위한 다음과 같은 데이터 예시가 있다고 가정해 봅시다:

```json
[
    {
        "sn": "1",
        "source": "Science",
        "question": "물(water)의 화학 기호는 무엇인가요?",
        "answer": "a",
        "a": "H₂O",
        "b": "CO₂",
        "c": "O₂",
        "d": "N₂",
    },
    {
        "sn": "2",
        "source": "History",
        "question": "미국의 초대 대통령은 누구인가요?",
        "answer": "a",
        "a": "조지 워싱턴",
        "b": "에이브러햄 링컨",
        "d": "존 애덤스",
    }
]
```

이 파일을 Typst로 가져와서 사용할 수 있습니다:

```typ
#let json_data = json("../file.json")

#for mcq in json_data {
    [== #mcq.sn. #mcq.question: ]
    for opt in ("a", "b", "c", "d", "e", "f", "g") {
        if opt in mcq and mcq.at(opt) != "" {
            [- #opt) #mcq.at(opt)]
        }
    }
}
```
