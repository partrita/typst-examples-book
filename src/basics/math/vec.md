# 벡터, 행렬, 세미콜론 문법

## 벡터 (Vectors)

> 여기서 벡터는 열(column)을 의미합니다. \
> 문자에 화살표 표기법을 쓰려면 `$arrow(v)$`를 사용하세요. \
> `#let arr = math.arrow`와 같이 단축키를 만드는 것을 추천합니다.

열을 쓰려면 `vec` 명령어를 사용하세요:

```typ
$
vec(a, b, c) + vec(1, 2, 3) = vec(a + 1, b + 2, c + 3)
$
```

### 구분자 (Delimiter)
열 주변의 괄호를 변경하거나 제거할 수도 있습니다:

```typ
$
vec(1, 2, 3, delim: "{") \
vec(1, 2, 3, delim: bar.double) \
vec(1, 2, 3, delim: #none)
$
```

### 간격 (Gap)

행 사이의 간격 크기를 변경할 수 있습니다:

```typ
$
vec(a, b, c)
vec(a, b, c, gap:#0em)
vec(a, b, c, gap:#1em)
$
```

### 간격 일정하게 만들기

벡터마다 간격이 반드시 일정하거나 같지 않다는 것을 쉽게 알 수 있습니다:

```typ
$
vec(a/b, a/b, a/b) = vec(1, 1, 1)
$
```
이는 `gap`이 요소의 중심 간 거리가 아니라 요소 _사이의 간격_을 의미하기 때문에 발생합니다.

이를 해결하려면 [이 스니펫](../../snippets/math/vecs.md)을 사용할 수 있습니다.

## 행렬 (Matrix)

> [공식 참조](https://typst.app/docs/reference/math/mat/)를 확인하세요.

행렬은 `vec`과 매우 유사하지만, `;`로 구분된 행을 받습니다:

```typ
$
mat(
    1, 2, ..., 10;
    2, 2, ..., 10;
    dots.v, dots.v, dots.down, dots.v;
    10, 10, ..., 10; // 끝에 있는 `;`는 선택 사항입니다
)
$
```

### 구분자와 간격

벡터와 같은 방식으로 지정할 수 있습니다.

<div class="warning">
    인수는 내용 앞이나 <strong>세미콜론 뒤에</strong> 지정하세요. 세미콜론이 없으면 코드가 패닉 상태가 됩니다!
</div>

```typ
$
mat(
    delim: "|",
    1, 2, ..., 10;
    2, 2, ..., 10;
    dots.v, dots.v, dots.down, dots.v;
    10, 10, ..., 10;
    gap: #0.3em
)
$
```

## 세미콜론 문법

세미콜론을 사용할 때, _세미콜론 사이의_ 인수는 배열로 병합됩니다. 직접 확인해 보세요:

```typ
#let fun(..args) = {
    args.pos()
}

$
fun(1, 2;3, 4; 6, ; 8)
$
```

일부 요소를 빠뜨리면 `none`으로 대체됩니다.

세미콜론 문법과 명명된 인수를 섞어 쓸 수 있지만 주의하세요!

```typ
#let fun(..args) = {
    repr(args.pos())
    repr(args.named())
}

$
fun(1, 2; gap: #3em, 4)
$
```

예를 들어, 이것은 작동하지 않습니다:

```typ-norender
$
//         ↓ `;`가 없으므로 (gap:)을 배열에 추가하려고 시도합니다.
mat(1, 2; 4, gap: #3em)
$
```
