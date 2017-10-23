# Bean In Spring

每一個被 Spring 管理的 Java 都稱之為 Bean，而 Spring 提供一個 IoC 容器用來初始化，並解決對象間的依賴與管理。

## 基本

| 名稱 | 說明 |
|------|------|
| @Component | 沒又明確定義 |
| @Service | 業務邏輯(Service)層使用 |
| @Repository | 資料訪問(DAO)層使用 |
| @Controller | 表現(MVC)層使用 |

```java

@Service
public class AService(){

}

```

## 注入

| 名稱 | 說明 |
|------|------|
| @Autowired | Spring 提供注入 |
| @Inject | JSR-330 提供注入 |
| @Resource | JSR-250 提供注入 |

```java

@Service
public class UseAService(){

@Autowired
aService aService


}


```