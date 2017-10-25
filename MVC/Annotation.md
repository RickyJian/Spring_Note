# Spring MVC 常用註解

## 基本

| 名稱 | 說明 |
|------|------|
| @Controller | DispatchServlet 會自動掃描此註解的類別，並將 Web 請求映射到此方法上 |
| @RequestMapping | 映射 Web 請求(路徑或參數)，支持 http request and http response 當作參數 |
| @ResponseBody | 將回應值放置 response 內，而不是換頁面，常跟 `ajax` 做配合 |
| @RequestBody | 將參數放置在 request 中，而不是待在網址後面，此註解放在參數前 |
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
    public @ResponseBody String demoPathVar (XXXObj obj){
        return new XXXObj();
    }
}

```

## 部署

| 名稱 | 說明 |
|------|------|
| @EnableWebMVC | 自動開啟默認配置 |
