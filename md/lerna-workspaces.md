![shake-hands](../images/shake-hands.png)

# Lerna & Yarn worksapces

[back to README.md](../README.md)

# 개요

- Lerna와 Yarnk workspaces는 상호보완적으로 사용할 수 있다.

# NPM / Yarn / leran

- NPM과 Yarn 그리고 Lerna가 서로 어떤 관계인지 파악해보자.

- `NPM / Yarn`

  - 네이티브 패키지 관리자이며 서로 공통된 기능이 많다.
  - yarn을 사용하는 이유는 yarn이 npm 보다 더 빠르고 기능이 많기 때문이다.
  - 현재는 npm과 yarn의 격차가 많이 줄어들었고 기능적으로도 거의 동일한 기능을 제공한다. (버전 관리 방식도 동일함)
  - 가장 큰 차이점은 workspaces기능이었지만 이것도 최근 NPM에서 거의 동일한 기능을 제공하고 있다.

- `네이티브 모노레포?`
  - 모노레포 기능을 제공하는 툴은 대표젹으로 3가지가 있다. (`yarn-workspaces`, `lerna`, `bolt`)
  - 위의 3가지 툴 중에서 네이티브 모노레포 툴은 `yarn-workspaces`가 유일하다.
  - lerna는 yarn-workspaces가 나오기도 전에 먼저 모노레포 기능을 제공했지만 user-land 수준이었다.
  - lerna는 모노레포 기능을 제공하기 위해서 자체적으로 `semantic link`라는 기술을 사용고 있지만 모노레포와 관련된 기능은 전체적으로 yarn-workspaces가 제공하는 네이티브 기능으로 대체하여 사용할 수 도 있다.
  - lerna는 모노레포 관리 이상의 기능을 제공한다. 예를들어 각각의 패키지별로 버전관리와 배포를 할 수 있도록 도와주는 여러 세부적인 기능을 제공한다. 반면 yarn-workspaces는 오직 모노레포 워크플로에 관련한 기능만을 제공한다.
  - bolt는 비교적 최근에 시작된 프로젝트로 yarn-workspaces를 기반하고 있으며 leran에서 영감을 받았다고 한다. 목표는 lerna 보다 더 많은 기능을 제공하는 것이지만 활발하게 활동이 이루어지고 있지는 않다.

# 모노레포를 구성하는 여러가지 방법들

- 아래의 3가지 중 원하는 방식을 택하면 된다.

  1. 수동으로 구성하기
  2. NPM + Lerna
  3. Yarn + Lerna
  4. yarn workspaces
  5. **Yarn workspaces + Lerna**

- 1번 방식은 가능은 하지만 굉장히 힘드므로 추천하진 않는다.
- 2,3번은 본질적으로 거의 차이가 없다. 단지 클라이언트로 npm을 쓸지 yarn을 쓸지 결정하는 것이 전부다. 거의 Lerna 단독 사용이나 다름 없다.

  - yarn과 npm 중에 고민이 된다면 다음을 참고하면 도움이 될 것이다.

    - 어떤 명령어를 더 선호하는가? `npm run ~` vs `yarn ~`
    - 표준을 따르고 싶은가 아니면 페이스북을 따르고 싶은가?
    - bootstrapping 시간이 중요한가? 그렇다면 벤치마크 결과를 참고하라.

- 4번 방식은 Lerna가 필요하지 않다. yarn에는 기본적으로 모노레포 기능이 탑재되어 있다. Lerna와는 다르게 bootstrap 과정도 없고 전용 구성 파일도 필요하지 않다. 오직 pakcage.json에서 `private` 프로퍼티와 `workpsaces` 프로퍼티만 지정해 주면 된다.

- 5번 방식은 4번과 마찬가지로 package.json 설정을하고 lerna.json에 yarn을 사용하도록 설정하면 된다. 또한 bootstrap 과정이 필요없이 yarn을 호출하면 끝이다.
- 5번 방식에서 lerna는 의존성관리와 bootstrapping 과정을 전적으로 yarn-workspaces에 의존한다.
- 5번 방식의 워크플로를 요약해보면 다음과 같다.

  1. 모노레포와 관련된 워크플로(의존성 관리)는 전적으로 yarn-workspaces를 사용한다.
  2. 나머지 패키지 관리 요구사항(e.g. 선택적 테스트 스크립트 실행 등...)들은 Lerna를 활용해서 최적화 한다.
  3. Lerna는 버전관리, 배포와 관련된 세부적인 기능을 제공하므로 이를 활용한다.

# Yarn-workspaces와 Lerna 사용법 알아보기

## Yarn-workspaces

- 패키지들간 종속성 관리외에 다른 기능을 제공하지 않는다.
- Yarn을 기반으로 작동하기 때문에 Yarn의 기본 기능들을 모두 사용할 수 있다.
- 모노레포 환경에서만 작동하는 몇 가지 추가 명령어가 있다.

  ```shell
  # 현재 프로젝트의 의존성 트리를 보여준다.

  yarn workspaces info
  ```

  ```shell
  # 선택한 내부 패키지의 명령어를 실행한다.

  yarn workspace <package-name> <command>
  ```

  ```shell
  # 선택한 내부 패키지에 의존성을 추가, 제거한다.

  yarn workspace <package-name> add react --dev
  yarn workspace <package-name> remove react
  ```

  ```shell
  # 모든 패키지에 적용할 공통 의존성을 설치한다.

  yarn add <some-package> -W
  ```

- 내부 패키지들간에 종속성을 추가하려면 버전 번호를 반드시 명시해야한다. 그렇지 않으면 외부 저장소에서 패키지를 찾게된다.

  ```shell
  yarn workspace @my0project/awesome-app add @my-project/awesome-components@0.1.0
  ```

- yarn-workspaces는 종속성을 해당 패키지의 node_modules에 추가하지 않고 root 경로의 node_modules에 호이스팅한다. 이때 심볼링크를 사용하여 종속성을 관리하므로 중복되는 의존성들은 한번만 설치된다.

- 만약 외부 패키지가 모노레포 환경을 지원하지 않는다면 `nohoist` 기능을 사용하면 된다.

  ```shell
  // package.json
  {
    ...
    "workspaces": {
      "packages": ["packages/*"],
      "nohoist": [
        "**/react-native"
      ]
    }
    ...
  }
  ```

## Lerna

- Lerna는 자체적으로 모노레포 기능을 제공한다.
- Lerna를 yarn 또는 npm과 사용하는 경우 자체 모노레포 기능을 사용하며 bootstrap을 해야한다.
- Lerna를 yarn-workspaces와 사용하는 경우 모노레포와 관련된 기능을 전적으로 yarn-workpsaces에게 의존한다.
- Lerna의 기본 명령어 몇 가지를 살펴보자.

  ```shell
  # 모든 패키지에 공통 종속성을 설치한다.

  lerna add react
  ```

  ```shell
  # 특정 패키지에 종속성을 설치한다.

  lerna add react --scope <my-package>
  ```

  ```shell
  # 공통 종속성을 설치하고 특정 패키지에서만 버저닝을 한다.

  lerna add react@16.0.0 --scope <my-package>
  ```

  ```shell
  # 공유 종속성을 호이스팅 한다.

  lerna add react -D --hoist
  ```

- Lerna에는 몇가지 필터링 옵션이 있으니 참조하도록 한다. [link](https://github.com/lerna/lerna/tree/main/core/filter-options)

- Lerna의 --scope 옵션을 사용해서 특정 패키지 테스트를 실행할 수도 있다.

  ```json
  // package.json
  {
    ...
    "scripts": {
      "test": "lerna exec yarn test"
    }
    ...
  }
  ```

  ```besh
  yarn test --scope @my-project-services/*
  yarn test --scope @my-project/web-*
  ```

# References

- [Why Lerna and Yarn Workspaces is a perfect match for building mono-repos](https://doppelmutzi.github.io/monorepo-lerna-yarn-workspaces/)
- [Monorepos By Example: Part 1](https://codeburst.io/monorepos-by-example-part-1-3a883b49047e)
- [Monorepos By Example: Part 2](https://codeburst.io/monorepos-by-example-part-2-4153712cfa31)
