# SessionFactory

SessionFactory接口負責初始化Hibernate。它充當數據存儲源的代理，並負責創建Session對象。這裡用到了工廠模式。需要注意的是SessionFactory並不是輕量級的，因為一般情況下，一個項目通常只需要一個SessionFactory就夠，當需要操作多個資料庫時，可以為每個資料庫指定一個SessionFactory。

[原文網址](https://read01.com/OnanQ.html)

## LocalSessionFactoryBean

Spring 與 Hibernate 常用配置，建立時會自動載入 mappingResource 中的 class (類別)和 hibernate 映射配置 (XXX.hbm.xml)

**在 hibernate3 時只能用 xml 配置，但在 hibernate4 後支持 annotation 配置**

```java

   @Bean
    public SessionFactory sessionFactory() {
        LocalSessionFactoryBean lsfb = new LocalSessionFactoryBean();
        // DataSource 注入
        lsfb.setDataSource(dataSource());
        // 掃描入徑內所有 class 及 xml 檔案並做載入
        lsfb.setPackagesToScan(root);
        // Hibernate 設定配置
        Properties properties = new Properties();
        properties.put("hibernate.hbm2ddl.auto", ddlStatus);
        properties.put("hibernate.dialect",dialect);
        properties.put("hibernate.show_sql",isShowSQL);
        properties.put("hibernate.format_sql",isFormatSQL);
        // SessionFactory Hibernate 配置設定
        lsfb.setHibernateProperties(properties);
        lsfb.afterPropertiesSet();
        return lsfb.getObject();
    }

```

## AnnotationSessionFactoryBean

Spring 與 Hibernate 配置，建立時會自動載入 annotatedClasses 中的 class (類別)

**在 Spring 4.3以上, 或 Hibernate 4.x/5.x 以上不建議使用**

```java


   @Bean
    public SessionFactory sessionFactory() {
        AnnotationSessionFactoryBean sessionFactory = new AnnotationSessionFactoryBean();
        // DataSource 注入
        sessionFactory.setDataSource(dataSource);
        // 掃描入徑內所有 class 及 xml 檔案並做載入
        sessionFactory.setPackagesToScan(root);
        // entity class 檔案設定
        sessionFactory.setAnnotatedPackages(basePackage);
        // Hibernate 設定配置
        Properties properties = new Properties();
        properties.put("hibernate.hbm2ddl.auto", ddlStatus);
        properties.put("hibernate.dialect",dialect);
        properties.put("hibernate.show_sql",isShowSQL);
        properties.put("hibernate.format_sql",isFormatSQL);
        // SessionFactory Hibernate 配置設定
        sessionFactory.setHibernateProperties(p);
        sessionFactory.afterPropertiesSet();
        return sessionFactory;
    }


```
-----

DataSource：[連結](DataSource.md)