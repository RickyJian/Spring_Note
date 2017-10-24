# Bean In Spring

每一個被 Spring 管理的 Java 都稱之為 Bean，而 Spring 提供一個 IoC 容器用來初始化，並解決對象間的依賴與管理。

## 基本

| 名稱 | 說明 |
|------|------|
| @Component | 沒又明確定義 |
| @Service | 業務邏輯(Service)層使用 |
| @Repository | 資料訪問(DAO)層使用 |
| @Controller | 表現(MVC)層使用 |

```java

@Service
public class AService(){

}

```

## 注入

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

## 部署


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