# DataSource

Java’s javax.sql.DataSource interface provides a standard method of working with database connections.
java 提供 ` javax.sql.DataSource ` 介面提供基本資料庫連線。

## DriverManagerDataSource

database connection 沒有 connection pool 功能

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

database connection 有 connection pool 功能

### DBCP

apache java database connection pool

> Gradel 配置：<br>
> compile('commons-dbcp:commons-dbcp:1.4')

參照：[連結](https://blog.csdn.net/z_x_1000/article/details/14055571)

```java

    @Bean
    public DataSource dataSource(){
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName( driver );
        dataSource.setUsername( username );
        dataSource.setPassword( password );
        dataSource.setUrl( url );
        // connection pool最大連線數，若為 0 時則無限制
        dataSource.setMaxActive( 50 );
        // 最大等待連線數量，若為 0 時則無限制
        dataSource.setMaxIdle( 10 );
        // 最大等待秒數
        dataSource.setMaxWait( 10000 );
        return ds;
    }

```


### C3P0