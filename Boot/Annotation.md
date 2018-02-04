# Spring Boot 常用註解

## 基本

| 名稱 | 說明 |
|------|------|
| @SpringBootApplication | 啟動 Spring Boot ， 可透過 exclude 參數關閉配置檔案 |

> SpringBootApplication：組合註解，組合了 @Configuration、@EnableAutoConfiguration、@ComponentScan 

## 配置

| 名稱 | 說明 |
|------|------|
| @ImportResource | 匯入 xml 配置 |
| @PropertyResource | 匯入 properties 配置 |
| @Value | 將配置的值注入屬性中 |