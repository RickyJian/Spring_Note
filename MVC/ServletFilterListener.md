# 註冊 Servlet、Listener、Filter

## 直接註冊

```java

// 註冊 Servlet
@Bean
public MyServlet myServlet(){
    return new MyServlet();
} 

// 註冊 Listener
@Bean
public MyListerner myListerner(){
    return new myListerner();
} 

// 註冊 Filter
@Bean
public MyFilter myFilter(){
    return new MyFilter();
} 

```

## 透過 RegistrationBean

```java

// 註冊 Servlet
@Bean
public ServletRegistrationBean servletRegistrationBean(){
    return new ServletRegistrationBean(new MyServlet(),"/");
} 

// 註冊 Listener
@Bean
public ServletListenerRegistrationBean<MyListener> myListernerServletRegistrationBean(){
    return new ServletListenerRegistrationBean<MyListener>(new MyListener());
} 

// 註冊 Filter
@Bean
public FilterRegistrationBean filterRegistrationBean(){
    FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean();
    filterRegistrationBean.setFilter(new MyFilter());
    filterRegistrationBean.setOrder(2);
    return filterRegistrationBean;
} 

```