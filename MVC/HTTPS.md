# HTTPS 配置


## 生成 SSL 憑證

```terminal

// java ssl 生成 command
keytool -genkey -alias tomcat

```

## 配置 SSL

* 使用 application.properties
* 將 SSL 憑證放置在與 application.properties 相同目錄



```property

## HTTPS port 為 8443
server.port = 8443

## 自己生成的 SSL 憑證 
server.ssl.key-store = .keystore

## 生成憑證的密碼
server.ssl.key-store-password = secret

## 憑證格式，JAVA 憑證格式為 JKS
server.ssl.keyStoreType = JKS

## 配置用的 server
server.ssl.key-alias=tomcat


```

## http 導向 https

```java

@Configuration
public class HttpConfig {

  @Bean
    public EmbeddedServletContainerFactory servletContainer() {
        TomcatEmbeddedServletContainerFactory tomcat = new TomcatEmbeddedServletContainerFactory() {
            @Override
            protected void postProcessContext(Context context) {
                SecurityConstraint securityConstraint = new SecurityConstraint();
                securityConstraint.setUserConstraint("CONFIDENTIAL");
                SecurityCollection collection = new SecurityCollection();
                collection.addPattern("/*");
                securityConstraint.addCollection(collection);
                context.addConstraint(securityConstraint);
            }
        };
    
        tomcat.addAdditionalTomcatConnectors(httpConnector());
        return tomcat;
    }

    @Bean
    public Connector httpConnector(){
        connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
        connector.setScheme("http");
        connector.setPort(8080);
        connector.setSecure(false);
        connector.setRedirectPort(8443);
        return connector;
    }

}



```

---------------------------------------

JAVA SSL：https://github.com/spring-projects/spring-boot/blob/v1.4.1.RELEASE/spring-boot/src/main/java/org/springframework/boot/context/embedded/Ssl.java
