# HttpMessageConverter

* 用來處理 request 和 respnse 裡的資料

| 類型 | 說明 |
| ----- | ----- |
| StringHttpMessageConverter | |
| FormHttpMessageConverter | |
| MarshallingHttpMessageConverter | |
| MappingJacksonHttpMessageConverter | |
| AtomFeedHttpMessageConverter | |
| RssChannelHttpMessageConverter | |

## 自訂

一般 JavaBean 

```java

public class Student {
	
	private String no;
	private String name;
	
	public Student() {
	}
	
	public Student(String no, String name) {
		this.no = no;
		this.name = name;
	}
	
	public String getNo() {
		return no;
	}
	public void setNo(String no) {
		this.no = no;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	

}

```

AbstractHttpMessageConverter 覆寫

```java

//若要自定 HttpMessageConverter 必須繼承 AbstractHttpMessageConverter
public class MessageConverterConfig extends AbstractHttpMessageConverter<Student> {
	
	
	public MessageConverterConfig() {
//	自訂 ContentType 型別
		super(new MediaType("application","x-student",Charset.forName("UTF-8")));
	}

//	表明此 HttpMessageConverter 只處理 Student 類別
	@Override
	protected boolean supports(Class<?> clazz) {

		return Student.class.isAssignableFrom(clazz);
	}

//	處理 request 資料
	@Override
	protected Student readInternal(Class<? extends Student> clazz, HttpInputMessage inputMessage)
			throws IOException, HttpMessageNotReadableException {
		String temp = StreamUtils.copyToString(inputMessage.getBody(), Charset.forName("UTF-8"));
		String[] tempArr = temp.split("-");
		
		return new Student(tempArr[0],tempArr[1]);
	}

//	處理 response 資料
	@Override
	protected void writeInternal(Student t, HttpOutputMessage outputMessage)
			throws IOException, HttpMessageNotWritableException {
		String out ="No：" + t.getNo() + " Name：" +t.getName();
		outputMessage.getBody().write(out.getBytes());
		
	}
	
} 

```

配置

* configureMessageConverters：會覆蓋掉 MVC 默認配置的 HttpMessageConverter
* extendMessageConverters：不會覆蓋掉 MVC 默認配置的 HttpMessageConverter，並添加新的 HttpMessageConverter

```java

@Configuration
@EnableWebMvc
public class MvcConfig implements WebMvcConfigurer {

	@Override
	public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
		converters.add(conveter());
		WebMvcConfigurer.super.extendMessageConverters(converters);
	}

	@Bean
	public MessageConverterConfig conveter() {
		return new MessageConverterConfig();
	}
	
}

```