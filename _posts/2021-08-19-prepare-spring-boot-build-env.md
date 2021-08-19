IntelliJ Idea에서 스프링 개발을 위한 환경 설정 중, 구글링했던 내용 정리

# JDK

## 버전 선택

필요한 버전으로 다운받으면 되며, IDE에서는 최신버전만 다운되는 것으로 보인다.  
따라서, 구버전이 필요한 경우 검색해서 설치 필요하다.

추가로 Gradle에서 지원되지 않는 JDK도 있으니 버전이 맞지 않다고 하면 재설치해주면 된다.

# Gradle

## `peer not authenticated`

- JDK에 인증서 등록하기  
  의존성 다운로드 URL의 인증서를 저장한 후, 설정된 JDK의 키스토어에 인증서 등록

  ```
  keytool -import -alias gradlerepo -file <path/of/certificate> -keystore cacerts -storepass changeit
  ```

