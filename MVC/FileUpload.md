# FileUpload

Spring 中要上傳文件必須配置一個 `MultipartResolver`

| commons-fileupload | Spring 檔案上傳 |
| commons-io | 簡化 IO 操作 |

```html

<!-- html name = upload.html -->

<div calss = "upload">
  <form action ="upload" enctype = "multipart/form-data" method = "post">  
    <input type="file" name = "file">
    <input type="submit" value = "上傳">
  </form>
<div>

```


```java

// ViewController ， multipartresolver 配置

@Configuration
@EnableWebMvc
@ComponentScan("com.xx.xx.xxxx.xx")
public class WebConfig extends WebMvcConfigurerAdapter {

   @Override 
   public void addViewControllers(ViewControllerRegistry registry){
       registry.addViewController("/toUpload").setViewName("/upload");
   }

   @Bean 
   public MultipartResolver multipartResolver(){
       CommonsMultipartResolver multipartResolver = new CommonsMultipartResolver();
       multipartResolver.setMaxUploadSize(100000);
       return multipartResolver;
   }

} 

```

```java

// 上傳程式
// 單檔上傳 MultipartFile file ， 多檔上傳 MultipartFile[] files
@RequestMapping(value = "/upload" , method = RequestMethod.POST)
public @ResponseBody String upload (MultipartFile file){
    try{
        FileUtils.writeByteArrayToFile(new File("path")),file.getBytes());
        return "OK" ;
    }catch(IOException ioEx){
        return "WRONG";

    }
}

```