## 依赖引用
这是一个common异常处理的包,其他项目会依赖于这个包,所以在更改后,需要把snapshot的库更新以下,以便其他项目可以依赖到最新的包.

```
mvn deploy:deploy-file -DgroupId=com.mbp.eng -DartifactId=common.error -Dversion=1.0.0-SNAPSHOT -Dpackaging=jar -Dfile=./target/common.error-1.0.0-SNAPSHOT.jar -Durl=http://xxx.xxx.com/snapshots/ -DrepositoryId=snapshots
```

release:
```bash
mvn deploy:deploy-file -DgroupId=com.mbp.eng -DartifactId=common.error -Dversion=1.0.0 -Dpackaging=jar -Dfile=./target/common.error-1.0.0-SNAPSHOT.jar -Durl=http://xxx.xxx.com/releases/ -DrepositoryId=releases
```

## 错误处理
common中包含了统一的ErrorStatus集合.所有的error code都在这里定义.为了方便以后国际化,*error.properties*里面定义了每个error code对应的详细信息.其他国际化的信息可以添加,例如添加error_cn_Zh.properties.
MyException中的参数包括error code和该异常本身的错误信息（注意不是error code对应的信息）.
### How to use
对于spring的工程引用该错误处理机制,需要作如下操作：
- 在pom.xml中依赖common包
- 定义`ResourceBundleMessageSource`的Bean
```text
    @Bean
    public MessageSource messageSource() {
        ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
        messageSource.setBasename("locale/error");
        return messageSource;
    }
```
- 定义`@ControllerAdvice`,拦截各种Exception,通过MessageSource获取error code对应的错误信息返回给前端.

对于非spring的java工程,需要作如下操作：
- 在pom.xml中依赖common包
- 定义MessageSource包,指向error.properties
- 利用MessageSource获取error code对应的信息.