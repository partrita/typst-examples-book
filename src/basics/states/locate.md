# 위치 찾기 (Locate)
<div class="warning">이 섹션은 완전하지 않을 수 있으며 최신 Typst 버전에 맞춰 충분히 업데이트되지 않았을 수 있습니다. 모든 기여를 환영합니다!</div>

## 위치 (Location)
> [참조](https://typst.app/docs/reference/meta/location/) 링크

```typ
나의 위치: #context #here()!
```

## `state.at(loc)`
주어진 위치에서 _상태의 값_을 반환합니다.
일종의 _시간 여행_을 가능하게 하여, 문서의 _어느 지점에서든_ 위치를 가져올 수 있습니다.

`state.display`는 대략 다음과 동일합니다.
```typ
#let display(state) = locate(location => {
  state.at(location)
})

#let x = state("x", 0)
#x.display() \
#x.update(n => n + 3)
#display(x)
```

## 최종 값 (Final)
상태의 _최종 값_을 계산합니다.

재컴파일 시 변경될 콘텐츠를 제한하기 위해 위치가 필요합니다.
이는 속도를 크게 높이고 "충돌"을 더 잘 해결합니다.
```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  최종 x 값은 #x.final(loc) 입니다.
])

#x.update(-3)
x = #x.display()

#x.update(n => n + 1)
x = #x.display()
```

## 수렴 (Convergence)
때때로 레이아웃이 _수렴하지 않을 수 있습니다_. 예를 들어 다음과 같은 상황을 가정해 보세요:

```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  // x를 최종 x + 1로 설정하면
  // 어떤 일이 벌어질까요?
  #x.update(x.final(loc) + 1)
  #x.display()
])
```

**경고**: 레이아웃이 5회 시도 내에 수렴하지 않았습니다.

이 레이아웃은 해결이 불가능하므로 Typst는 포기하고 경고를 보냅니다.

즉, 상태를 사용할 때는 _주의_해야 한다는 뜻입니다!

이것은 큰 희생이 따르는 _진정한 **어둠의 마법**_입니다!
