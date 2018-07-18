# JpaRepository

## 實作

```java

public interface DemoDAO extends JpaRepository<Demo,Long>{

}

```

## 配置

@EnableJpaRepositories：開啟 Spring Data JPA 支持

```java

@Configuration
@EnableJpaRepositories
public class JpaConfig {

    @Bean 
    public EntityManagerFactory entityManagerFactory(){

    }
}

```