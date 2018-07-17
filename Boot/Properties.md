
# properties 配置

| 名稱 | 說明 |
|------|------|
| @PropertyResource | 匯入 properties 配置 |
| @Value | 將配置的值注入屬性中 |
| @ConfigurationProperties | 將值自動注入POJO中 |

application.properties

```properties

server.port=9090
server.servlet.contextPath = /project

```

> application.properties：spring boot 預設配置


## @PropertyResource and @Value

將配置的值注入屬性中

book.properties

```properties

book.author=ricky
book.name=spring

```

注入 JAVA


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

## @ConfigurationProperties

將值自動注入POJO中

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

---

## application.propoerties

### Tomcat 配置

[連結](/MVC/Tomcat.md)