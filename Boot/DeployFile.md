# 常用配置文件

## properties 配置

| 名稱 | 說明 |
|------|------|
| @ImportResource | 匯入 xml 配置 |
| @PropertyResource | 匯入 properties 配置 |
| @Value | 將配置的值注入屬性中 |
| @ConfigurationProperties | 將值自動注入POJO中 |

application.properties

```properties

server.port=9090
server.context-path=/hello

```

### @PropertySource and @Value

book.properties

```properties

book.author=ricky
book.name=spring

```

注入 JAVA<br><br>
RouteController.java

```java

@RestController
public class RouteController {

    @Value("${book.author}")
    private String author;
    @Value("${book.name}")
    private String name;


    @RequestMapping("/")
    public String index (){
        return  "author:"+this.author+"  name:"+this.name;
    }
}


```

SpringBootApplication.java

```java

@SpringBootApplication
@PropertySource({"classpath:book.properties"})
public class FirstApplication {

	public static void main(String[] args) {
		SpringApplication.run(FirstApplication.class, args);
	}
}


```

### @ConfigurationProperties

book.properties

```properties

book.author=ricky
book.name=spring

```

BookBean.java 

```java

@Component
@PropertySource({"classpath:book.properties"})
@ConfigurationProperties(prefix = "book" )
public class BookBean {
    private String author;
    private String name;

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

RouteController.java

```java

@RestController
public class RouteController {

    @Autowired
    private BookBean bookBean;

    @RequestMapping("/")
    public String index (){
        return  "author:"+bookBean.getAuthor()+"  name:"+bookBean.getName();
    }
}

```

SpringBoot.java

```java

@SpringBootApplication
public class FirstApplication {

	public static void main(String[] args) {
		SpringApplication.run(FirstApplication.class, args);
	}
}

```


## yml 配置

application.yml

```yml

server:
  port: 9090
  contextPath: /hello

```

### xml 配置

| 名稱 | 說明 |
|------|------|
| @ImportResource | 匯入 xml 配置 |

使用 @ImportResource

```java

@ImportResource({"classpath:content.xml","classpath:context.xml"})

```
