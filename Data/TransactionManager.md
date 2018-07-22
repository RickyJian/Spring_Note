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

    @Bean
    public PlatformTransactionManager transactionManager(){
        // Hibernate 交易管理
        HibernateTransactionManager htm = new HibernateTransactionManager();
        htm.setDataSource(dataSource());
        htm.setSessionFactory(sessionFactory());
        return htm;
    }

```
