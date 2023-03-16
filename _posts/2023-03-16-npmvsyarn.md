---
layout: single
title: "🔎 npm vs yarn"
toc: true
toc_sticky: true
toc_label: "npm vs yarn"
categories: js
excerpt: "둘다 비슷한것같은데..."
tag: [js]
---

- npm과 yarn은 자바스크립트 런타임 환경인 노드(Node.js)의 패키지 관리자임
- 전 세계의 개발자들이 자바스크립트로 만든 다양한 패키지를 npm 온라인 데이터베이스 (opens new window)에 올리면 npm, yarn과 같은 패키지 관리자를 통해 설치 및 삭제가 가능함
- 그리고 명령 줄 인터페이스(Command-line interface, CLI)를 통해 패키지 설치 및 삭제뿐 아니라 패키지 버전 관리, 의존성 관리도 편리하게 할 수 있음

# 01. npm

- npm은 노드 패키지 매니저 (Node Package Manager)의 줄임말로, 노드를 설치할 때 자동으로 설치되는 기본 패키지 관리자임
- 크게 2가지 역할을 수행하게 됨

1. 온라인 플랫폼

- github처럼, 사람들이 node 패키지를 만들고, 업로드 하고, 공유할 수 있는 공간으로 누구나 온라인 플랫폼(npm 레지스트리)에 게시된 패키지를 사용 할 수 있음

2. CLI
   - 온라인 플랫폼과 상호 작용하기 위해 명령 줄 인터페이스를 사용하며 패키지 설치 및 제거가 가능함

## npm 설치

- 노드를 다운로드 하면 npm이 자동으로 설치됨
- `node -v` or `npm -v`를 사용해 npm이 설치되어있는지 확인 할 수 있음

# 02. yarn

- yarn은 2016년 페이스북에서 개발한 패키지 관리자
- React와 같은 프로젝트를 진행하며 겪었던 어려움을 해결하기 위해 개발되었음
- npm 레지스트리와 호환하면서 속도나 안정성 측면에서 npm보다 향상되었음

## yarn 설치

- yarn은 npm을 통해 설치함
- `npm install yarn --global`
- mac user라면 brew를 통해 설치 할 수도 있음
- `brew update` -> `brew install yarn`

# 03. npm과 yarn의 차이점

### 속도

- 패키지 설치 프로세스를 처리하는 방법이 다름
- npm은 패키지를 하나씩 순차적으로 처리함
- yarn은 여러 패키지를 동시에 가져오고 설치하도록 최적화 되어있어, 패키지 설치 속도 측면에서 yarn이 npm보다 빠름

### 보안

- yarn은 보안 측면에서 npm보다 더 안전함
- npm은 자동으로 패키지에 포함된 다른 패키지 코드를 실행함
- 이로 인해 보안 시스템에 몇가지 취약성이 발생하여 심각한 문제가 발생할 수 있음
- 하지만 yarn은 `yarn.lock` or `package.json`파일에 있는 파일만을 설치함
- 보안은 yarn의 핵심 기능 중 하나이지만, 최근 npm이 업데이트를 통해 보안 업데이트도 크게 향상됨

### 명령어

|                       명령어                       |                 npm                 |             yarn              |
| :------------------------------------------------: | :---------------------------------: | :---------------------------: |
|                 dependencies\n설치                 |             npm install             |             yarn              |
|                    패키지 설치                     |      npm install `[패키지명]`       |     yarn add `[패키지명]`     |
|                  dev 패키지 설치                   |  npm install --save-dev [패키지명]  |   yarn add --dev [패키지명]   |
| 글로벌 패키지 설치 npm install --global [패키지명] |     yarn global add [패키지명]      |
|                    패키지 제거                     |      npm uninstall [패키지명]       |    yarn remove [패키지명]     |
|                  dev 패키지 제거                   | npm uninstall --save-dev [패키지명] |    yarn remove [패키지명]     |
|                 글로벌 패키지 제거                 |  npm uninstall --global [패키지명]  | yarn global remove [패키지명] |
|                      업데이트                      |             npm update              |         yarn upgrade          |
|                  패키지 업데이트                   |        npm update [패키지명]        |    yarn upgrade [패키지명]    |
