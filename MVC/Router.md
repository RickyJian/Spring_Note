# Router

路由器設定

## Controller

| 名稱 | 說明 |
|------|------|
| @Controller | DispatchServlet 會自動掃描此註解的類別，並將 Web 請求映射到此方法上 |
| @RequestMapping | 映射 Web 請求(路徑或參數)，支持 http request and http response 當作參數 |
| @ResponseBody | 將回應值放置 response 內，而不是換頁面，常跟 `ajax` 做配合 |
| @RequestBody | 將參數放置在 request 中，而不是待在網址後面，此註解放在參數前，常用來處理 Content-Type 不是 application/x-www-form-urlencoded 的格式 |
| @PathVariable | 接收入徑參數，此註解放在參數前 |
| @RestController | 複合註解，組合了 `@Controller` 和 `@ResponseBody` |

```java

// Controller , RequestMapping , ResponseBody  應用

@Controller
@RequestMapping("/Demo")
public class DemoController {

    @RequestMapping(produces = "text/plain;charset=UTF-8") // produces 制定 response 的類型及編碼，若是 json 格式則為 text/json;charset=UTF-8"
    public @ResponseBody String index (HttpServletRequest request){
        return "url:" +request.getRequestURL() + "can access";
    }

    @RequestMapping(value = "/pathvar/{str}" , produces = "text/plain;charset=UTF-8")
    public @ResponseBody String demoPathVar (@PathVariable String str ,HttpServletRequest request){
        return "url:" +request.getRequestURL() + "can access,str:"+str;
    }

    @RequestMapping(value = "/requestParam" , produces = "text/plain;charset=UTF-8")
    public @ResponseBody String demoPathVar (Long id ,HttpServletRequest request){
        return "url:" +request.getRequestURL() + "can access,id:"+id;
    }

    @RequestMapping(value = "/requestParam" , produces = "text/plain;charset=UTF-8")
    @ResponseBody
    public  String demoPathVar (Long id ,HttpServletRequest request){
        return "url:" +request.getRequestURL() + "can access,id:"+id;
    }

    @RequestMapping(value = "/name1" , "name2" , produces = "text/plain;charset=UTF-8") //映射不同路進到相同方法
    public @ResponseBody String remove (HttpServletRequest request){
        return "url:" +request.getRequestURL() + "can access";
    }


}


```

```java

// RestController 應用

@RestController
@RequestMapping("/demoREST")
public class DemoRESTController{
    @RequestMapping(value = "/getjson" , produces = "text/json;charset=UTF-8")
    public String demoPathVar (XXXObj obj){
        return new XXXObj();
    }
}

```

## @ControllerAdvice 

對 @Controller 的類別以下所有的 @RequestMapping 方法都有效

| 名稱 | 說明 |
|------|------|
| @ExceptionHandler | 全域處理 Controller 的異常。它組合了`@Conponent`註解，因此自動註冊成 Spring 的 Bean |
| @InitBinder | 用來設置 WebDataBinder |
| @ModelAttribute | 綁定鍵值對應到 Model 裡 |

```java

// 制定 Advice

@ControllerAdvice
public class ExceptionHandlerAdvice {

    @ExceptionHandler(value = Exception.class) // 全域錯誤處理，透過 value 可以過濾錯誤條件
    public ModelAndView exception (Exception exception ,WebRequest request){
        ModelAndView modelAndView = new ModelAndView("error");
        modelAndView.addObject("errorMessage",exception.getMessage());
        return modelAndView;
    }

    @ModelAttribute // 將鍵值添加到全域 @RequestMapping 的方法中
    public void addAttributes(Model model){
        model.addAttribute("msg","其他訊息");
    }

    @InitBinder 
    public void initBinder(WebDataBinder webDataBinder){
        web.setDisallowedFields("id");
    }
}

```

```java

// Controller

@Controller 
public class AdviceController{
    @RequestMapping("/advice")
    public String getSomething (@ModelAttribue("msg") String msg , DemoObj demoObj){
        throw new Exception ("錯誤："+msg);
    }
}


```

## ViewController 

簡單配置頁面跳轉 Route

```java

// 配置

@Configuration
@EnableWebMvc
public class WebConfig extends WebMvcConfigurerAdapter {

   @Override 
   public void addViewControllers(ViewControllerRegistry registry){
       registry.addViewController("/index").setViewName("/index");
   } 

} 

```