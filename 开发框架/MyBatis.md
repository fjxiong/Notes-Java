# MyBatis

## 1. MyBatis简介

MyBatis 是一款优秀的持久层框架，用于简化 Java 应用程序与数据库的交互。它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。

MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。它在保证灵活性和高性能的同时，提供了一个半自动化的 ORM（Object Relational Mapping）解决方案。与全自动的 ORM 工具如 Hibernate 不同，MyBatis 允许开发者对 SQL 进行更细粒度的控制，使得复杂查询和数据库优化变得更加容易。

## 2. MyBatis入门

### 导入MyBatis依赖

在使用 MyBatis 之前，我们需要在项目中引入 MyBatis 的依赖。如果是 Maven 项目，`pom.xml` 文件中可以加入以下依赖：

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.9</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.28</version>
</dependency>
```

### 编写MyBatis核心配置文件

MyBatis的使用需要依靠一个核心配置文件，用来定义数据库连接的相关信息以及决定事务作用域和控制方式的事务管理器等。我们可以在类路径下的Resources目录下定义一个`mybatis-config.xml`文件，以下是一个简单的示例：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis_demo"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    
    <mappers>
        <mapper resource="com/example/mapper/UserMapper.xml"/>
    </mappers>
</configuration>
```

当然，还有很多可以在 XML 文件中配置的选项，上面的示例仅罗列了最关键的部分。 注意 XML 头部的声明，它用来验证 XML 文档的正确性。environment 元素体中包含了事务管理和连接池的配置。mappers 元素则包含了一组映射器（mapper），这些映射器的 XML 映射文件包含了 SQL 代码和映射定义信息。

### 定义Mapper接口

Mapper接口用来定义一系列与数据库操作相关的方法，MyBatis最终会让接口方法与对应的SQL语句绑定起来，并通过代理自动生成接口的实现类，我们在进行数据库操作时，只需调用相关接口方法便可实现相应的操作。以下是一个Mapper接口的示例，它主要用来定义针对User表的SQL操作，我们命名为`UserMapper`：

```java
public interface UserMapper {
    //查询所有用户
    List<User> getAllUsers();

    //新增用户
    void insertUser(User user);
}
```

### 在XML中定义SQL语句

MyBatis允许我们把SQL语句集中地定义在一个XML文件中。比如，我们可以在`UserMapper.xml`中定义一组针对User表的SQL语句：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.mapper.UserMapper">
    
    <select id="getAllUsers" resultType="com.example.entity.User">
       select * from user
    </select>

    <insert id="insertUser" parameterType="com.example.entity.User">
        insert into user (name, age) values (#{name}, #{age})
    </insert>
    
</mapper>
```

这里需要注意，MyBatis为了实现自动生成Mapper接口实现类，将SQL语句绑定到各个接口方法上，有以下几点要求：

* SQL映射文件的命名空间需要和Mapper接口的全类名一致
* 每个SQL语句的id要和Mapper接口中的抽象方法名一致

* SQL映射文件要和Mapper接口处在统一路径下

其中，针对最后一点要求我们并不用将UserMapper.xml放到源码目录下的UserMapper所在的包中，我们可以在Resources目录下新建一个和UserMapper所在的包一样的路径，这样在编译后，它们就会被放在同一路径下了。

### 通过注解定义SQL语句

我们也可以直接在Mapper接口的方法上通过注解来定义一条SQL，并实现SQL与该方法的绑定。但这种方法只适用于简单的SQL，对于复杂一点的SQL，还是推荐在XML中定义。以下是一个通过注解定义SQL的示例：

```java
public interface UserMapper {
    //查询所有用户
    @Select("select * from user")
    List<User> getAllUsers();

    //新增用户
    @Insert("insert into user (name, age) values (#{name}, #{age})")
    void insertUser(User user);
}
```

### 执行数据库操作

每个基于MyBatis的应用都是以一个SqlSessionFactory的实例为核心的。SqlSessionFactory的实例可以通过SqlSessionFactoryBuilder 获得，而SqlSessionFactoryBuilder则可以读取XML配置文件来构建出SqlSessionFactory实例。MyBatis包含一个名叫Resources的工具类，它包含一些实用方法，使得从类路径或其它位置加载资源文件更加容易。

有了SqlSessionFactory对象，我们就可以通过它获得SqlSession对象，SqlSession对象提供了在数据库执行SQL命令所需的所有方法，通过它，我们可以直接执行映射的SQL语句，但更好的方式是使用和指定语句的参数和返回值相匹配的接口方法，就像下面这样：

```java
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

SqlSession sqlSession = sqlSessionFactory.openSession();
UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

//新增用户
User user = new User("zhangsan",18);
userMapper.insertUser(user);
sqlSession.commit();

//查询所有
List<User> users = userMapper.getAllUsers();
System.out.println(users);

sqlSession.close();
```

## 3. MyBatis小结

MyBatis 是一个灵活、轻量的持久层框架，特别适用于需要对 SQL 有高度控制的项目。在理解了 MyBatis 的基本配置和操作后，可以更深入地学习动态 SQL、高级映射、缓存管理等特性，进一步提高开发效率。