# 테마 (Themes)

Typst에서 테마는 주로 패키지 형태로 제공되며, 문서 전체의 스타일(`set` 및 `show` 규칙)을 한 번에 적용하는 함수로 구현됩니다.

## 프레젠테이션 테마: Touying
[Touying](https://touying.pages.dev/)은 현재 Typst에서 가장 강력한 프레젠테이션 패키지 중 하나입니다. 다양한 내장 테마를 제공합니다.

```typ
#import "@preview/touying:0.5.3": *
#import themes.university: *

#show: university-theme.with(
  aspect-ratio: "16-9",
  config-info: (
    title: [테마가 적용된 프레젠테이션],
    author: [저자 성함],
    institution: [소속 기관],
  ),
)

== 첫 번째 슬라이드
테마가 깔끔하게 적용되었습니다.

- 항목 1
- 항목 2
```

## 이력서 테마: Modern CV
이미 데모에서 보았듯이, `modern-cv`와 같은 패키지는 전문적인 이력서 테마를 제공합니다.

```typ
#import "@preview/modern-cv:0.8.0": *

#show: resume.with(
  author: (
    firstname: "길동",
    lastname: "홍",
    positions: ("전문가", "개발자"),
  ),
  profile-picture: none,
  font: "Noto Sans CJK KR",
)

= 경험
- Typst를 이용한 문서 자동화 전문가
```

## 테마 패키지 찾는 법
더 많은 테마와 템플릿은 [Typst Universe](https://typst.app/universe)의 'Templates' 카테고리에서 확인할 수 있습니다.

- **학술 논문**: `IEEE`, `ACM`, `Elsevier` 등 주요 학회 템플릿
- **도서**: `book` 스타일 템플릿
- **공식 문서**: 각국 정부 또는 기관의 표준 서식 템플릿
