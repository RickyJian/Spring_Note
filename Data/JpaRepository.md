# JpaRepository

> JpaRepository<T,ID extends Serializable> <br>
> T：entity<br>
> ID：PK Type

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

EntityManagerFactory：[連結](EntityManagerFactory.md)

## @NamedQuery

@NamedQuery 撰寫

```java

// entity

@Entity
@NamedQuery(name = "Demo.findByXX" , query = "select d from Demo d where d.XX = ?1 ")
public class Demo{

}

```

@NamedQuery 綁定

```java

// Repository

public interface DemoDAO extends JpaRepository<Demo,Long>{

    /**
     * 
     * 綁定NamedQuery
     * 
     */
    public List<Demo> findByXX(String xx)

}

```

## @Query

```java

public interface DemoDAO extends JpaRepository<Demo,Long>{

    /**
     * 
     * @Query使用參數索引
     * 
     */
    @Query("Select d from Demo d where d.XX = ?1")
    public List<Demo> findByXX(String xx)

    /**
     * 
     * @Query使用命名參數
     * 
     */
    @Query("Select d from Demo d where d.XX = :xx")
    public List<Demo> findByXX(@Param("xx") String xx)

}

```

