# TransactionManager

Spring 交易管理配置及實作

## PlatformTransactionManager

PlatformTransactionManager 介面有許多具體的交易實現類別，例如：DataSourceTransactionManager、 HibernateTransactionManager、JdoTransactionManager、JtaTransactionManager 等，藉由依賴於PlatformTransactionManager 介面及各種的技術實現

[原文網址](https://openhome.cc/Gossip/SpringGossip/SpringTransaction.html)

| 交易名稱 | 說明 |
| ---- | ---- | 
| DataSourceTransactionManager | JDBC、MyBatis 交易管理 |
| HibernateTransactionManager | Hibernate 交易管理 |
| JdoTransactionManager | JDO 交易管理 | 
| JtaTransactionManager | Java 分散式事件 交易管理 | 
| JpaTransactionManager | JPA 交易管理 |

```java

@Configuration
@EnableTransactionManagement
public class PersistenceConfig {

    @Bean
    public PlatformTransactionManager transactionManager(){
        // Hibernate 交易管理
        HibernateTransactionManager htm = new HibernateTransactionManager();
        htm.setDataSource(dataSource());
        htm.setSessionFactory(sessionFactory());
        return htm;
    }

}

```

## @EnableTransactionManager

* 開啟 `@Transactional` 註解
* 可以註解在 interface、class、方法上

| 屬性 | 說明 |
| ----- | ----- | 
| value | 當有多個 TransactionManager 時，指定由哪個 TransactionManager 做交易管理。 |
| propagation | Transaction 傳播行為，指何時該開始一個新的交易，或何時交易該被暫停，或者方法是否要在交易中進行。默認為 REQUIRED。 |
| isolation | 多 transaction 中各 transaction 隔離的程度，默認為 DEFAULT。 |
| timeout | transaction 時間，若超時會 rollback。默認為 -1。 |
| readOnly | 指定 transaction 是否只做讀取 |
| rollbackFor | 指定哪些異常發生須要 rollback，已 class 為對象 |
| rollbackForClassName | 指定哪些異常發生須要 rollback，已 className(型態 string) 為對象 |
| noRollbackFor | 指定哪些異常發生不須要 rollback，已 class 為對象 |
| rollbackForClassName | 指定哪些異常發生不須要 rollback，已 className(型態 string) 為對象  |

[API](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#getPropagationBehavior--)

[參考文章](https://openhome.cc/Gossip/SpringGossip/TransactionAttribute.html)

```java

public interface DemoService {

    @Transactional(propagation = Propagation.REQUIRES)
    public save(Pojo pojo);

}

```

### propagation

| 屬性 | 說明 |
| ----- | ----- |
| PROPAGATION_REQUIRED | 若無 transaction 存在，則創建 |
| PROPAGATION_REQUIRES_NEW | 創建新的 transaction ，暫停現有 transaction |
| PROPAGATION_SUPPORTS | 若 transaction 存在，則以 transaction 方式進行，若無，則以無 transaction 方式進行 |
| PROPAGATION_NOT_SUPPORTED | 已非 transaction 方式進行，若有則關閉 transaction ，並執行 |
| PROPAGATION_NEVER | 已非 transaction 方式進行，若有則拋出異常 | 
| PROPAGATION_MANDATORY | 若無 transaction 存在，則拋出異常 |
| PROPAGATION_NESTED | 在一個巢狀交易中進行，若無則像 REQUIRED | 

### isolation

| 屬性 | 說明 |
| ----- | ----- |
| ISOLATION_DEFAULT | 使用資料庫預設層級 |
| ISOLATION_READ_COMMITTED | 允許其他 transaction 讀取已 commit 的資料欄位，防止 dirty read 產生，但 non-repeatable reads 和 phantom reads 有可能發生 |
| ISOLATION_READ_UNCOMMITTED | 允許其他 transaction 讀取未 commit 的資料欄位，dirty read 、 non-repeatable reads 、 phantom reads 有可能發生 |
| ISOLATION_REPEATABLE_READ | 執行相同查詢時回應相同資料，防止 dirty read 和 non-repeatable reads 產生，但 phantom reads 有可能發生  |
| ISOLATION_SERIALIZABLE | 防止 dirty read 、 non-repeatable reads 、 phantom reads 產生，由於會將資料表鎖住，因此有效能問題 |

------

AOP交易設定：[連結]("TransactionIntercepter.md")