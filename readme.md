# How to get started Open Source with Node.js

비디오 튜토리얼 소개, 깃허브에서 자바스크립트로 만든 작은 모듈을 개발을 처음부터 끝까지 설명하도록 하겠습니다. 작은 모듈을 실제 프로젝트에 사용되는 유용성 보다는 쉽게 이해하고 테스트 그리고 업데이트가 편한 모듈입니다. 이후 지속적인 업데이트를 통해서 최신 기술을 적용시켜 보도록 하겠습니다. 그리고 깃허브 계정을 만들고 사용하는 방법과 저장소를 활용하는 방법 그리고 그 저장소와 깃을 사용하여 협업하는 방법을 또한 처음부터 소개하도록 하겠습니다. 그리고 마지막으로 제작된 모듈을 npm 에 배포 관리하는 방법까지 알아보도록 하겠습니다

## 1. Introduction Github

### 깃허브 소개와 계정 만들기

- 깃허브(github) 에 대한 간단한 소개와 우리가 왜 깃허브를 통해서 오픈소스를 하는지 이유 소개
- 깃허브 계정 만드는 방법 소개
- 앞으로 과정에서 사용 될 소스 저장소(Repository) 를 간단히 소개

### 라이센스

이 자료는 에그헤드 아이오에 켄트 닷즈의 Kent C. Dodds 오리지널 시리즈 두개의 아웃라인을 원저자의 허락하에 차용하여 제작되었음을 알려드립니다

All of contents and outlines originally written by [@kentcdodds](https://twitter.com/kentcdodds). He so much thanksfully allowed me to it is referred and used in this document and videos in Korean. We would recommend to watch the original videos below if you are familiar with English.

- [How to Contribute to an Open Source Project on GitHub * - Course by @kentcdodds @eggheadio](https://goo.gl/XvuzVU)
- [How to Write an Open Source JavaScript Library * - Course by @kentcdodds @eggheadio](https://goo.gl/Q5FNOM)

### 깃허브 살펴보기

- 저장소 소개, 생성방법
- 팀(Organization) 소개, 생성방법, 페이플랜소개
- 유명 조직/그룹 소개, facebook, GoogleChrome, nodejs, jquery, yeoman, angular, reactjs
- 다른 저장소 살펴보기 (explore)
  - showcase, trending
- 프로파일 (profile)
  - 탑바: 풀리퀘스트, 이슈, gist
  - 상단바: 자기의 저장소, 스타, 팔로워와 퐈로잉
  - 프로파일, 속한팀, 인기 저장소, 컨트리뷰션 달력
  - <div>Icons made by <a href="http://www.flaticon.com/authors/roundicons" title="Roundicons">Roundicons</a> from <a href="http://www.flaticon.com" title="Flaticon">www.flaticon.com</a>

### 저장소 살펴보기

- 저장소 버튼: Watch, Star, Fork(Demo)
- 저장소: 코드(readme, GFM), 이슈, PR, Wiki, Pulse, Graph, Settings

## 2. Setup Development Environments

### Git 개발환경 셋팅하기

- git 을 로컬 머신에 설치확인 (version)
  - git —version
  - 미설치시 https://git-scm.com 로 가서 설치
- git global 정보 설정, 깃 커밋시에 사용자 정보를 글로벌 환경파일에 저장
  - git config —global user.name "Jimmy Moon"
  - git config —global user.email "raging wind@gmail.com"
  - cat ~/.gitconfig | grep -E 'name|email'
- 시스템 [.gitignore](https://help.github.com/articles/ignoring-files/) 설정
  - cat ~/.gitignore
  - https://github.com/github/gitignore
  - mac 으로 검색, 복사, 저장

### SSH 를 이용하여 깃허브에 인증하기

로컬에 설치된 깃과 깃허버를 연동하기 위해서는 깃허브의 인증을 받아야 합니다. 그래야 깃허브에 만들어 놓은 계정과 로컬 깃이 연동되어 실제로 누가 커밋하고 프로젝트 저장소를 관리하는지 깃허브에서 인식할 수 있습니다. 그러기 위해서는 SSH 를 사용해서 인증을 과정을 거쳐야 합니다. 먼저

- ls ~/.ssh 로 현재 생성된 SSH 키가 있는지 확인 합니다. 있다면 기존의 키를 깃허브에 등록시키면 됩니다
- 없다면 SSH 키를 생성해서 깃허브에 등록하도록 하겠습니다. 먼저 설명을 위해서 [저도 새로 키를 발급받도록 하겠습니다](https://help.github.com/articles/generating-an-ssh-key/)
  - 윈도우즈 머신이라면 쉘을 사용할 수 있는 환경을 먼저 만드세요
  - ssh-keygen -t rsa -b 4096 -C ragingwind@gmail.com
  - 계속 엔터, 만약 [패스워드외에 엑스트라 시큐어 레이어](https://help.github.com/articles/working-with-ssh-key-passphrases/)가 필요하다면 값은 입력 하지만 지금은 간단히 계속 진행
- ls ~/.ssh 로 생성된 키 파일들을 확인
- 백그라운드로 ssh-agent 실행, eval "$(ssh-agent -s)"
- 생성된 ssh-key 를 등록, ssh-add ~/.ssh/id_rsa
- 생성된 퍼블릭키를 복사 pbcopy < ~/.ssh/id_rsa.pub
- 프로파일 -> 셋팅 -> SSH and GPG keys => New SSH Key -> 복사한 퍼브릭키 복사 (머쉰이름)
- 깃이 설치된 로컬 머쉰과 깃허브가 연동되는지 확인, ssh -T git@github.com
- 깃허브에서 셋팅화면서 상태 확인

### Node.js 개발환경 셋팅하기

- Node 설치
  - https://nodejs.org
  - https://github.com/tj/n: `npm install -g n`
  - https://github.com/creationix/nvm: `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash`
  - 현재 노드 버전 검사 `node -v`
- [npm config 셋업](https://docs.npmjs.com/misc/config)
  - `npm set init-author-name 'Jimmy Moon'`
  - `npm set init-author-email 'ragingwind@gmail.com'`
  - `npm set init-author-url 'http://ragingwind.me'`
  - `npm set init-license 'MIT'`
  - cat .npmrc
- https://npmjs.com 에 계정생성
- `npm adduser` 를 통해서 npm 유저 등록

## 3. Creating a repository on Github with a new Node.js project

자바스크립트의 업스트림 저장소를 먼저 오거나이저에 생성하고 프로젝트를 간단하게 생성, 셋업한후 이루 제 계정으로 이 저장소를 포크해서 실제로 오픈소스에서 이루어지는 컨리뷰션 과정을 앞으로 보여드리도록 하겠습니다. 그러기 위해서는 먼저 오거나이저에 새로운 간단한 자바스크립트 앱을 위한 저장소를 생성하겠습니다

### 새로운 저장소 생성하기

- 저장소 이름, 설명 입력 후 생성
- 브라우저에 프린트된 생성 스크립트로 초기 커밋

### Node.js 프로젝트 생성하기

- Node.js 프로젝트를 생성한다. npm init

- 리뷰 package.json

- http://editorconfig.org/ 소개와 .editorconfig 생성. editorconfig 는 오픈소스 프로젝트에서 들여쓰기나 라인변경 문자에 때문에 생기는 코드 변화를 줄이기 위해서 사용되는 에디터 플러그인입니다. 대부분의 자바스크립트 프로젝트에서 일괄된 코딩 스타일을 유지하기 위해서 사용되는 필수 플러그인입니다. 여러분들이 사용하시는 대부분의 에디터에서 지원하며 여러분이 선호하는 스타일을 에디터에서 사용하면서 소스코드 변경에는 영향을 주지 않고 오픈소스코드에 기여할 수 있습니다

  ```
  root = true

  [*]
  indent_style = tab
  end_of_line = lf
  charset = utf-8
  trim_trailing_whitespace = true
  insert_final_newline = true

  [*.md]
  trim_trailing_whitespace = false

  [{package.json,.travis.yml}]
  indent_style = space
  indent_size = 2
  ```

- CONTRIBUTING.md 를 추가한다

  ```
  # Setup Project

  - Fork this repository to
  - Clone your repository
  - Run `npm install`

  # Commit Message Rule

  Commit message should be started with present verb not past, second empty line and add more details`
  ```

## 4. Creating the library and adding dependencies

### 메인 프로그램 작성과 추가 모듈 설치

- 프로그램 데이터 파일을 생성한다. `touch codebusking.json`

  ```js
  {
  	firstName: 'Code',
  	lastName: 'Busking
  };
  ```

- 추가 모듈을 설치한다. `npm install --save chalk`

- 메인 소스 파일을 생성후 간단한 코딩을 한다. `touch index.js

  ```js
  'use strict';

  const chalk = require('chalk');
  const codeBusking = require('./codebusking');

  module.exports = {
  	firstName: codeBusking.firstName,
  	lastName: codeBusking.lastName,
  	name: function() {
  		return `${chalk.blue(this.firstName)} ${chalk.red(this.lastName)}`
  	}
  };
  ```

  ​

- REPL 에서 해당 모듈이 동작하는지 확인한다. `const lib = require('./')`

### 깃허브에 프로젝트 커밋, 푸쉬하기

- .gitginore 생성하고, node_modules 와 추가 후 커밋
- git status, git add -A && git commit -a -m 'Add app code'
- git push origin master

## 5. Publishing to npm

### npm 에 퍼블리싱(Publishing) 하기

- 패키지이름 업데이트, package.json 업데이트

- 퍼블리싱, `npm publish`

- 퍼블리싱 정보 확인, `npm info codebusking`

- 테스트용 프로젝트 생성, `npm install codebusking`

  ```js
  const codeBusking = require('codebusking');

  console.log(codeBusking.name());
  ```

- npmjs.com/codebusking 에서 실제 모듈 확인, 유저, 깃허브 주소, 버전 그리고 라이센스

### 깃허브에 릴리즈 버전 태깅하기

npm publish 를 통해서 릴리즈 된 버전을 태킹하여 깃허브에 [태그 정보](https://docs.npmjs.com/cli/dist-tag)를 커밋할 수 있습니다. 이렇게 발행된 태그 버전은 히스토리에서 특정 시점을 명시할 수 있습니다. 대부분 릴리즈 포인트로 사용됩니다. 발행된 태그를 통해서 사용자는 얼마든지 이전 특정 버전을 사용할 수 있으며 깃허브에서는 추가적인 릴리즈 정보를 제공할 수 있습니다.

- git tag 1.0.0
- git push —tags
- 깃허브의 tags와 릴리즈에서 발행된 버전 확인
- Draft Release 에 릴리즈 정보를 추가, 타이틀, 설명
  - 참고로 보여줄 자료 https://github.com/electron/electron/releases

## 6. Publishing a new version to npm

### npm 에 새로운 버전 발행 하기

새로운 기능이 추가되거나 사용하는 디펜던시 모듈이 업데이트가 되는 경우추가 버전이 발행해야 합니다. 새로운 버전 발행은 변경/추가되는 기능에 따라서 업데이트 되어야 합니다. 자바스크립트/노드에서는 각 버전별로 의미를 가지는 [시멘틱 버저닝](https://goo.gl/3qWJ)을 사용하고 있으며 추가로 Range 버전명을 사용해서 디펜던시 버전을 관리합니다.

- [JSConf Budapest: what everybody should know about npm by seldo](https://goo.gl/COVSRg)
  - 메이저 버전 업데이트는 주로 API 나 기능의 큰 변화의 경우
  - 마이너 버전은 단순 기능 API 추가의 경우
  - 패치 버전은 버그 픽스나 마이너한 패치의 경우에 사용됩니다


- Range syntax
  - X-Range: x 또는 * 가 명시된 버전의 모든 버전을 허용 1.x := >=1.0.0 < 2.0.0, 1.2.x := >= 1.2.0 < 1.3.0
  - Tild Range: ~ 은 패치-레벨의 변화를 위해서 사용된다. 명시된 버전이 최대한 버전업 할 수 있을까지만 허용한다. 버전을 명시해서 주로 마이너 체인지만 받을 때 사용, ~1.2.3 은 최대 1.3.0, ~0.2.3 dms 0.3.0 미만
  - Caret Range: 왼쪽의 논-제로 버전을 업데이트 하지 않는 한에서 업데이트 최대한 변화를 허용할 수 있다. 예를 들어 메이저 버전을 명시하면 다음 메이저 버전까지 업데이트 가능 ^1.2.3 은 최대 2.0.0 이전 버전. ^0.2.3 은 0.3.0 미만 그리고 특이하게 ^0.0.3 은 0.0.4 이전까지임으로 업데이트가 힘들다
- [npm semantic version calculator](https://goo.gl/Bbxu6K)
- 추가 기능 업데이트 email
- 변경사항 추적, `git diff`
- 변경사항 커밋, `git add -A && git commit -a -m ''`
- 태깅, `git tag 1.1.0`
- 깃허브에 푸시, `git push origin master —tags`
- npm 에 새로운 버전 발행, `npm publish`
- npm 정보 확인, `npm info codebusking`

### npm 에 베타 버전 발행하기

[프리릴리즈(prerelease-tags)](https://docs.npmjs.com/misc/semver#prerelease-tags) 를 사용하여 지정된 버전에 대한 프리플리즈 버전들을 사용할 수 있습니다. 보통 베타 테스트를 위해서 빠르게 자주 업데이트 되거나 실험적인 기능을 추가하는 용도로 사용됩니다. 실제로 프리릴리즈 테크가 붙은 경우에는 사용자의 주의를 환기 시키는 역활도 합니다

- 코드 업데이트, 홈페이지 (임시사이트)
- bumpup to `1.2.0-beta.0`
- 변경사항 추적, git diff
- 변경사항 커밋, `git add -A && git commit -a -m ''`
- 태깅, `git tag 1.2.0-beta.0`
- 깃허브에 푸시, `git push origin master -—tags`
- npm 에 새로운 베타 버전 발행, `npm publish —tag beta`
- 베타 버전 확인, `npm info codebusking`
- 베타 버전 테스트를 위한 테스트 앱, `npm install codebusking@beta` 로 실제 베타 버전 설치 되는지 확인

## 7. Unit Testing with AVA

오픈소스 프로젝트는 여러 개발자들이 동시에 많은 기능을 개발하기 때문에 유닛테스트는 필수입니다. 자바스크립트에서는 지금 사용할 에이바 말고도 모카, 차이등 여러가지 유니테스트 프레임웍이 있으니 사용해보세요. 에이바는 최근에 나온 유닛테스트 프레임웍 중에 하나이며 ES2015 을 사용 할 수 있으며 빠른 테스트 성능을 보장합니다

- AVA 를 데브디펜턴시에 설치 후 확인, `npm install --save-dev ava`
- 테스트 코드 생성, make a test.js
- 최초 테스트 코드 작성
- npm test 스크립트 수정 확인, `"test": "ava"`
- 테스트 스크립트를 실제 테스트 코드로 업데이트

## 8. Releasing with TravisCI

### [Travis CI](https://travis-ci.org/)

오픈소스 프로젝트에 유닛테스트를 작성했으면 이제 CI 툴을 사용할 수 있습니다. 앞으로 컷밋등으로 인해서 소스코드가 변경되면 프로젝트의 빌드가 깨지거나 테스트를 통과하지 못해서 결함이 발견되었는지 지속적으로 확인할 수 있습니다. 깃허브에서는 외부의 CI 툴을 사용하도록 설정하면 해당 리포지토리에 PR 이나 커밋등이 추가되는 경우 자동으로 테스트를 해서 그 결과를 리포팅 해줍니다. 이후 테스트 코드가 얼마나 잘 반영되었는지 알 수 있는 코드 커버리지를 사용하려면 CI 서비스의 테스팅 패스는 필수입니다. 테스트 코드를 바탕으로 테스트 코드를 검사해서 리포팅을 해주기 때문입니다.

-   먼저 .travis.yml 추가, 기본 적인 코드 작성하기

    ```yaml
    sudo: false
    language: node_js
    node_js:
    - v4
    - v5
    ```
  ```

- Travis CI 에서 계정 생성 후 리포지터리 연동 활성화

- 커밋 후 푸쉬하여 테스트 코드가 도는 지 확인

- node 의 새로운 버전 추가, `  -v7`

## 9. Adding Code Coverage Reporting

### Code Coverage 사용하기

코드 커버리지는 작성된 테스트 코드가 모듈의 API 를 얼마나 잘 커버하고 있는지, 즉 테스트 코드가 충실히 작성되었는지 확인하는 툴입니다. 작성된 API 에 임의의 코드들을 추가하여 테스트 코드에서 호출이 되었는지등을 판단해서 리포팅을 해줍니다. 코드 커버리지는 두가지 파트로 나뉩니다. 실제 코드 커버리지를 테스트 하는 툴과 생성된 리포트를 받아서 다양한 데이터를 보여주고 깃허브와 연동할 수 있는 써드파티 서비스입니다. 

- Istanbul 페이지 가기: 여기에서는 [Istanbul Code Coverage · GitHub](https://goo.gl/F9yICG) 에서 제공하는 niece CLI 툴을 사용할 예정입니다. 빠르고 간단하며 AVA 테스트 프레임웍을 지원합니다
- 커버올아이오 페이지 가기: 이제 CI 에서 전송된 리포팅 결과를 받아서 보여주고 커버리지에 관련된 여러가지 정보를 제공해주는 서드파티 서비스인 커버올 아이오를 사용할 것입니다. 
- 커버올아이오 페이지, 가입, 리포팅을 보내고 연동하고자 하는 깃허브 리포지토리를 활성화
- nyc 와 커버올 클라이언트 설치:`npm install —save-dev nyc coveralls`
- 테스트 스크립트 수정: `"test": "nyc ava"
- 테스트 스크립트 실행: `npm test`

- travis.yml 업데이트:

  ```yaml
  after_success:
    - './node_modules/.bin/nyc report --reporter=text-lcov | ./node_modules/.bin/coveralls'
  ```

- .gitignore 업데이트: .nyc_output 추가

- 커밋, 푸쉬후 CI 로그와 CC 결과 확인

## 10. How to fork and clone a Github Repository

### 생성된 저장소 포크(Fork) 하기

- 먼저 CONTRIBUTING.md 를 읽습니다. 그에 따라 다른 프로젝트의 CONTRIBUTING.md 도 리뷰해봅니다
  - [angular/CONTRIBUTING.md at master · angular/angular](https://goo.gl/XRbkrM)
  - https://github.com/facebook/react
  - https://github.com/yeoman/generator-chrome-extension/pull/117


- fork 하기
- clone 하기, git clone https://github.com/ragingwind/node-codebusking.git node-codebusking-fork
- upstream 등록, git remote add upstream https://github.com/codebusking/node-codebusking.git
- upstream 의 최신 데이터 갱신, `git fetch upstream`
- 로컬 저장소의 master 브랜치를 upstream/master 로 셋팅: upstream 의 모든 변경 사항을 master 로 가져오도록 설정, `git branch --set-upstream-to=upstream/master master or -u`
- 현재 마스터에, upstream 데이터 가져오기: `git pull`

### 로컬 프로젝트 셋팅하기

- 컨티르뷰팅의 다음 단계인 브렌치 생성: `git checkout -b update-homepage`


- 개발환경 셋팅: `npm install`
- 테스트 코드 동작확인: `npm test`

## 11. How to creat a PR request on Github

### 깃허브에서 첫 PR 요청을 만들기

- 먼저 upstream 에 이슈를 등록: `Update official website` and description
  - 어떻게 구현할 것인지 코드 보여준다
  - 다른 사람이 동의 하는 내용 추가
- 추가 정보를 리턴하는 코드 작성
- 추가 정보를 리턴하는 API 를 테스트 하는 코드 작성: `npm test -- --watch`
- 코드 커버리지 확인: `npm test`
- 오리진에 커밋, 푸쉬: `git push origin update-homepage`
- 깃허브 페이지에서 PR 작성하여 전달
- 관련된 서드파티 어플리케이션의 동작 확인과 리뷰를 받음
- 관련 이슈 기록을 남기고 이슈 닫음

### 로컬 레파지토리에 최근 변경사항 적용하기

여러 컨트리뷰터로 부터 머지된 변경 사항을 현재 작업중인 브랜치에 머지해보도록 하겠습니다. 이 경우에 같은 파일의 변경사항이 충돌이 나는 경우가 흔히 있습니다. 

- PR 된 커밋 가져오기: `git fetch upstream && git rebase upstream/master`

### PR 요청 업데이트 하기

- 코드 인티그레이션 작업 반복:
  - 코드리뷰, 추가기능, 덧댄 변경 사항을 수정 그리고 테스트
  - 오리진에 커밋, 푸쉬: `git push origin update-homepage`
  - 여러개의 커밋이 생길 수 있음

## 12. How to update a Pull Request on Github

### 여러 커밋들을 한개의 커밋으로 정리하기

오픈소스에서는 하나의 이슈의 하나의 커밋을 통상적으로 요구합니다. 커밋로그 관리나 롤백등 리스토리 관리 측면에서 유용하기 때문입니다. 그래서 로컬에서 작업한 모든 싱글 커밋을 모아서 PR 을 보낸다면 그것을 한개의 커밋, 영어로는 Squash  해줄 것을 요청하는 경우가 많습니다.

- 이슈에서 중복된 커밋을 스쿼쉬(squash) 해 줄 것을 요청
- 커밋메세지 squash: git rebase -i HEAD~2 또는 커밋 아이디
- 변경 사항을 모두 기록하고 싶다면 세켠 라인에 추가 정보를 모두 남겨둔다
- git 히스토리가 변경 됨으로: `git push origin update-homepage --force

### PR 충돌 해결

- PR 된 커밋 가져오기: `git fetch upstream && git rebase upstream/master`

- 본래는 `git stash` 명령을 통해서 현재 변경 사항을 감추지만: `git stash`, `git stash pop/drop`
- 간단한 충돌의 경우 수정 후 merge 를 할 수 있습니다
- 충돌나는 부분 수정 후 적용: `git add .`
- rebase 계속 진행: `git rebase --continue` / `git rebase —abort`
- git log 로 히스토리가 정리가 되었는지 확인
- git 히스토리가 변경 됨으로: `git push origin update-homepage --force

### 적용된 PR 확인

- 레포지토리의 contribution 탭 확인 어떤 변경사항을 주었는지 통계로 확인한다

### 최신 버전 발행

- 최신 버전을 발행을 요청하고 발행한다: tagging and npm publish