# 위치 찾기
<div class="warning">이 섹션은 최신 Typst 버전에 대해 완전히 완전하거나 업데이트되지 않았을 수 있습니다. 어떤 기여든 매우 환영합니다!.</div>

## 위치
> [참조](https://typst.app/docs/reference/meta/location/) 링크

```typ
내 위치: #context #here()!
```

## `state.at(loc)`
주어진 위치에서 _상태의 값_을 반환합니다.
이것은 일종의 _시간 여행_을 허용하며, 문서의 _어느 곳에서나_ 위치를 얻을 수 있습니다.

`state.display`는 대략 다음과 같습니다
```typ
#let display(state) = locate(location => {
  state.at(location)
})

#let x = state("x", 0)
#x.display() \
#x.update(n => n + 3)
#display(x)
```

## 최종
상태의 _최종 값_을 계산합니다.

재컴파일 내에서 변경될 내용을 제한하기 위해 위치가 필요합니다.
이것은 속도를 크게 향상시키고 "충돌"을 더 잘 해결합니다.
```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  최종 x 값은 #x.final(loc)입니다
])

#x.update(-3)
x = #x.display()

#x.update(n => n + 1)
x = #x.display()
```

## 수렴
때때로 레이아웃이 _수렴하지 않을 수 있습니다_. 예를 들어, 이것을 상상해보십시오:

```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  // x를 최종 x + 1로 설정해 봅시다
  // 그리고 무슨 일이 일어나는지 봅시다?
  #x.update(x.final(loc) + 1)
  #x.display()
])
```

**경고**: 5번의 시도 내에 레이아웃이 수렴하지 않았습니다

해당 레이아웃을 해결하는 것은 불가능하므로 Typst는 포기하고 경고를 표시합니다.

이는 상태에 _주의해야 함_을 의미합니다!

이것은 큰 희생을 요구하는 _어둡고, **어두운 마법**_입니다!
