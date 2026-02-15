# 하이픈 연결 (Hyphenation)

Typst는 텍스트가 줄 끝에 걸칠 때 자동으로 하이픈(-)을 넣어 단어를 끊어주는 기능을 지원합니다.

## 자동 하이픈 활성화
기본적으로 하이픈 연결은 비활성화되어 있을 수 있습니다. `set text` 규칙을 사용하여 활성화합니다.

```typ
#set page(width: 15em)
#set text(hyphenate: true, lang: "en")

Hyphenation is the process of inserting hyphens between the syllables of a word, especially such that an appropriate line break can occur.
```

## 언어 설정의 중요성
하이픈 연결 규칙은 언어마다 다릅니다. 올바른 하이픈 연결을 위해 반드시 `lang` 속성을 지정해야 합니다.

```typ
// 독일어 하이픈 규칙 적용
#set text(lang: "de", hyphenate: true)
Donaudampfschifffahrtselektrizitätenhauptbetriebswerkbauunterbeamtengesellschaft
```

## 수동 하이픈 제어
특정 단어가 끊어지는 것을 방지하거나, 특정 위치에서만 끊어지게 하려면 다음과 같은 기호를 사용합니다.

- **줄 바꿈 방지 공백**: `~` 또는 `#sym.space.nobreak`
- **소프트 하이픈 (Soft hyphen)**: `\-` (필요한 경우에만 하이픈 표시)
- **줄 바꿈 방지 하이픈**: `\u{2011}`

```typ
#set page(width: 10em)
#set text(hyphenate: true)

// 이 단어는 절대 끊어지지 않습니다.
#box[unbreakable-word]

// 하이픈 위치를 직접 지정합니다.
유비쿼\-터스 환경에서의 조판
```
