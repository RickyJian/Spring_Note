## ViewController 

簡單配置頁面跳轉 Route


```java

// 配置

@Configuration
@EnableWebMvc
@ComponentScan("com.xx.xx.xxxx.xx")
public class WebConfig extends WebMvcConfigurerAdapter {

   @Override 
   public void addViewControllers(ViewControllerRegistry registry){
       registry.addViewController("/index").setViewName("/index");
   }

} 

```