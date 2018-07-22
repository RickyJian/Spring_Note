# DataSource

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
        return dataSource;
    }

```

### C3P0

C3P0 是個開源 database connection pool

參照：[連結](http://josh-persistence.iteye.com/blog/2229929)

```java

    @Bean
    public DataSource dataSource(){
        ComboPooledDataSource dataSource = new ComboPooledDataSource(); 
        dataSource.setDriverClass(driver);  
        dataSource.setJdbcUrl(url);  
        dataSource.setUser(username);  
        dataSource.setPassword(password); 
        // connection pool 初始創建的 connection 數量
        dataSource.setInitialPoolSize(1);
        // connection 最大連線數量，默認為 15
        dataSource.setMaxPoolSize(15);
        // connection pool 保持最小的連接數量
        dataSource.setMinPoolSize(5);
        // 連線生存時間，超過時間未使用將會被 close ，若還在使用則等使用完畢後 close
        dataSource.setMaxConnectionAge(100));
        // 當 connection pool 空時，自動增加連線數量
    	dataSource.setAcquireIncrement(3);
        // 檢查 connection pool 的 connection 是否使用，已秒為單位
    	dataSource.setIdleConnectionTestPeriod(120);
        return dataSource;
    }

```

[配置](https://mvnrepository.com/artifact/org.hibernate/hibernate-c3p0/4.1.0.Final)