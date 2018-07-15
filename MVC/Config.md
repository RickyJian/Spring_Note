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

自動開啟默認配置，當要自我撰寫設定檔時必須註解

### ViewResolvver

[連結](ViewResolver.md)

### 靜態檔案配置

[連結](Static.md)

### configurePathMatch

在 Spring MVC 中倘若路徑最後帶`.`，`.`後的值將會被忽略，若不想忽略後方值必須實作`configurePathMatch`


```java

@Configuration
@EnableWebMvc
public class MvcConfig implements WebMvcConfigurer {

    @Override
    public void configurePathMatch(PathMatchConfigurer configurer){
        configurer.setUseSuffixPatternMatch(false);
    }

}

```