# Banner 

## application.properties

```property

## 關閉 Banner
spring.main.banner-mode=off

```

## Java Config

```java

@SpringBootApplication
public class firstApplication {

    public static void main (String args[]){
        SpringApplication app = new SpringApplication(firstApplication.class);
        app.setShowBanner(false);
        app.run(args);
    }
}

```