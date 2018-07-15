# 靜態檔案配置

* spring boot：放置在classpath：/resources、resources/static或resources/public裡
* jsp：放置在 classpath：/WebContent/WEB-INF/

## addResourceHandler

實作 WebMvcConfigurer 並覆寫 addResouceHandlers 可添加靜態檔案資源

```java

@Configuration
@EnableWebMvc
public class MvcConfig implements WebMvcConfigurer {

    @Override
    public void addResouceHandlers(ResourceHandlerRegistry registry){
        // addResourceHandler：對外訪問路徑
        // addResourceLocation：檔案或目錄位置
        registry.addResourceHandler("/assets/**").addResourceLocation("classpath:/assets/");
    }

}

```

### @Configuration

[連結](/Fundamental/Config.md)

### @EnableWebMvc

[連結](Config.md)



