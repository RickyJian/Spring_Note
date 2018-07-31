# Interceptor 攔截器

對每一 request 前後進行邏輯處理，類似 servlet 的 filter。

必須繼承 `HandlerInterceptorAdapter` 類別，並覆寫其方法。

## 方法：PreHandler

request 進 controller 前做邏輯處理

```java

// 定義 Interceptor

public class DemoInterceptor extends HandlerInterceptorAdapter {

    @Override
    public boolean preHandler(HttpServletRequest request , HttpServletResponse response , Object handler) throws Exception {
        // 業務邏輯部分
        System.out.println("pre")
        return true;
    }

}

```

## 方法：postHandler

request 進 controller 後做邏輯處理

```java

// 定義 Interceptor

public class DemoInterceptor extends HandlerInterceptorAdapter {

    @Override
    public void postHandler(HttpServletRequest request , HttpServletResponse response , Object handler , ModelAndView modelAndView) throws Exception {
        // 業務邏輯部分
        System.out.println("post")
    }
}

```

## 方法：AddInterceptors

配置 攔截器

```java

@Configuration
@EnableWebMvc
public class WebConfig extends WebMvcConfigurer {

    @Bean 
    public DemoInterceptor demoInterceptor(){
        return new DemoInterceptor();
    }

    @Override
	public void addInterceptors(InterceptorRegistry registry) {
		registry.addInterceptor(demoInterceptor());
		WebMvcConfigurer.super.addInterceptors(registry);
	}

} 

```