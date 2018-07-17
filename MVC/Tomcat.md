# Tomcat

配置 Tomcat

## application.properties

```property

## servlet container

## port 配置，默認為 8080
server.port = 8080

## session 過期時間，已秒為單位
server.session-timeout = 1280

## 訪問配置，默認為 /
server.servlet.contextPath = /project

## Tomcat

## 編碼配置，默認為 UTF-8
server.tomcat.uri-encoding = UTF-8

## Tomcat 是否開啟壓縮，默認為 off
server.tomcat.compression = off


```

## JAVA Config

實作 EmbeddedServletContainerCustomizer 的 Bean

```java

@Component 
public class CustomServletContainer implements EmbeddedServletContainerCustomizer {

    @Override
    public void customize(ConfigurableEmbeddedServletContainerCustomizer container){
        // port 設定
        container.setPort(8080); 
        // 設定 error 頁面
        container.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND,"/Error404.html"));
        // 設定 session 過期時間
        container.setSessionTimeout(10,TimeUnit.MINUTES);

    }

}

```

## 其他容器配置


```java

@Bean
public EmbeddedServletContainerFactory servletContainer(){
    // Tomcat 
    TomcatEmbeddedServletContainerFactory factory = new TomcatEmbeddedServletContainerFactory();
    // Jetty 
    JettyEmbeddedServletContainerFactory factory = new JettyEmbeddedServletContainerFactory();
    // Undertow 
    UndertowEmbeddedServletContainerFactory factory = new UndertowEmbeddedServletContainerFactory();
    factory.setPort(8080);
    factory.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND,"/Error404.html"));
    factory.setSessionTimeout(10,TimeUnit.MINUTES);
    return factory;
}

```