# TransactionInercepter

以 AOP 方式設定 Transaction 

```java

@Configuration
@EnableTransactionManagement
public class PersistenceConfig {   
    @Bean
    public TransactionInterceptor transactionInterceptor() {
//    	交易攔截器，設定 service method 的交易行為
        Properties props = new Properties();
        props.setProperty("add*", "PROPAGATION_REQUIRED,-java.lang.RuntimeException");
        props.setProperty("update*", "PROPAGATION_REQUIRED,-java.lang.RuntimeException");
        props.setProperty("delete*", "PROPAGATION_REQUIRED,-java.lang.RuntimeException");
        props.setProperty("get*", "PROPAGATION_NOT_SUPPORTED,readOnly");
        props.setProperty("search*", "PROPAGATION_NOT_SUPPORTED,readOnly");
        props.setProperty("*", "PROPAGATION_NOT_SUPPORTED,readOnly");
        return new TransactionInterceptor(transactionManager(), props);
    }

    @Bean
    public DefaultPointcutAdvisor defaultPointcutAdvisor() {
        // AOP advisor：AOP 切入點，在 service method 增加交易
        AspectJExpressionPointcut expression = new AspectJExpressionPointcut();
        expression.setExpression("execution(* tw.org.ils.service.*.*(..))");
        return new DefaultPointcutAdvisor(expression, transactionInterceptor());
    }
}

```