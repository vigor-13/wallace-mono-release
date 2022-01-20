![shake-hands](../images/shake-hands.png)

# Lerna & Yarn worksapces

[back to README.md](../README.md)

# 개요

- Lerna와 Yarnk workspaces는 상호보완적으로 사용할 수 있다.

# NPM & Yarn & Yarn-workpsaces & leran

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
  - 하지만 lerna는 모노레포 관리 이상의 기능을 제공한다. 예를들어 각각의 패키지별로 버전관리와 배포를 할 수 있도록 도와주는 여러 세부저인 기능을 제공한다. 반면 yarn-workspaces는 모노레포 워크플로에 관련한 기능만을 제공한다.

# References

- [Why Lerna and Yarn Workspaces is a perfect match for building mono-repos](https://doppelmutzi.github.io/monorepo-lerna-yarn-workspaces/)
