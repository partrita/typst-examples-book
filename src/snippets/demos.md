# 데모

## 이력서 (템플릿 사용)

```typ
#import "@preview/modern-cv:0.8.0": *

#show: resume.with(
  author: (
    firstname: "John",
    lastname: "Smith",
    email: "js@example.com",
    homepage: "https://example.com",
    phone: "(+1) 111-111-1111",
    github: "DeveloperPaul123",
    twitter: "typstapp",
    scholar: "",
    orcid: "0000-0000-0000-000X",
    birth: "January 1, 1990",
    linkedin: "Example",
    address: "111 Example St. Example City, EX 11111",
    positions: (
      "Software Engineer",
      "Software Architect",
      "Developer",
    ),
  ),
  profile-picture: none,
  date: datetime.today().display(),
  language: "en",
  colored-headers: true,
  show-footer: false,
  paper-size: "us-letter",
)

= 경력

#resume-entry(
  title: "수석 소프트웨어 엔지니어",
  location: "예시 시, 예시 주",
  date: "2019 - 현재",
  description: "예시 주식회사",
  title-link: "https://github.com/DeveloperPaul123",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]

#resume-entry(
  title: "소프트웨어 엔지니어",
  location: "예시 시, 예시 주",
  date: "2011 - 2019",
  description: "이전 회사 주식회사",
)

#resume-item[
  // 내용은 글머리 기호가 아니어도 됩니다.
  #lorem(72)
]

#resume-entry(
  title: "인턴",
  location: "예시 시, 예시 주",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]

= 프로젝트

#resume-entry(
  title: "스레드 풀 C++ 라이브러리",
  location: [#github-link("DeveloperPaul123/thread-pool")],
  date: "2021년 5월 - 현재",
  description: "설계자/개발자",
)

#resume-item[
  - 최신 C++20 및 C++23 기능을 사용하여 C++로 스레드 풀 라이브러리를 설계하고 구현했습니다.
  - 라이브러리에 대한 광범위한 문서와 단위 테스트를 작성하고 Github에 게시했습니다.
]

#resume-entry(
  title: "이벤트 버스 C++ 라이브러리",
  location: github-link("DeveloperPaul123/eventbus"),
  date: "2019년 9월 - 현재",
  description: "설계자/개발자",
)

#resume-item[
  - C++17을 사용하여 이벤트 버스 라이브러리를 설계하고 구현했습니다.
  - 라이브러리에 대한 자세한 문서와 단위 테스트를 작성하고 Github에 게시했습니다.
]

= 기술

#resume-skill-item(
  "언어",
  (strong("C++"), strong("Python"), "Java", "C#", "JavaScript", "TypeScript"),
)
#resume-skill-item("구사 언어", (strong("영어"), "스페인어"))
#resume-skill-item(
  "프로그램",
  (strong("Excel"), "Word", "Powerpoint", "Visual Studio"),
)

= 학력

#resume-entry(
  title: "예시 대학교",
  location: "예시 시, 예시 주",
  date: "2014년 8월 - 2019년 5월",
  description: "컴퓨터 과학 학사",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]
```

## 책 표지
```typ
// 저자: bamdone
#let accent  = rgb("#00A98F")
#let accent1 = rgb("#98FFB3")
#let accent2 = rgb("#D1FF94")
#let accent3 = rgb("#D3D3D3")
#let accent4 = rgb("#ADD8E6")
#let accent5 = rgb("#FFFFCC")
#let accent6 = rgb("#F5F5DC")

#set page(paper: "a4",margin: 0.0in, fill: accent)

#set rect(stroke: 4pt)
#move(
  dx: -6cm, dy: 1.0cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent1,
)))

#set rect(stroke: 4pt)
#move(
  dx: -2cm, dy: -1.0cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent2,
)))

#set rect(stroke: 4pt)
#move(
  dx: 8cm, dy: -10cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 1cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent3,
)))

#set rect(stroke: 4pt)
#move(
  dx: 7cm, dy: -8cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent4,
)))

#set rect(stroke: 4pt)
#move(
  dx: 0cm, dy: -0cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent1,
)))

#set rect(stroke: 4pt)
#move(
  dx: 9cm, dy: -7cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 1.5cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent6,
)))

#set rect(stroke: 4pt)
#move(
  dx: 16cm, dy: -13cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 1cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent2,
)))

#align(center)[
  #rect(width: 30%,
    fill: accent4,
    stroke:none,
    [#align(center)[
      #text(size: 60pt,[제목])
    ]
    ])
]

#align(center)[
  #rect(width: 30%,
    fill: accent4,
    stroke:none,
    [#align(center)[
      #text(size: 20pt,[저자])
    ]
    ])
]
```
