# 設定配置

## 介面：WebApplicationInitlizer

替代 web.xml 

```java

public class WebInitializer implements WebApplicationInitlizer{

    @Override 
    public void onStartup(ServletContext servletContext) throws Exception {
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.setRegister(MvcConfig.class);
        ctx.setServletContext(servletContext);

        Dynamic servlet = servletContext.addServlet("dispatcher", new DispatcherServlet(ctx));
        servlet.addMapping("/");
        servlet.setLoadOnStartup(1);

    }
}

```

## 註解：@EnabledWebMvc

自動開啟默認配置

```java


@Configuration
@EnableWebMvc
public class MvcConfig {

    @Bean
    public InternalResourceViewSolver viewResolver(){
        InternalResourceViewSolver viewResolver = new InternalResourceViewSolver();
        // 設定 view 頁面放置位置
        viewResolver.setPrefix("/WEB-INF/views");
        // 設定後綴字
        viewResolver.setSuffix(".jsp");
        return viewResolver;
    }

}

```