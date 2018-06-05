### 1.Spring生成Bean的三种方式
model如下
```
public interface UserDaoInterface {
    public void sayHello();
    public void sayinit();
    public void saydestory();
}
```
1.1 无参数的构造方式，通过id获取
applicationContext.xml中bean配置如下
 `<bean id="userdaointerface" class="com.dao.UserDaoImp" init-method="sayinit" destroy-method="saydestory">`
 获取bean方式如下
```
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        // 1.通过id获取bean
        UserDaoInterface userDaoInterface = (UserDaoInterface) applicationContext.getBean("userdaointerface");
        userDaoInterface.sayHello();
```
1.2 静态工厂实例化
applicationContext.xml中bean配置如下
`<bean id="bean2" class="com.utils.Bean2Factory" factory-method="getBean2"/>`
获取bean方式如下
```
UserDaoInterface userDaoInterface = Bean2Factory.getBean2();
        userDaoInterface.sayHello()
```

```
public class Bean2Factory {
    public static UserDaoInterface getBean2(){
        return new UserDaoImp();
    }

}
```
1.3 实例化工厂获取bean
applicationContext.xml配置bean如下
```
<bean id="bean3Factory" class="com.utils.Bean3Factory"></bean>
    <bean id="bean3" factory-bean="bean3Factory" factory-method="getBean3"></bean>
```
获取bean方式如下
```
 Bean3Factory bean3Factory = new Bean3Factory();
        UserDaoInterface userDaoInterface = bean3Factory.getBean3();
        userDaoInterface.sayHello();
```

```
public class Bean3Factory {

    public UserDaoInterface getBean3(){
        return new UserDaoImp();
    }
}
```



 

