![ganesha](../images/ganesha.png)

# Monorepo & Lerna

[back to README.md](../README.md)

# 개요

- 모노레포는 언뜻 보기에 최근 개발 트렌드(모듈화, 마이크로서비스 ...)와 맞지 않아 보이지만 그렇지 않다.
- 모노레포는 단일 저장소에서 여러 모듈 패키지를 관리하는 것을 말하며 이를 통해서 모듈식 소프트웨어의 개발 프로세스를 크게 단순화 할 수 있다.
- 모노레포를 사용하면 많은 이점이 있지만 동시에 문제점도 있는데 배포가 까다롭다는 점이 그 중 하나이다. 이러한 문제점들을 해결하기 위해서 babel 프로젝트의 개발자들은 모노레포 기반 프로젝트의 배포 워크플로를 도와줄 `Lerna`라는 도구를 만들었다.

# Monorepo란?

- 여러 가지 프로젝트의 코드를 관리하는 단일 저장소이다.
- 모노레포에서 관리되는 프로젝트는 서로 의존성이 있을 수도 있지만 전혀 관련이 없을 수도 있다.

# Monorepo의 장점

- 코드베이스 구축 및 테스트와 같은 작업을 위해 작성해야 하는 반복적인 코드의 양을 줄일 수 있다.
- 재사용되는 코드를 여러 프로젝트에 공유하기 좋다.
- 대규모 리펙토링이 쉬워진다.
- 팀간의 협업에 도움이된다.

# Monorepo의 단점

- 다량의 프로젝트를 한 곳에서 관리하기 때문에 처음 코드를 접하는 신규 개발자가 접근하기 어려워진다.
- 저장소의 크기가 기가바이트 단위로 커지게 될 경우 성능 문제를 유발할 가능성이 있다. (페이스북, 구글과 같은 대기업들은 이러한 문제를 해결했지만 중소기업이나 개인은 해결하기 어려울 수 있다.)
- 현재 대부분의 소스 제어 시스템은 모노레포를 관리하기에 적합하지 않다. 전체적인 접근 관리와 코드 베이스의 특정 부분에 접근을 제한 하는 기능들은 구현이 불가능할 수도 있다.
- 기존의 빌드 프로세스와 통합하는 것도 쉽지 않다.

# Lerna

- Lerna는 Git과 NPM을 사용해서 모노레포의 워크플로를 최적화해주는 도구이다.

## 버전관리 (lerna version)

- Lerna는 2가지 방식으로 버전관리를 한다.

  1. `fixed` : 중앙에서 버전 관리를 하며 내부의 모든 패키지가 동일한 버전을 공유한다.
  2. `independent` : 패키지별로 독립적으로 버전을 관리한다.

## 기존 저장소 가져오기 (lerna import)

- 기존의 멀티레포들을 모노레포로 전환할 때 기존의 Git 히스토리를 잃고 싶지 않은 경우 `lerna import`를 사용한다.
- 기존의 저장소를 새 모노레포의 패키지 경로로 옮길 수 있다.

## 기본 Lerna 워크플로 (lerna bootstrap ~ lerna publish)

- Lerna를 구성한 후 하나 이상의 패키지를 추가한 다음 `lerna bootstrap`을 실행한다.
- 이 명령은 패키지 디렉토리의 모든 패키지를 검색한 후 관련된 종속성을 처리한다.
- 만약 내부 패키지들이 서로간의 종속성이 있는 경우 `node_modules` 디렉토리에 symlink 생성한다.
- 마지막으로 `lerna publish`로 npm에 퍼블리싱한다.

# References

- [Why Lerna and Yarn Workspaces is a perfect match for building mono-repos](https://doppelmutzi.github.io/monorepo-lerna-yarn-workspaces/)
- [Monorepos in the Wild](https://medium.com/@maoberlehner/monorepos-in-the-wild-33c6eb246cb9)
