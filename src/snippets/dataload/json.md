# JSON

`저자: MuhammadAly11`

json 파일에서 json 배열을 가져와 사용하는 방법의 예입니다.

작성하려는 테스트에 대한 다음 데이터 예제를 고려하십시오:

```json
[
    {
        "sn": "1",
        "source": "Science",
        "question": "물의 화학 기호는 무엇입니까?",
        "answer": "a",
        "a": "H₂O",
        "b": "CO₂",
        "c": "O₂",
        "d": "N₂",
    },
    {
        "sn": "2",
        "source": "History",
        "question": "미국의 초대 대통령은 누구였습니까?",
        "answer": "a",
        "a": "George Washington",
        "b": "Abraham Lincoln",
        "d": "John Adams",
    }
]
```

이 파일을 가져와 Typst에서 사용할 수 있습니다:

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