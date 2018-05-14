# Spring Core

| 名稱 | 說明 |
|------|------|
| @SpringBootApplication | 啟動 Spring Boot ， 可透過 exclude 參數關閉配置檔案 |

放置於一般 JAVA main方法 class中

```java

@SpringBootApplication
public class firstApplication {

    public static void main (String args[]){
        SpringApplication.run(firstApplication.class);
    }
}

```

## 關閉配置

增加 exclude 參數

```java

@SpringBootApplication(exclude = {Data.calss})
public class firstApplication {

    public static void main (String args[]){
        SpringApplication.run(firstApplication.class);
    }
}

```