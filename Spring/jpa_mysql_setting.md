## 문제 상황

- SpringBoot에서 JPA로 데이터베이스에 접근
- 아무 설정 없이 실행할 경우 → H2 쿼리가 적용됨 ⇒ MySQL 쿼리가 적용되도록 하기 위함

## 해결 방법

- `application.properties`에 아래 코드 추가

```java
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
spring.datasource.hikari.jdbc-url=jdbc:h2:mem://localhost/~/testdb;MODE=MYSQL
```
