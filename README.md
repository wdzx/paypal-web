# paypal-web
参考java paypal支付，提供token刷新解决方案，参考地址为https://blog.csdn.net/change_on/article/details/73881791
在上述地址可以会出现token超时错误，解决方案如下
1.
<dependency>
            <groupId>com.paypal.sdk</groupId>
            <artifactId>rest-api-sdk</artifactId>
            <version>1.4.2</version>
</dependency>
此处改成
<dependency>
            <groupId>com.paypal.sdk</groupId>
            <artifactId>rest-api-sdk</artifactId>
            <version>1.14.0</version>
</dependency>

2.

        payment.setRedirectUrls(redirectUrls);
        return payment.create(apiContext);
        此处改成
        payment.setRedirectUrls(redirectUrls);
        APIContext apiContext = new APIContext(paypalConfig.getClientId(), paypalConfig.getClientSecret(), paypalConfig.getMode());
        return payment.create(apiContext);

原因浅析，bean注解单例注入，在单次运行时只生成一次AccessToken,1.4.2版本没找到支持新实例化的方案，修改后自动重新获取。
