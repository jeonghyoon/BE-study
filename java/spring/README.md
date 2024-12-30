## [인프런 - 스프링 입문 ~ 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술](https://www.inflearn.com/course/스프링-입문-스프링부트)

### 섹션 1. 강의 소개 : 2개 (5분)

- 강의 소개 05:02

  <details>
    <summary>강의 자료</summary>

  ```markdown
  # 버전 수정 이력

  ## v2024-01-20

  - MemoryMemberRepositoryTest 코드 오류 수정(qdlsungls님 도움)

  ## v2023-11-27

  - 스프링 부트 3.2 업데이트 관련 이슈

  - start.spring.io 스프링 부트 2.x 지원 종료

  - 스프링 부트 3.0 이상을 사용해주세요.

  - 자바 17 이상을 사용해주세요.

  - 강의 메뉴얼 분할

  - 강의 메뉴얼 링크

  ### v2023-08-16

  - 메뉴 링크 이동

  ## v2022-11-28

  - 스프링 부트 3.0 내용 추가

  - 프로젝트 선택에서 `Gradle - Groovy` 추가

  ## v2022-09-04

  - 오타 `helloConroller` -> `helloController` (hswkd9895님 도움)

  - 코드 오타 `template/` -> `templates/` (anthologia님 도움)

  ## v2021-12-01

  _주의!_

  h2 데이터베이스는 꼭 다음 링크에 들어가서 _1.4.200_ 버전을 설치해주세요.

  최근에 나온 2.0.206 버전을 설치하면 일부 기능이 정상 동작하지 않습니다.

  https://www.h2database.com/html/download-archive.html

  만약 이미 설치하고 실행까지 했다면 다시 설치한 이후에 _~/test.mv.db_ 파일을 꼭 삭제해주세요.

  그렇지 않으면 다음 오류가 발생하면서 접속되지 않습니다.

  General error: "The write format 1 is smaller than the supported format 2 [2.0.206/5]" [50000-202] HY000/50000

  ## v2021-07-18

  스프링 부트 최신 버전 선택 설명 추가

  ## v2021-03-03

  - 윈도우 사용자는 h2.bat 실행 추가

  ## v2021-02-11

  - 회원 리포지토리 테스트 케이스 작성에서 result, member 위치 변경

  - 도움 주신 분 : 박동훈님

  ## v1.7 - 2020-11-23

  - 스프링부트 2.4 에서 데이터베이스 커넥션 오류 해결방안 추가

  - 스프링부트 2.4부터는 `spring.datasource.username=sa`를 꼭 추가해주어야 한다. 그렇지 않으면 `Wrong user name or password` 오류가 발생한다.

  - [Databases that support embedded and non-embedded modes are always detected as embedded by somayaj · Pull Request #23693 · spring-projects/spring-boot · GitHub](https://github.com/spring-projects/spring-boot/pull/23693)

  ## v1.6 - 2020-10-14

  - helloController -> memberController 이미지 오류 수정 (도움주신분: 최성규님)

  ## v1.5 - 2020-10-10

  - IntelliJ JDK 설치 확인 추가

  ## v1.4 - 2020-09-18

  - 인텔리J 커뮤니티(무료) 버전에서 `application.properties` 파일에서 키가 회색으로 인식 설명

  ## v1.3 - 2020-09-07

  - 윈도우 gradlew.bat -> gradlew로 변경

  ## v1.2 - 2020-08-28

  - 윈도우 사용자를 위한 IntelliJ 단축키 조회 방법 추가

  ## v1.1 - 2020-08-28

  - 윈도우 사용자를 위한 도움 추가

  윈도우에서 맥의 iTerm이 없는데 어떻게 하나요? 링크 추가

  - 도움 주신 분: 루시님

  ## v1.0 - 2020-07-20

  - 강의 오픈
  ```

  </details>

### 섹션 2. 프로젝트 환경설정 : 4개 (47분)

- 프로젝트 생성 16:29

- 라이브러리 살펴보기 12:52

- View 환경설정 14:09

- 빌드하고 실행하기 03:37

### 섹션 3. 스프링 웹 개발 기초 : 3개 (33분)

- 정적 컨텐츠 06:32

- MVC와 템플릿 엔진 10:33

- API 15:58

### 섹션 4. 회원 관리 예제 - 백엔드 개발 : 5개 (55분)

- 비즈니스 요구사항 정리 04:54

- 회원 도메인과 리포지토리 만들기 08:28

- 회원 리포지토리 테스트 케이스 작성 16:26

- 회원 서비스 개발 08:00

- 회원 서비스 테스트 17:32

### 섹션 5. 스프링 빈과 의존관계 : 2개 (27분)

- 컴포넌트 스캔과 자동 의존관계 설정 14:07

- 자바 코드로 직접 스프링 빈 등록하기 13:47

### 섹션 6. 회원 관리 예제 - 웹 MVC 개발 : 3개 (17분)

- 회원 웹 기능 - 홈 화면 추가 03:49

- 회원 웹 기능 - 등록 09:09

- 회원 웹 기능 - 조회 04:48

### 섹션 7. 스프링 DB 접근 기술 : 6개 (1시간 33분)

- H2 데이터베이스 설치 10:51

- 순수 JDBC 21:38

- 스프링 통합 테스트 12:50

- 스프링 JdbcTemplate 11:54

- JPA 20:50

- 스프링 데이터 JPA 15:35

### 섹션 8. AOP : 2개 (22분)

- AOP가 필요한 상황 08:18

- AOP 적용 14:03

### 섹션 9. 다음으로 : 1개 (18분)

- 다음으로 18:55
