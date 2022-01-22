![shake-hands](../images/books.png)

# Lerna로 배포하기

[back to README.md](../README.md)

# 개요

- Lerna를 사용해서 배포하는 방법을 자세히 알아보자.

# 기본 명령어 (`lerna publish`)

- 패키지들을 배포한다.

  ```besh
  # 마지막 릴리즈 이후 변경된 패키지들을 배포한다.
  lerna publish

  # 현재 커밋에서 태그가 지정된 패키지를 명시적으로 배포한다.
  lerna publish from-git

  # 레지스트리에 최신 버전이 없는 경우 패키지를 명시적으로 배포한다.
  lerna publish from-package
  ```

  - 마지막 릴리즈 이후 업데이트된 패키지를 배포한다. (내부적으로 `lerna version`을 호출함.)
  - 현재 커밋에서 태그가 지정된 패키지를 명시적으로 배포한다. (from-git 옵션)
  - 레지스트리에 버전이 없는 최신 커밋의 패키지를 배포한다. (from-package 옵션)

- Lerna는 package.json에 `private` 속성이 true인 패키지는 배포하지 않는다.

- lifecycle scripts가 root 그리고 각각의 패키지에서 실행된다. (`--ignore-scripts` 옵션을 사용하여 제외할 수 도 있다.)

# References

- [Lerna Github](https://github.com/lerna/lerna/blob/main/commands/publish/README.md)
