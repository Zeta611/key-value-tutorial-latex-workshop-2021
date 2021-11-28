# The "key-value" structure in LaTeX
공주대학교 문서작성 워크숍 2021에서 **The "key-value" structure in LaTeX**을 주제로 발표한 자료입니다.

## Key-value 입력이란?
LaTeX 문서를 작성하다보면, `<key>=<value>` 형태의 인자를 넘겨주는 명령어들을 자주 찾아볼 수 있습니다.
예를 들어, 이미지를 넣을 경우 사용하는 명령어는 다음과 같이 사용할 수 있습니다:
```tex
\includegraphics[width=0.9\textwidth]{image}
```
하지만 놀랍게도 LaTeX 2e에는 `<key>=<value>` 인자 형식을 처리하는 방식이 표준으로 정해져 있지 않습니다.
즉, 패키지 저자가 위와 같은 입력을 지원하기 위해서는 써드파티 패키지에 의존할 수 밖에 없습니다.
그럼에도 불구하고 이런 입력 방식이 사용자 입장에서는 굉장히 간편하고, 패키지 저자 입장에서는 패키지의 유연한 설정을 가능케하기 때문에 자주 사용됩니다.
따라서 이를 지원하는 패키지들도 [서로 다른 사람들에 의해 꽤 많이 만들어졌습니다](https://ctan.org/topic/keyval).

다행히 현시점에는 LaTeX 3 프로젝트의 '실험적인' 프로그래밍 언어이자 인터페이스인 *expl3*에 포함된 *l3keys*를 통해서 key-value 형식을 상당히 편리하게 다룰 수 있습니다.
*expl3*가 거의 안정화된 것을 고려하면, 지금 이 방식을 쓰지 않을 이유가 없습니다.
나아가 *l3prop* 모듈의 (다른 언어에서 사전, 맵, 연관 배열 등으로 불리우는) property list를 통해 범용 자료 구조로써의 key-value 형식을 쓸 수 있습니다.

본 발표에서는 지금까지 key-value 형식을 처리하기 위해 어떤 노력들이 있었는지 살펴보고, 현시점에서 가장 권장할 만한 key-value 처리 모듈인 *l3keys* 사용법에 대해서 소개합니다.
나아가, *expl3* 언어를 사용하여 key-value 시스템이 실제로 활용되는 방법을 보여드리기 위해 [간단한 패키지](materials/textstats/textstats.sty)를 데모로 만들었습니다.

## 튜토리얼 자료에 관하여
[materials](materials) 디렉터리 안에서 실습자료들을 확인할 수 있습니다.
[발표자료](keyval-slides.pdf)의 각 슬라이드에 해당하는 실습자료 파일명이 나와 있습니다.

어느정도 최근 버전의 TeX 배포판을 사용하지 않으면 다른 결과가 나오거나 오류가 발생할 수 있습니다.
자료들을 제작한 당시에는 TeX Live 2021 배포판을 사용하였습니다.

### 조판
pdfLaTeX, XeLaTeX, LuaLaTeX 등의 엔진으로 조판합니다.
```sh
pdflatex keyval-tutorial.tex
```

## 발표자료에 관하여
폰트는 [Fira Sans](https://fonts.google.com/specimen/Fira+Sans), [Noto Sans CJK KR](https://fonts.google.com/noto)을 사용했으며, *minted* 패키지에 필요한 [Python 3](https://www.python.org) 및 [Pygments](https://pygments.org) 패키지가 필요합니다.
아래 권장된 설치 방법을 따르지 않을 시 폰트 이름의 차이로 인해 발표자료의 [소스코드](keval-slides.tex]에서 폰트 설정 부분을 조정해야 할 수 있습니다.

### 폰트 설치
macOS의 경우 [Homebrew](https://brew.sh)의 [Homebrew Cask](https://github.com/Homebrew/homebrew-cask)를 사용해 설치를 권장합니다.
[homebrew-cask-fonts](https://github.com/Homebrew/homebrew-cask-fonts)를 tap하여 사용합니다:
```sh
brew tap homebrew/cask-fonts
brew install font-fira-sans font-noto-sans-cjk-kr
```

나머지 운영체제의 경우 각 운영체제의 권장 폰트 설치 방법을 참고하기 바랍니다.

폰트를 직접 다운로드 받아 설치할 수 있습니다.
Fira Sans는 [여기](https://github.com/mozilla/Fira/archive/4.202.tar.gz), Noto Sans CJK KR은 [여기](https://noto-website-2.storage.googleapis.com/pkgs/NotoSansCJKkr-hinted.zip)를 눌러 받으세요.

### 조판
XeLaTeX으로 조판합니다.
```sh
xelatex keyval-slides.tex
```
