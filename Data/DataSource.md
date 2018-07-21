# DataSource

Java’s javax.sql.DataSource interface provides a standard method of working with database connections.
java 提供 ` javax.sql.DataSource ` 介面提供基本資料庫連線。

## DriverManagerDataSource

當有心的 connection 則新建一個 connection 沒有 connection pool 功能

```java

    @Bean
    public DataSource dataSource(){
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername( username );
        dataSource.setPassword( password );
        return dataSource;
    }


```

## BasicDataSource