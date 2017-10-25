# Spring EL

在開發過程中為了使用各種資源，我們可應用 Spring EL 來做資源注入。

## jar

| 名稱 | 描述 | 
| -----|-----|
| commons-io | Spring EL |

## 實例

使用 @Value

### 普通字串

```java

public class ELConfig {

    @Value("Hello Everyone")
    private String hello;

}

```

### 系統屬性

```java

public class ELConfig {

    @Value("#{systemProperties['os.name']}")
    private String osName;

}

```

### 表達式運算結果

```java

public class ELConfig {

    @Value("#{ T(java.lang.Math).random() * 100.0 }")
    private double randomNumber;

}

```

### `Bean`屬性

```java

public class ELConfig {

    @Value("#{aService.something}")
    private String something;

}

```

### 文件內容

```java

public class ELConfig {

    @Value("classpath:com/xx/xxxx/xxx/test.txt")
    private Resource testFile;

}

```

### 網址內容

```java

public class ELConfig {

    @Value("http://google.com")
    private Resource testURL;

}

```

### 屬性文件

```java

@PropertySource("classpath:com/xx/xxx/xxxx/xx.properties")
public class ELConfig {

    @Value("${author.name}")
    private Resource authorName;

    @Autowired
    private Enviroment enviroment;

    @Bean
    public static PropertySourcesPlaceholderConfigure propertyConfigure(){
        return new PropertySourcesPlaceholderConfigure();
    }


}

```
