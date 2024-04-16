# 자바 - 학점 계산기

- [기능 요구사항](#기능-요구사항)
- [입출력 요구사항](#입출력-요구사항)
    - [입력](#입력)
    - [출력](#출력)
    - [실행결과 예시](#실행결과-예시)
- [프로그래밍 요구사항](#프로그래밍-요구사항)
    - [테스트 실행 가이드](#테스트-실행-가이드)
    - [라이브러리](#라이브러리)
- [과제 진행방식](#과제-진행방식)

---

## 기능 요구사항

전공/교양 과목명과 학점, 성적을 입력하면 평점평균을 계산하는 CLI 기반 학점 계산기를 구현하라.

- `과목명`은 공백 포함 10자 이내이며, 공백만으로 구성될 수 없다.
- `과목학점`은 아래와 같이 1학점부터 4학점까지 존재한다.

  | 학점 | 1 | 2 | 3 | 4 |
  |----|---|---|---|---|

- `과목성적`은 크게 `ABCDF 과목`과 `P/NP 과목`으로 구분된다.
    - `ABCDF 과목`은 성적을 A부터 F까지 부여하며, 9가지 등급이 존재한다.
    - `P/NP 과목`은 성적을 P와 NP 두 가지 등급으로 부여한다.
    - F 또는 NP 성적을 받은 과목의 학점은 `취득학점`에 포함되지 않는다.

      | 성적 | A+  | A0  | B+  | B0  | C+  | C0  | D+  | D0  | F | P    | NP         |
      |----|-----|-----|-----|-----|-----|-----|-----|-----|---|------|------------|
      | 평점 | 4.5 | 4.0 | 3.5 | 3.0 | 2.5 | 2.0 | 1.5 | 1.0 | 0 | Pass | Not Passed |

- `평점평균` 계산 공식은 다음과 같다.
    - `평점평균` = `과목성적가중치의 총합` / `과목학점의 총합`
    - `과목성적가중치` = `과목평점` * `과목학점`
    - 평점평균은 소수점 셋째 자리에서 반올림하여 둘째 자리까지 표현한다.
    - `P/NP 과목`은 평점평균 계산에서 제외한다.

- 평점평균을 출력한 후에는 애플리케이션을 종료한다.
- 사용자가 잘못된 값을 입력할 경우 `IllegalArgumentException`을 발생시키고 애플리케이션을 종료한다.

## 입출력 요구사항

### 입력

- 과목 정보(`<과목명>-<학점>-<성적>`)
- 과목 정보는 쉼표(,)를 기준으로 구분한다.

```
데이타구조-3-A0,자바프로그래밍언어-3-B+,컴퓨터구조-3-C0,컴퓨터네트워크-3-D+
```

### 출력

- 취득학점

```
<취득학점>
15학점
```

- 평점평균(전공, 교양 과목 모두 포함)

```
<평점평균>
2.36 / 4.5
```

- 전공 평점평균(전공 과목만 포함)

```
<전공 평점평균>
2.75 / 4.5
```

### 실행결과 예시

```
전공 과목명과 이수학점, 평점을 입력해주세요(예시: 프로그래밍언어론-3-A+,소프트웨어공학-3-B+):
데이타구조-3-A0,자바프로그래밍언어-3-B+,컴퓨터구조-3-C0,컴퓨터네트워크-3-D+

교양 과목명과 이수학점, 평점을 입력해주세요(예시: 선형대수학-3-C0,인간관계와자기성장-3-P):
미술의이해-3-P,교양특론3-1-NP,기독교의이해-2-F

<취득학점>
15학점

<평점평균>
2.36 / 4.5

<전공 평점평균>
2.75 / 4.5
```

## 프로그래밍 요구사항

- JDK 17 버전에서 실행 가능해야 한다.
- 프로그램 실행의 시작점은 `Application`의 `main()`이다.
- `build.gradle` 파일을 변경할 수 없고, 외부 라이브러리를 사용하지 않는다.
- [Java 코드 컨벤션](https://google.github.io/styleguide/javaguide.html) 가이드를 준수하며 프로그래밍한다.
- 프로그램 구현이 완료되면 `ApplicationTest`의 모든 테스트가 성공해야 한다.
- 프로그래밍 요구 사항에서 달리 명시하지 않는 한 파일, 패키지 이름을 수정하거나 이동하지 않는다.

### 테스트 실행 가이드

- 터미널에서 `java -version`을 실행하여 Java 버전이 17인지 확인한다.
  Eclipse 또는 IntelliJ IDEA와 같은 IDE에서 Java 17로 실행되는지 확인한다.
- 터미널에서 Mac 또는 Linux 사용자의 경우 `./gradlew clean test` 명령을 실행하고,
  Windows 사용자의 경우 `gradlew.bat clean test` 또는 `./gradlew.bat clean test` 명령을 실행할 때 모든 테스트가 아래와 같이 통과하는지 확인한다.

```
BUILD SUCCESSFUL in 0s
```

### 라이브러리

- `camp.nextstep.edu.missionutils`에서 제공하는 `Console` API를 사용하여 구현해야 한다.
    - 사용자가 입력하는 값은 `camp.nextstep.edu.missionutils.Console`의 `readLine()`을 활용한다.

```java
import static camp.nextstep.edu.missionutils.Console.readLine;

import camp.nextstep.edu.missionutils.Console;

// ...

String input = Console.readLine();
```

## 과제 진행방식

- 과제는 이 저장소를 Fork & Clone 해 시작한다.
- 기능을 구현하기 전에 구현할 기능 목록을 `docs/README.md`에 정리한다.
    - 작성 양식은 자유이나, 필요한 경우 [마크다운](https://github.com/jinkyukim-me/markdown_ko) 문법을 참고한다.
- 구현이 완료되면 이 저장소에 Pull Request 를 보내 과제를 제출한다.
    - PR 제목은 `홍길동 과제 리뷰 요청합니다.` 형식으로 작성한다.
    - PR 본문에는 자유 형식으로 과제에 대한 소감(회고)을 작성한다.
    - 과제 진행중에 궁금한 점은 깃허브 `Discussions`을 활용해 질문한다.

---

**"이 과제는 [우아한테크코스](https://www.woowacourse.io)에서 제공하는 프리코스 미션을 바탕으로 설계되었습니다."**
