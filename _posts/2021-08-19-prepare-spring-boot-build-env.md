# Gradle

## `peer not authenticated`

- JDK에 인증서 등록하기  
  의존성 다운로드 URL의 인증서를 저장한 후, 설정된 JDK의 키스토어에 인증서 등록

  ```
  keytool -import -alias gradlerepo -file <path/of/certificate> -keystore cacerts -storepass changeit
  ```

