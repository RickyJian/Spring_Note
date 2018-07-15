# 設定配置

| 名稱 | 說明 |
|------|------|
| @Configuration | 宣告此類別為配置類別 |
| @ComponentScan | JSR-330 提供注入 |
| @EnableAutoConfiguration | 讓 Spring Boot 的 jar 檔自動配置 | 

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