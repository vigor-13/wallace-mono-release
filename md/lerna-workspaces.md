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
  5. Yarn workspaces + Lerna

- 1번 방식은 가능은 하지만 굉장히 힘들 것이다.
- 2,3번은 본질적으로 거의 차이가 없다. 단지 클라이언트로 npm을 쓸지 yarn을 쓸지 결정하는 것이 전부다.

  - yarn과 npm 중에 고민이 된다면 다음을 참고하면 도움이 될 것이다.

    - 어떤 명령어를 더 선호하는가? `npm run ~` vs `yarn ~`
    - 표준을 따르고 싶은가 아니면 페이스북을 따르고 싶은가?
    - bootstrapping 시간이 중요한가? 그렇다면 벤치마크 결과를 참고하라.

- 4번 방식은 lerna가 필요하지 않다. yarn에는 기본적으로 모노레포 기능이 탑재되어 있다. lerna와는 다르게 bootstrap 과정도 없고 전용 구성 파일도 필요하지 않다. 오직 pakcage.json에서 `private` 프로퍼티와 `workpsaces` 프로퍼티만 지정해 주면 된다.

- 5번 방식은 4번과 마찬가지로 package.json 설정을하고 lerna.json에 yarn을 사용하도록 설정하면 된다. 또한 bootstrap 과정이 필요없이 yarn을 호출하면 끝이다.
- 5번 방식에서 lerna는 의존성관리와 bootstrapping 과정을 전적으로 yarn-workspaces에 의존한다.

# References

- [Why Lerna and Yarn Workspaces is a perfect match for building mono-repos](https://doppelmutzi.github.io/monorepo-lerna-yarn-workspaces/)
