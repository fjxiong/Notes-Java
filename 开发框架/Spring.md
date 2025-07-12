# Spring

## 1. 简介

Spring是一个支持快速开发Java EE应用程序的框架。它提供了一系列底层容器和基础设施，并可以和大量常用的开源框架无缝集成，可以说是开发Java EE应用程序的必备。

Spring最早是由Rod Johnson在他的《[Expert One-on-One J2EE Development without EJB]》一书中提出的用来取代EJB的轻量级框架。随后这哥们又开始专心开发这个基础框架，并起名为Spring Framework。

随着Spring越来越受欢迎，在Spring Framework基础上，又诞生了Spring Boot、Spring Cloud、Spring Data、Spring Security等一系列基于Spring Framework的项目。

## 2. IoC容器

什么是容器？容器是一种为某种特定组件的运行提供必要支持的一个软件环境。

例如，Tomcat就是一个Servlet容器，它可以为Servlet的运行提供运行环境。类似Docker这样的软件也是一个容器，它提供了必要的Linux环境以便运行一个特定的Linux进程。

Spring的核心就是提供了一个IoC容器，它可以管理所有轻量级的JavaBean组件，提供的底层服务包括组件的生命周期管理、配置和组装服务、AOP支持，以及建立在AOP基础上的声明式事务服务等。

Spring提供的容器又称为IoC容器，什么是IoC？IoC全称Inversion of Control，直译为控制反转。如何理解控制反转？我们可以通过下面的代码来一探究竟：

```java
public class UserServiceImpl implements UserService {
    private UserMapper userMapper = new UserMapperImpl1();

    public void addUser() {
        userMapper.addUser();
    }
}
```

```java
public class UserMapperImpl1 implements UserMapper {
    @Override
    public void addUser() {
        System.out.println("实现方案一");
    }
}
```

```java
public class UserMapperImpl2 implements UserMapper {
    @Override
    public void addUser() {
        System.out.println("实现方案二");
    }
}
```

可以看到，在第一个代码块中，我们在业务类中手动new了一个UserMapper接口的实现类。但是，UserMapper接口的实现类可能不止一个，如第二和第三个代码块所示，UserMapper接口有两个实现类，甚至更多。

如果我们想更换一个实现，就必须修改service中new的那个对象。如果在众多的类中都用到了UserMapper，这样的修改是极为不便的，况且我们也没必要在每一个用到UserMapper的地方都创建一个新的对象，完全可以共享一个对象。

所以，当一个系统有大量的组件，其生命周期和相互之间的依赖关系如果由组件自身来维护，不但大大增加了系统的复杂度，而且会导致组件之间极为紧密的耦合，继而给测试和维护带来了极大的困难。

现在我们希望程序中的对象，不要由程序本身进行创建，而是由第三方根据实际需要为我们创建。也就是说将对象的创建控制权由程序本身转移到第三方。这就是Spring的第一大核心内容——控制反转IoC！

帮我们创建和管理实例对象的这个第三方就是Spring提供的IoC容器，也称Spring容器。

一个由Spring容器创建和管理的对象我们称之为Bean。

## 3. Bean的注册与配置

IoC容器要负责实例化所有的Bean组件，因此，有必要告诉IoC容器如何创建组件，以及各组件的依赖关系。这个过程我们称之为Bean的注册与配置。

Bean的注册与配置有以下几种方式：

### 3.1 基于XML的配置

首先，我们用Maven创建工程并引入`spring-context`依赖：

* org.springframework:spring-context:6.0.0

然后，我们需要在resource目录下编写一个`application.xml`配置文件，告诉Spring容器应该如何创建并组装Bean：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userService" class="com.test.service.UserService">
        <property name="userMapper" ref="userMapper1" />
    </bean>

    <bean id="userMapper1" class="com.test.mapper.UserMapper" />
</beans>
```

上面的配置文件完成了两件事：

* 指示Ioc容器创建了两个Bean；
* 将id为`userMapper1`的Bean注入到id为`userService`的`userMapper`属性上。

其中第二点我们称之为依赖注入（DI）。所谓依赖注入，就是Spring容器需要根据组件之间的依赖关系来完成组件的完整装配。

想让Spring实现依赖注入，总得给它一个注入依赖的途径吧，如果我们的Bean封装的死死的，并没有提供对外的setter方法或相应的带参构造器，Spring就算有天大的本事，也不可能凭空把依赖注入进来。

所以，依赖注入其实是依靠于Bean的setter方法或带参构造器来完成的。即基于xml的依赖注入有两种途径：

* setter注入
* 构造器注入

我们先来看一下setter注入：

在XML配置方式下，可以通过`property`标签来指定要注入的依赖，这里的依赖可以是一个Bean，也可以是一个普通的变量，区别就是注入Bean用`ref`属性，注入普通变量用`value`属性：

```xml
<bean id="userService" class="com.test.service.UserService">
    <property name="userDao" ref="userDao1"/>
    <property name="number" value="666"/>
</bean>

<bean id="userDao1" class="com.test.dao.UserDao"/>
```

当然，在这之前，要在UserService中设置一个setUserDao和setNumber方法，事实上，Spring容器在注入依赖时就是根据property标签中的name属性的值去找对应的setter方法的。Spring容器通过该setter方法，将指定的依赖注入到该Bean中：

```java
public class UserService {
    private UserDao userDao;
    private int number;
    
    //Spring容器实现依赖注入的入口
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    //Spring容器实现依赖注入的入口
    public void setNumber(int number) {
        this.number = number;
    }
}
```

接下来我们再来看一看构造器注入：

我们可以在配置Bean的时候，为Spring容器指明一个构造器，通过构造器来实现依赖注入，这样，我们就将依赖注入的时机提前到了对象构造时。以XML配置方式为例，构造器注入与setter注入的操作方式极为类似，无非就是用`constructor-arg`标签替换`property`标签：

```xml
<bean id = "userService" class = "com.test.service.UserService">
    <constructor-arg name="userDao" ref="userDao1"/>
    <constructor-arg name="number" value="666"/>
</bean>

<bean id="userDao1" class="com.test.dao.UserDao"/>
```

当然，前提是在UserService中要存在相应的构造器才行，构造器的参数名要和`constructor-arg`标签中的`name`属性的值保持一致。这样Spring容器才能找到正确的构造器并通过它来创建对象：

```java
public class UserService {
    private UserDao userDao;
    private int number;

    //Spring容器调用该构造器创建对象的同时也完成了依赖注入
    public UserService(UserDao userDao, int number) {
         this.userDao = userDao;
         this.number = number;
    }
}
```

### 3.2 基于注解的配置

我们可以采用在类上添加注解的形式代替在XML中通过一个个\<bean>标签来配置Bean。

通过在类上添加如下四个注解都能让Spring容器把它们注册为Bean：

| 注解        | 说明                     |
| ----------- | ------------------------ |
| @Component  | 将类标识为一个普通的Bean |
| @Service    | 将类标识为服务层的Bean   |
| @Repository | 将类标识为持久层的Bean   |
| @Controller | 将类标识为控制层的Bean   |

如果不指定Bean的名称，Spring容器会自动生成一个名称，默认为类名首字母小写，当然，我们也可以明确指定一个名称：

```java
@Component("helloBean")
public class Hello {
}
```

比如，我们可以通过下面的这种形式来实现UserService的注册与装配：

```java
@Service
public class UserService {
    @AutoWired
    private UserDao userDao;
    @Value(666)
    private int number;
}
```

使用`@Autowired`就相当于把指定类型的Bean注入到指定的字段中。和XML配置相比，`@Autowired`大幅简化了注入，因为它不但可以写在setter方法上，还可以直接写在字段上，甚至可以写在构造方法中。`@Value`用来注入普通变量。

上面这种通过注解来实现Bean的注册与配置有一个前提，就是得声明一个Java配置类，并开启注解扫描：

```java
@Configuration
@ComponentScan
public class MainConfiguration {
}
```

`@ComponentScan`用来告诉容器，自动扫描当前类所在的包以及子包，也可以指定具体要扫描的包。

其实注解扫描在XML文件中也能开启，但不如配置类来的简单，况且我们通过注解配置的一个目的就是为了替代掉XML文件，所以这里就不再赘述如何通过XML来开启注解扫描了。

### 3.3 基于Java类的配置

从Spring Framework 3.0 开始，我们可以使用Java类来代替XML文件，只需要在Java类上加一个@Configuration注解，就将该Java类标识为了一个配置类，它可以代替XML文件来实现一些配置工作。

上面我们介绍了可以通过这样一个配置类来开启组件扫描功能，以通过注解实现Bean的注册与配置，其实还可以在配置类中就完成Bean的注册与配置。

比如，我们可以像下面这样来配置一个Bean：

```java
@Configuration
public class MainConfiguration {
    @Bean
    public Student student(){
        return new Student();
    }
}
```

如果要注入依赖，我们可以直接将其作为形参放到方法中：

```java
@Configuration
public class MainConfiguration {
    @Bean
    public Teacher teacher(){
        return new Teacher();
    }

    @Bean
    public Student student(Teacher teacher){
        return new Student(teacher);
    }
}
```

上面的这种配置方式主要是用来注册第三方Bean的，试想一下，如果一个Bean不在我们自己的package管理之内，我们如何将它注册进容器，扒出它的源码然后给它加个`@Component`注解？很明显不太现实，所以通过上面这种配置方式，我们就可以很轻松地讲第三方Bean注册进来。

## 4. Bean的个性化定制

除了以上这样简单的将某个对象注册为Bean之外，还可以在注册Bean的时候根据需要个性化的对Bean进行一些定制：

比如，在基于XML配置的方式下，除了指明Bean的`id`和`class`之外，还有很多其他的可供配置的属性：

```xml
<bean id = "xxx" name ="xxx" class = "xxx" scope = "xxx" lazy-init = "xxx" depends-on = "xxx" init-method = "xxx" destory-method = "xxx"/>
```

其中：

* `name`：指定Bean的别名。

* `scope`：singleton单例模式，对于一个Bean，容器只创建一次，每次通过容器获取的都是同一个Bean；

  ​	       prototype原型模式，每通过容器获取一次Bean，就会创建一个新的Bean。

* `lazy-init`：懒加载，设置为true则容器只在第一次获取Bean时创建这个Bean。

* `depends-on`：指明依赖的Bean，告诉容器正确的初始化顺序。

* `init-method`：指定初始化方法。

* `destory-method`：指定销毁方法。

再比如，基于注解或Java类的配置，也有类似的注解可供选择：

```java
@Repository("userDao")
@Scope("prototype") //原型模式  
public class UserDao {
    @PostConstruct //指明初始化方法
    public void init() {
        System.out.println("init...");
    }

    @PreDestroy //指明销毁方法
    public void destroy() {
        System.out.println("destroy...");
    }
}
```

```java
@Configuration
public calss Config {
    @Bean("xiaoming") //起别名
    @Scope("prototype") //原型模式  
    public Student student(){
        return new Student();
    }
    
    @Bean
    @Qualifier("xiaohong") //起别名
    @Lazy(true) //开启懒加载
    public Student student(){
        return new Student();
    }
}
```

## 5. 从容器中获取Bean

### 5.1 ApplicationContext

注册与配置完Bean之后，我们需要让Spring容器读取我们的配置文件来加载Bean，以及在加载完Bean之后，我们应该能从容器中获取到Bean，也就是说，Spring容器应该提供一个对外的接口来供我们操作。

我们可以用下面的代码来创建一个Spring容器：

```java
ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
```

可以看到，`ApplicationContext`就是Spring容器，它是一个接口，常用的实现类有：

* `ClassPathXmlApplicationContext`：它可以加载类路径下的配置文件；
* `FileSystemXmlApplicationContext`：它可以加载磁盘任意路径下的配置文件；
* `AnnotationConfigApplicationContext`：它用于读取注解来创建容器。

获得了`ApplicationContext`的实例，就获得了IoC容器的引用。现在我们可以从容器中获取Bean了，可以根据Bean ID进行获取，但更多的时候我们会根据Bean的类型来获取：

```java
UserService userService = context.getBean(UserService.class);
```

### 5.2 BeanFactory

Spring还提供另一种IoC容器叫`BeanFactory`，使用方式和`ApplicationContext`类似：

```java
BeanFactory factory = new XmlBeanFactory(new ClassPathResource("application.xml"));
```

`BeanFactory`和`ApplicationContext`的区别在于，`BeanFactory`的实现是按需创建，即第一次获取Bean时才创建这个Bean，而`ApplicationContext`会一次性创建所有的Bean。

实际上，`ApplicationContext`接口是从`BeanFactory`接口继承而来的，并且，`ApplicationContext`提供了一些额外的功能，包括国际化支持、事件和通知机制等。通常情况下，我们总是使用`ApplicationContext`，很少会考虑使用`BeanFactory`。

## 6.  AOP理论基础

AOP（Aspect Oriented Programming），即面向切面编程。

和面向对象编程OOP一样，AOP也是一种编程范式。不同的是，OOP把系统看作是多个对象之间的交互，每个对象可能完成多个功能，不同的对象之间可能有重复的功能；而AOP把系统视作由不同的关注点，或者称为切面组成，每个切面专注于完成一项功能。AOP的目的是通过分离横切关注点来提升代码的模块化程度。

这里提到的关注点，其实就是一段特定的功能，有些关注点出现在多个模块中，就称为横切关注点。这么说可能有点抽象，举个例子，一个后台客服系统的每个模块都需要记录客服的操作日志，这就是一个能从业务逻辑中分离出来的横切关注点，完全不用交织在每个模块的代码中，可以作为一个单独的模块存在。

在AOP中有几个重要的概念，在开始实践之前，有必要先来了解一下：

| 概念          | 说明                                                     |
| ------------- | -------------------------------------------------------- |
| Aspect        | 切面，即一个横跨多个核心逻辑的功能，或者称之为系统关注点 |
| Joinpoint     | 连接点，即定义在应用程序流程的何处插入切面的执行         |
| Pointcut      | 切入点，即一组连接点的集合                               |
| Advice        | 通知，指特定连接点上执行的动作                           |
| Target Object | 目标对象，即真正执行业务的核心逻辑对象                   |
| AOP Proxy     | AOP代理对象，是客户端持有的增强后的对象                  |

实际上，AOP就是通过对目标对象的目标方法进行代理，从而实现方法的增强。方法的增强指的是在方法原有功能的基础上增加其他一些功能。这样就可以让方法专注于实现它的核心功能，一些与核心功能不相干的代码交给代理对象去做。

## 7.  AOP的使用

首先，我们通过Maven引入Spring对AOP的支持：

- org.springframework:spring-aspects:6.0.0

上述依赖会自动引入AspectJ，使用AspectJ实现AOP比较方便，因为它的定义比较简单。

### 7.1 定义切面类

我们可以通过`@Aspect`注解来定义一个切面类，切面类就是用来定义增强方法的：

```java
@Aspect
@Component
public class LogAspect {
    //在执行UserService的每个方法前执行:
    @Before("execution(public * com.test.service.UserService.*(..))")
    public void log() {
        System.out.println("print log before method");
    }
}
```

与此同时，我们需要给配置类加上一个`@EnableAspectJAutoProxy`注解：

```java
@Configuration
@EnableAspectJAutoProxy
public class Configuration {...}
```

Spring容器看到这个注解，就会自动查找带有`@Aspect`的Bean，并自动生成相应的AOP代理类：

```java
public UserServiceAopProxy extends UserService {
    private UserService target;
    private LogAspect aspect;

    public UserServiceAopProxy(UserService target, LoggingAspect aspect) {
        this.target = target;
        this.aspect = aspect;
    }

    public User login(String email, String password) {
        //先执行Aspect的代码
        aspect.log();
        //再执行UserService的逻辑
        return target.login(email, password);
    }

    public User register(String email, String password, String name) {
        //先执行Aspect的代码
        aspect.log();
        //再执行UserService的逻辑
        return target.register(email, password, name);
    }
}
```

AOP代理类取代了原始的`UserService`（原始的`UserService`实例作为内部变量隐藏在`UserServiceAopProxy`中）。如果我们打印从Spring容器获取的`UserService`实例类型，它类似`UserService$$EnhancerBySpringCGLIB$$1f44e01c`，实际上是Spring使用CGLIB动态创建的子类，但对于调用方来说，感觉不到任何区别。

> Spring对接口类型使用JDK动态代理，对普通类使用CGLIB创建子类。如果一个Bean的class是final，Spring将无法为其创建子类。

### 7.2 声明切入点

#### 7.2.1 通过execution表达式

声明切入点就是声明我们要拦截的那个目标方法，一种方式是通过在切面类中声明切入点（当然也可以在任意一个类中声明，这个无关紧要），切入点的声明依托于一个无实际意义的方法，该方法无参数、无返回值、无方法体。在这样一个方法上添加一个@Pointcut注解，并在注解中通过切入点表达式指明切入点，即我们要切入的那个方法，就像下面这样：

```java
@Aspect
public class MyAspect {
    @Pointcut("execution(public * update())") //指明切入点为所有public的update方法
    public void pt() {}
    
    @Before("pt()")
    public void before() {
        System.out.println("Before Advice");
    }
}
```

另一种更简单的方式就像上面定义切面类时演示的那样，直接在`@Before`等注解后面声明切入点：

```java
@Aspect
public class MyAspect {
    @Before("execution(public * update())")
    public void before() {
        System.out.println("Before Advice");
    }
}
```

#### 7.2.2 通过自定义注解

我们在使用AOP时，要注意到虽然Spring容器可以通过execution表达式定位到目标方法并生成AOP代理对其增强，但是，有可能因为execution表达式中定义了不恰当的范围，导致意想不到的结果，即很多不需要AOP代理的Bean也被自动代理了，并且，后续新增的Bean，如果不清楚现有的AOP装配规则，容易被纳入AOP代理范围。

使用AOP时，被装配的Bean最好自己能清清楚楚地知道自己被安排了。

我们以一个实际例子演示如何使用注解实现AOP装配。为了监控应用程序的性能，我们定义一个性能监控的注解：

```java
@Target(METHOD)
@Retention(RUNTIME)
public @interface MetricTime {
    String value();
}
```

在需要被监控的关键方法上标注该注解：

```java
@Component
public class UserService {
    //监控register()方法性能:
    @MetricTime("register")
    public User register(String email, String password, String name) {
        ...
    }
    ...
}
```

然后，我们定义`MetricAspect`：

```java
@Aspect
@Component
public class MetricAspect {
    @Around("@annotation(metricTime)")
    public Object metric(ProceedingJoinPoint joinPoint, MetricTime metricTime) throws Throwable {
        String name = metricTime.value();
        long start = System.currentTimeMillis();
        try {
            return joinPoint.proceed();
        } finally {
            long t = System.currentTimeMillis() - start;
            //写入日志或发送至JMX:
            System.err.println("[Metrics] " + name + ": " + t + "ms");
        }
    }
}
```

注意`metric()`方法标注了`@Around("@annotation(metricTime)")`，它的意思是，符合条件的目标方法是带有`@MetricTime`注解的方法，因为`metric()`方法参数类型是`MetricTime`（注意参数名是`metricTime`不是`MetricTime`），我们通过它获取性能监控的名称。

有了`@MetricTime`注解，再配合`MetricAspect`，任何Bean，只要方法标注了`@MetricTime`注解，就可以自动实现性能监控。

### 7.3 声明通知类型

在前面我们演示的切面类中，可以看到在每个增强方法上都用了像`@Before`、`@Around`等注解。这是什么意思呢？

其实方法的增强有多种情况，可以在目标方法执行之前执行增强方法，也可以在目标方法执行之后执行增强方法，还可以在目标方法执行前后都执行增强方法。在Spring AOP中，我们定义的增强方法也称为通知（Advice），所以我们在定义增强方法的时候，要考虑通知的类型，通过下面的这几种注解，可以声明不同的通知类型：

- `@Before`：这种拦截器先执行拦截代码，再执行目标代码。如果拦截器抛异常，那么目标代码就不执行了；
- `@After`：这种拦截器先执行目标代码，再执行拦截器代码。无论目标代码是否抛异常，拦截器代码都会执行；
- `@AfterReturning`：和@After不同的是，只有当目标代码正常返回时，才执行拦截器代码；
- `@AfterThrowing`：和@After不同的是，只有当目标代码抛出了异常时，才执行拦截器代码；
- `@Around`：能完全控制目标代码是否执行，并可以在执行前后、抛异常后执行任意拦截代码，可以说是包含了上面所有功能。

#### 7.3.1 前置通知

@Before注解可以用来声明一个前置通知，注解中可以引用事先定义好的切入点，也可以直接传入一个切入点表达式。被拦截到的方法开始执行前，会先执行该通知中的代码：

```java
@Aspect
public class MyAspect {
    @Before("execution(public * update())")
    public void before() {
        System.out.println("Before Advice");
    }
}
```

要是同时存在多个通知作用于同一处，可以让切面类实现Ordered接口，或者在上面添加@Order注解。指定的值越低，优先级越高。

#### 7.3.2 后置通知

一个方法执行后，可能正常返回，也可能抛出了异常。如果不关注执行是否成功，只是想在方法结束后做些动作，可以使用@After注解：

```java
@Aspect
public class MyAspect {
    @After("execution(public * update())")
    public void after() {
        System.out.println("After Advice");
    }
}
```

如果想要拦截正常返回的调用，可以使用@AfterReturing注解：

```java
@Aspect
public class MyAspect {
    @AfterReturing("execution(public * update())")
    public void afterReturing() {
        System.out.println("AfterReturing Advice");
    }
}
```

如果想要拦截抛出异常的调用，可以使用@AfterThrowing注解：

```java
@Aspect
public class MyAspect {
    @AfterThrowing("execution(public * update())")
    public void afterThrowing() {
        System.out.println("AfterThrowing Advice");
    }
}
```

#### 7.3.3 环绕通知

环绕通知功能比较强大，它可以在方法执行前和执行后都加入自己的逻辑，需要注意的是，环绕通知中需要显式的调用原始的方法并保持与原始方法相同的返回类型，我们可以使用@Around注解来声明一个环绕通知，它的第一个参数必须是ProceedingJoinPoint类型的。比较标准的一种写法如下：

```java
@Aspect
public class MyAspect {
    @Around("execution(public * update())")
    public Object around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("Before Advice");
        Object ret =  pjp.proceed();
        System.out.println("After Advice");
        return ret;
    }
}
```

### 7.4 个性化通知

现在我们已经知道如何通过声明切入点和通知来实现AOP了，可以发现，同一个通知往往会切入到好多不同的方法中，但是在某些情况下，我们希望针对不同的方法，采用更具有针对性的通知，或者说给不同的方法个性化的定制通知。这就需要我们能在通知中获取到原始方法的一些参数，比如方法调用时传入了什么参数，或是方法执行之后返回了什么，等等。

这个时候，我们可以在通知中添加一个JoinPoint类型的参数，通过此参数可以获取到原始方法的调用参数，获取到的是一个对象数组：

```java
@Aspect
public class MyAspect {
    @After("execution(public * update())")
    public void after(JoinPoint jp) {
        Object[] args = jp.getArgs();
        System.out.println(Arrays.toString(args));
    }
}
```

其实，环绕通知中的ProceedingJoinPoint参数就是JoinPoint的一个子类。

除了获取到原始方法的调用参数外，还可以通过其他的做法获取到原始方法的返回值，或者抛出的异常信息，具体可以自行了解。

## 8.  Spring中的数据库访问

数据库基本上是现代应用程序的标准存储，绝大多数程序都把自己的业务数据存储在关系数据库中，可见，访问数据库几乎是所有应用程序必备能力。我们都知道JDBC是Java程序访问数据库的标准接口，但使用起来代码比较繁琐。那么，下面我们就来看看Spring在数据库访问方面都给我们提供了哪些便捷：

- 提供了简化的JDBC的模板类，不必手动释放资源；
- 能方便地集成Hibernate、JPA和MyBatis这些数据库访问框架。

### 8.1 在Spring中使用JDBC

在Spring中使用JDBC，首先我们通过IoC容器创建并管理一个`DataSource`实例，然后，Spring提供了一个`JdbcTemplate`，可以方便地让我们操作JDBC，因此，通常情况下，我们会实例化一个`JdbcTemplate`。

我们以实际工程为例，先创建Maven工程`spring-data-jdbc`，然后引入以下依赖：

- org.springframework:spring-context:6.1.12
- org.springframework:spring-jdbc:6.0.0
- jakarta.annotation:jakarta.annotation-api:2.1.1
- com.zaxxer:HikariCP:5.0.1
- org.hsqldb:hsqldb:2.7.1

> 编写示例代码或者测试代码时，强烈推荐使用HSQLDB这个数据库，它是一个用Java编写的关系数据库，可以以内存模式或者文件模式运行，本身只有一个jar包，非常适合演示代码或者测试代码。

第一步，针对HSQLDB写一个配置文件`jdbc.properties`：

```properties
#数据库文件名为testdb:
jdbc.url=jdbc:hsqldb:file:testdb
#Hsqldb默认的用户名是sa，口令是空字符串:
jdbc.username=sa
jdbc.password=
```

第二步，在`AppConfig`中，我们需要创建以下几个必须的Bean：

```java
@Configuration
@ComponentScan
@PropertySource("jdbc.properties")
public class AppConfig {

    @Value("${jdbc.url}")
    String jdbcUrl;
    @Value("${jdbc.username}")
    String jdbcUsername;
    @Value("${jdbc.password}")
    String jdbcPassword;

    @Bean
    DataSource createDataSource() {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl(jdbcUrl);
        config.setUsername(jdbcUsername);
        config.setPassword(jdbcPassword);
        config.addDataSourceProperty("autoCommit", "true");
        config.addDataSourceProperty("connectionTimeout", "5");
        config.addDataSourceProperty("idleTimeout", "60");
        return new HikariDataSource(config);
    }

    @Bean
    JdbcTemplate createJdbcTemplate(DataSource dataSource) {
        return new JdbcTemplate(dataSource);
    }
}
```

接下来，我们只需要在需要访问数据库的Bean中，注入`JdbcTemplate`即可：

```java
@Component
public class UserService {
    @Autowired
    JdbcTemplate jdbcTemplate;
    ...
}
```

`JdbcTemplate`中的方法有很多，这里我们不一一介绍。需要强调的是，`JdbcTemplate`只是对JDBC操作的一个简单封装，它的目的是尽量减少手动编写`try(resource) {...}`的代码，对于查询，主要通过`RowMapper`实现了JDBC结果集到Java对象的转换。

最后，我们总结一下`JdbcTemplate`的用法，那就是：

- 针对简单查询，优选`query()`和`queryForObject()`，因为只需提供SQL语句、参数和`RowMapper`；
- 针对更新操作，优选`update()`，因为只需提供SQL语句和参数；
- 任何复杂的操作，最终也可以通过`execute(ConnectionCallback)`实现，因为拿到`Connection`就可以做任何JDBC操作。

### 8.2 Spring中的事务管理

Spring中提供了两种事务管理的方式，分别是编程式事务管理和声明式事务管理。

#### 8.2.1 编程式事务管理

编程式事务管理就是通过 `TransactionTemplate`或者`TransactionManager`手动管理事务，实际应用中很少使用，但是对于理解 Spring 事务管理原理有帮助。

使用`TransactionTemplate` 进行编程式事务管理的示例代码如下：

```java
@Autowired
private TransactionTemplate transactionTemplate;

public void testTransaction() {
    transactionTemplate.execute(new TransactionCallbackWithoutResult() {
        @Override
        protected void doInTransactionWithoutResult(TransactionStatus transactionStatus) {
            try {
                //一组数据库相关操作
            } catch (Exception e){
                transactionStatus.setRollbackOnly();//回滚事务
            }
        }
    });
}
```

使用 `TransactionManager` 进行编程式事务管理的示例代码如下：

```java
@Autowired
private PlatformTransactionManager transactionManager;

public void testTransaction() {
    TransactionStatus status = transactionManager.getTransaction(new DefaultTransactionDefinition());
    try {
        //一组数据库相关操作
        transactionManager.commit(status);//提交事务
    } catch (Exception e) {
        transactionManager.rollback(status);//回滚事务
    }
}
```

在Spring中，要想像上面这样进行事务管理，就需要我们在`AppConfig`中，定义一个`TransactionTemplat`或者`PlatformTransactionManager`对应的Bean：

```java
@Configuration
@ComponentScan
public class AppConfig {
    ...
    @Bean
    PlatformTransactionManager createTransactionManager(DataSource dataSource) {
    	return new DataSourceTransactionManager(dataSource);//这里选择DataSourceTransactionManager实现类
   	}
}
```

#### 8.2.2 声明式事务管理

声明式事务管理将事务管理的相关代码从业务方法中抽离了出来，以声明式的方式来实现事务管理，对于开发者来说，声明式事务显然比编程式事务更易用、更好用。

我们只需在需要事务支持的方法上，添加一个`@Transactional`注解：

```java
@Transactional
public void testTransaction() {
    //一组数据库相关操作
}
```

添加了`@Transactional`注解意味着该方法中的所有数据库操作都处于同一个事务管理下，要么同成功，要么同失败。

在上面的代码中，我们并没有手动开启事务、提交事务和判断是否回滚，那该方法是如何通过一个注解就实现事务支持了呢？其实原理就是AOP，在AOP生成的代理类中增添了事务处理的代码。

在Spring中，要使用声明式事务管理，除了在`AppConfig`中定义一个`PlatformTransactionManager`外，还要再加一个`@EnableTransactionManagement`注解：

```java
@Configuration
@ComponentScan
@EnableTransactionManagement //启用声明式事务管理
public class AppConfig {
    ...
    @Bean
    PlatformTransactionManager createTransactionManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
}
```

以上就是Spring的两种事务管理方式，可以看出，声明式事务虽然优于编程式事务，但也有不足，声明式事务管理的粒度是方法级别，而编程式事务是可以精确到代码块级别的。

### 8.3 Spring整合MyBatis

首先，我们要引入MyBatis本身，其次，由于Spring并没有像Hibernate那样内置对MyBatis的集成，所以，我们需要再引入MyBatis官方自己开发的一个与Spring集成的库：

- org.mybatis:mybatis:3.5.11
- org.mybatis:mybatis-spring:3.0.0

和前面一样，先创建`DataSource`是必不可少的：

```java
@Configuration
@ComponentScan
@PropertySource("jdbc.properties")
public class AppConfig {
    @Bean
    DataSource createDataSource() { ... }
}
```

使用MyBatis的核心就是创建`SqlSessionFactory`，这里我们需要创建的是`SqlSessionFactoryBean`：

```java
@Bean
SqlSessionFactoryBean createSqlSessionFactoryBean(DataSource dataSource) {
    SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
    sqlSessionFactoryBean.setDataSource(dataSource);
    return sqlSessionFactoryBean;
}
```

下面就可以使用MyBatis啦。

我们来尝试编写一个`UserMapper`：

```java
public interface UserMapper {
	@Select("SELECT * FROM users WHERE id = #{id}")
	User getById(@Param("id") long id);
}
```

有了`UserMapper`接口，还需要对应的实现类才能真正执行这些数据库操作的方法。MyBatis提供了一个`MapperFactoryBean`来自动创建所有Mapper的实现类。可以用一个简单的`@MapperScan`注解来启用它：

```java
@Configuration
@ComponentScan
@MapperScan("com.test.mapper")
@PropertySource("jdbc.properties")
public class AppConfig {
    @Bean
    DataSource createDataSource() { ... }
}
```

这样就可以让MyBatis自动扫描指定包的所有Mapper并创建实现类。于是在真正的业务逻辑中，我们可以直接注入使用。
