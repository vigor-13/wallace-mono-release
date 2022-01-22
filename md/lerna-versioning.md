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

# References

- [Lerna Github](https://github.com/lerna/lerna/blob/main/commands/version/README.md)
