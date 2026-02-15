# Typst 예시 북 (Typst Examples Book)

책 내용은 여기에서 확인하세요: https://sitandr.github.io/typst-examples-book/book/

## 하이라이팅 및 렌더링

현재 https://github.com/sitandr/mdbook-typst-highlight 를 사용하고 있습니다.

## 기여하기

책에 추가하고 싶은 스니펫이 있다면 자유롭게 Issue를 생성해 주세요.

모든 PR(Pull Request)을 환영합니다!

일반적으로 다음과 같은 기여를 권장합니다:

- 편집 (예제 확장, 어색한 문장 수정)
- Discord 및 GitHub에서 정말 유용한 코드 예제 선별
- 아이디어 (책을 더 유용하게 만들기 위한 모든 아이디어)

현재 필요한 도움:
- 상태(state) 매뉴얼을 컨텍스트 표현식(context expressions)으로 업데이트하는 작업
- 새로운 Typst 버전의 기능을 반영하여 예제 업데이트
- 인상적인 데모 추가

큰 규모의 작업을 계획 중이시라면 작업 중복을 피하기 위해 Discord (@sitandr) 또는 이메일 (andr.sitnikov34@gmail.com)로 DM을 주세요.

또한 제가 PR을 잊고 있는 것 같다면 DM을 보내주세요. 기억력이 좋지 않습니다.

## 규칙

1. 많은 스니펫이 Discord, GitHub 또는 다른 곳에서 가져온 것입니다. 그분들의 도움이 없었다면 이 책을 쓰는 것은 훨씬 더 어려웠을 것입니다. 하지만 모든 스니펫에 대해 일일이 동의를 구하는 것은 매우 어렵습니다.
    따라서 일반적인 규칙으로, 스니펫이 사소하지 않은 것(Typst 함수를 스마트하게 조합한 것)인 경우 원작자의 크레딧을 명시해야 합니다 (원작자가 반대할 경우 크레딧은 삭제됩니다).
2. "Typst 기초" 섹션에서는 아직 설명하지 않은 개념은 가능하면 피해야 합니다. 하지만 정말 직관적이고 그 개념 없이는 설명이 너무 지루해진다면 사용하는 것도 괜찮습니다.
3. "Typst 스니펫"과 "Typstonomicon"에는 공식 패키지에 이미 존재하는 내용을 포함해서는 안 됩니다. 대신 해당 패키지로 연결되는 링크를 제공해야 합니다. 하지만 패키지 사용이 "부수적"이거나 특정 작업에 해당 패키지를 사용하는 아이디어가 명확하지 않은 경우에는 스니펫에서 패키지를 도구로 사용하는 것이 허용됩니다.
4. 거대한 쿼리나 해킹성 코드는 아무리 유용하더라도 "Typst 스니펫"이 아닌 "Typstonomicon"으로 가야 합니다. "Typst 스니펫"은 가능한 한 깨끗한 코드를 포함해야 합니다.

## 캐시된 Typst 파일 삭제

```bash
git clean -d -X -i
```

유용한 파일이 삭제되지 않도록 주의하세요.

## 컴파일

책을 컴파일하려면 `typst` cli, `mdbook`, 그리고 하이라이팅 및 렌더링 프리프로세서인 `mdbook-typst-highlight`가 설치되어 있어야 합니다. `typst`가 이미 설치되어 있다고 가정할 때, cargo를 이용한 설치 방법은 다음과 같습니다:

```bash
cargo install mdbook
cargo install --git https://github.com/sitandr/mdbook-typst-highlight
```

또는 `mdbook`과 `mdbook-typst-highlight` 릴리스 페이지에서 미리 컴파일된 바이너리를 설치할 수도 있습니다. 결과적으로 모든 도구의 최신 버전이 PATH에 포함되어 있어야 합니다.

모든 것이 설치되면 `mdbook build` 명령어로 책을 빌드할 수 있습니다. 지속적인 재빌드를 위해 `mdbook watch`를 사용할 수 있으며, `--open` 옵션을 사용하여 브라우저에서 책을 바로 열 수 있습니다. 빌드에 대한 자세한 내용은 `mdbook` 문서를 참조하세요.
