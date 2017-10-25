# Bean In Spring

每一個被 Spring 管理的 Java 都稱之為 Bean，而 Spring 提供一個 IoC 容器用來初始化，並解決對象間的依賴與管理。

## Bean Scope

Spring Container 創建 Bean 的過程

| 名稱 | 描述 | 備註 |
| ----- | ----- | ----- |
| Singleton | Spring Container 只有一個 Bean 實例 | 默認配置 |
| Prototype | 每次此用則創建一個 Bean |  |
| Request | 每一 http request 則創建一個 Bean |  |
| Session | 每一 http session 則創建一個 Bean |  |
| GlobalSession | 只在 portal 應用中有用，每一 global http session 則創建一個 Bean |  |

```java

@Service
@Scope("prototype")
public class UseAService(){

}

```

## Bean 生命週期

加入一些動作在 Bean 使用前或是 Bean 使用後

### 基本 `@Bean`

```java

// Bean Life Class

public class BeanLife(){
    public BeanLife(){
        System.out.println("Bean Construct")
    }
    public void init(){
        System.out.println("Bean Init")
    }
    public void destroy(){
        System.out.println("Bean Destroy")
    }
}

// Java Config

@Configuration
@ComponentScan("com.xx.xxx.xxx")
public class BeanConfig(){
    
    @Bean(initMethod="init",destroyMethod="destroy")
    BeanLife beanLife(){
        return new BeanLife();
    }
}

```

### JSR-250

```java

// Bean Life Class

public class JSR250BeanLife(){
    public JSR250BeanLife(){
        System.out.println("JSR250Bean Construct")
    }
    @PostConstruct
    public void init(){
        System.out.println("JSR250Bean Init")
    }
    @PreDestroy
    public void destroy(){
        System.out.println("JSR250Bean Destroy")
    }
}

// Java Config

@Configuration
@ComponentScan("com.xx.xxx.xxx")
public class BeanConfig(){
    
    @Bean
    JSR250BeanLife jsr250BeanLife(){
        return new JSR250BeanLife();
    }
}

```

#### jar

| 名稱 | 描述 | 
| -----|-----|
| JSR-250 | Bean 初始或銷毀操作 |

## Bean 事件及監聽

Bean 與 Bean 之間的溝通

1. 自訂事件，繼承 ApplicationEvent
2. 自訂監聽，實作 ApplicationListener
3. Container Show

```java

// 自訂事件

public CustomEvent extends ApplicationEvent{
    private String msg;

    public String getMsg(){
        return msg;
    }

    public void setMsg(String msg){
        this.msg = msg;
    }
}

```

```java

// 自訂監聽

@Component
public class CustomListener implements ApplicationListener<CustomEvent>{

    public void onApplicationEvent(CustomEvent event){
        String msg = evvebt.getMsg();
        System.out.println("listener接收到event發布的消息，此消息為："+msg) 
    }
}

```

```java

// 事件發布

@Component
public class CustomPublisher {

    @Autowired
    ApplicationContext applicationContext;

    public void publish(String msg){
        applicationContext.publishEvent(new CustomEvent(this,msg));
    }
}

```

```java

// Java Config

@Configuration
@Component("com.xx.xx.xxxx.xxx")
public class EventConfig{

}

```

```java

// 執行
public class Main {

    public static void main (String args){
        AnnotationConfigApplicationContext context = new  AnnotationConfigApplicationContext(EventConfig.class);

        CustomPublisher cp = context.getBean(CustomPublisher.class);
        cp.publish("application event");
        context.close();
    }
}

```

## 各種 Bean 的應用

### 基本

| 名稱 | 說明 |
|------|------|
| @Component | 沒有明確定義 |
| @Service | 業務邏輯(Service)層使用 |
| @Repository | 資料訪問(DAO)層使用 |
| @Controller | 表現(MVC)層使用 |

```java

@Service
public class AService(){

}

```

### 注入

| 名稱 | 說明 |
|------|------|
| @Autowired | Spring 提供注入 |
| @Inject | JSR-330 提供注入 |
| @Resource | JSR-250 提供注入 |

```java

@Service
public class UseAService(){

@Autowired
aService aService


}


```

### 部署


| 名稱 | 說明 |
|------|------|
| @Configuration | 宣告此類別為配置類別 |
| @ComponentScan | JSR-330 提供注入 |

```java

// 未使用 @Service , @Autowired
// 使用 @Bean
// 只要 Container 存在某個 Bean ， 就可以在另一個 Bean 注入

@Configuration
public class JavaConfig{


// 方法一
    @Bean
    public AService aService(){
        return new AService();
    }

    @Bean  
    public UseAService useAService(){
         UseAService useAService = new UseAService();
         useAService.setAService(ASerivce);
         return useAService;
    }

// 方法二
// 參數傳遞法

    @Bean  
    public UseAService useAService(AService aSrvice){
        UseAService useAService = new UseAService();
        useAService.setAService(ASerivce);
        return useAService;

    }
}

```

### AOP

| 名稱 | 說明 |
|------|------|
| @Aspect | 宣告切面 |
| @After | 定義 advice 可直接將攔截規則設為參數 |
| @Before | 定義 advice 可直接將攔截規則設為參數 |
| @Around | 定義 advice 可直接將攔截規則設為參數 |
| @PointCut | 定義攔截規則 |
