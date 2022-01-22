![shake-hands](../images/cars.png)

# Lerna로 버전 관리하기

[back to README.md](../README.md)

# 개요

- Lerna가 제공하는 버전 관리 기능을 자세히 알아보자.

# 기본 명령어 (`lerna version`)

- 마지막 릴리즈 이후 변경된 패키지(들)의 버전을 범핑한다.

  ```besh
  # 명시적으로 버전 업
  lerna version 1.0.1

  # semver 키워드를 사용하여 버전 업
  lerna version patch

  # prompt에서 선택하여 버전 업
  lerna version
  ```

  1. 태그가 지정된 이전 릴리즈 이후에 업데이트된 패키지를 식별한다.
  2. 새 버전 입력을 위해서 propmt를 실행한다.
  3. 새 릴리즈를 반영할 수 있도록 패키지의 메타데이터를 수정한 후 루트 및 패키지 단위로 적절한 lifecycle 스크립트를 실행한다.
  4. 변경 사항을 커밋하고 태그를 지정한다.
  5. 리모트 저장소에 푸시한다.

# References

- [Lerna Github](https://github.com/lerna/lerna/blob/main/commands/version/README.md)
- [Git tag](https://backlog.com/git-tutorial/kr/stepup/stepup4_1.html)
