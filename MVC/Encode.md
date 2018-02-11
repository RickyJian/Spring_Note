# 編碼配置

application.properties

```property

spring.http.encoding.charset=UTF-8
spring.http.encoding.force=true

```

```java


@ConfigurationProperties(prefix = "spring.http.encoding")
public class HttpEncodingProperties{

    public static final Charset DEFAULT_CHARSET =Charset.forName("UTF-8");

    private Charset charset = DEFAULT_CHARSET;

    private boolean force = true;


    public Charset getCharset() {
        return charset;
    }

    public void setCharset(Charset charset) {
        this.charset = charset;
    }

    public boolean isForce() {
        return force;
    }

    public void setForce(boolean force) {
        this.force = force;
    }
}


```