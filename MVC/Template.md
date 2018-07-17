# 模板配置

```java

@Configuration
@EnableWebMvc
public class MvcConfig implements WebMvcConfigurer {
	
	/**
	 * 
	 * 模板設定
	 * setPrefix：設定前綴字
	 * setSuffix：外部訪問路徑
     * setCharacterEncoding：設定模板編碼
	 * 
	 */
	@Bean
	public SpringResourceTemplateResolver templateResolver() {
		SpringResourceTemplateResolver templateResolver = new SpringResourceTemplateResolver();
		templateResolver.setPrefix("classpath:/templates/");
		templateResolver.setSuffix(".html");
		templateResolver.setCharacterEncoding("UTF-8");
		templateResolver.setCacheable(true);
		templateResolver.setTemplateMode(TemplateMode.HTML);
		return templateResolver;
	}
	
	
	/**
	 * 
	 * 模板引擎配置
	 * 
	 */
	@Bean
	public SpringTemplateEngine templateEngine() {
		SpringTemplateEngine templateEngine = new SpringTemplateEngine();
		templateEngine.setTemplateResolver(templateResolver());
		return templateEngine;
	}
	
	/**
	 * 
	 * Thymeleaf 模板設定
	 * setCharacterEncoding
     * 
	 */
	@Bean 
	public ThymeleafViewResolver thymeleafViewResolver() {
		ThymeleafViewResolver thymeleafViewResolver = new ThymeleafViewResolver();
		thymeleafViewResolver.setCharacterEncoding("UTF-8");
		thymeleafViewResolver.setTemplateEngine(templateEngine());
		return thymeleafViewResolver;
		
	}
	
}



```