# 템플릿
## 템플릿
스타일을 다른 파일에서도 재사용하고 싶다면 _템플릿(template)_ 관용구를 사용할 수 있습니다.
`set` 및 `show` 규칙은 현재 범위(scope) 내에서만 활성화되므로,
파일을 가져온(import) 대상 파일의 콘텐츠에는 영향을 주지 않습니다.
하지만 함수를 사용하면 예측 가능한 방식으로 이를 해결할 수 있습니다:
```typ-norender
// 다음과 같은 함수를 정의합니다:
// - 콘텐츠를 인수로 받음
// - 스타일을 적용함
// - 스타일이 적용된 콘텐츠를 반환함
#let apply-template(body) = [
  #show heading.where(level: 1): emph
  #set heading(numbering: "1.1")
  // ...
  #body
]
```

이것은 다음과 동일합니다:
```typ-norender
// 스크립팅 모드를 사용하면 필요한 해시(#) 기호의 수를 줄일 수 있습니다.
// 위와 동일하지만, 마크업 모드에서 스크립팅 모드로 전환하기 위해
// `[...]`를 `{...}`로 바꿨습니다.
#let apply-template(body) = {
  show heading.where(level: 1): emph
  set heading(numbering: "1.1")
  // ...
  body
}
```

그런 다음 메인 파일에서:
```typ-norender
#import "template.typ": apply-template
#show: apply-template
```

_이렇게 하면 문서의 나머지 부분에 "템플릿" 함수가 적용됩니다!_

### 인수 전달하기
```typ-norender
// 선택적인 명명된 인수를 추가합니다.
#let apply-template(body, name: "나의 문서") = {
  show heading.where(level: 1): emph
  set heading(numbering: "1.1")

  align(center, text(name, size: 2em))

  body
}
```

그런 다음, 템플릿 파일에서:
```typ-norender
#import "template.typ": apply-template

// `func.with(..)`는 함수에 인수를 적용하고,
// 해당 기본값이 적용된 새로운 함수를 반환합니다.
#show: apply-template.with(name: "보고서")

// 이것은 기능적으로 다음과 동일합니다.
#let new-template(..args) = apply-template(name: "보고서", ..args)
#show: new-template
```

[스크립팅](../scripting/index.md)을 이해한다면 템플릿을 작성하는 것은 매우 쉽습니다.

템플릿 작성에 대한 더 자세한 정보는 [공식 튜토리얼](https://typst.app/docs/tutorial/making-a-template/)에서 확인할 수 있습니다.

아직 공식 템플릿 저장소는 없지만, [awesome-typst](https://github.com/qjcg/awesome-typst?ysclid=lj8pur1am7431908794#general)에 수많은 커뮤니티 템플릿이 있습니다.
