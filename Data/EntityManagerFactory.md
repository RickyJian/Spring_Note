# EntityManagerFactory

JPA中要對資料庫進行操作前，必須先取得EntityManager實例，這有點類似JDBC在對資料庫操作之前，必須先取得Connection實例，EntityManager是JPA操作的基礎，它不是設計為執行緒安全（Thread-safe）。

[原文網址](https://openhome.cc/Gossip/EJB3Gossip/EntityManager.html)

```java

@Configuration
@EnableJpaRepositories
public class JpaConfig {

    @Bean 
    public LocalContainerEntityManagerFactoryBean entityManagerFactory(){
		HibernateJpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
		vendorAdapter.setDatabase(Database.HSQL);
		vendorAdapter.setGenerateDdl(true);

		LocalContainerEntityManagerFactoryBean factory = new LocalContainerEntityManagerFactoryBean();
		factory.setJpaVendorAdapter(vendorAdapter);
		factory.setPackagesToScan(getClass().getPackage().getName());
		factory.setDataSource(dataSource());

        return factory;
    }
}

````

--------

Datasource：[連結](DataSource.md)