# Interceptor 攔截器

對每一 request 前後進行邏輯處理，類似 servlet 的 filter。
<br>
必須繼承 `HandlerInterceptorAdapter` 類別，並覆寫其方法。
1. preHandler
2. postHandler


```java

// 定義 Interceptor

public class DemoInterceptor extends HandlerInterceptorAdapter {

    @Override
    public boolean preHandler(HttpServletRequest request , HttpServletResponse response , Object handler) throws Exception {
        // 業務邏輯部分
        System.out.println("pre")
        return true;
    }

    @Override
    public void postHandler(HttpServletRequest request , HttpServletResponse response , Object handler , ModelAndView modelAndView) throws Exception {
        // 業務邏輯部分
        System.out.println("post")
    }
}

```

```java

// 配置

@Configuration
@EnableWebMvc
@ComponentScan("com.xx.xx.xxxx.xx")
public class WebConfig extends WebMvcConfigurerAdapter {

    @Bean 
    public DemoInterceptor demoInterceptor(){
        return new DemoInterceptor();
    }

    @Override
    public void addInterceptors(InterceptorReistry registry){
        registry.addInterceptor(demoInterceptor())
    }

} 

```