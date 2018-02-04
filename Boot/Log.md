# Log 配置

## Profile 配置

* 針對不同環境做不同的配置
* 透過 application.properties 設置

> application-{profileName}.properties

application.properties

```properties

<!-- 指定使用profile -->

spring.profiles.active=dev

```

application-dev.properties

```properties

server.port =8080

```
