# Spring

### 1、 怎么理解 Spring 中的 IOC 容器？

```text
1、IOC是Spring中一大核心思想，指的是把对象的创建权限转交给Spring容器。
2、IOC到底是什么样的思想？
    a)之前都是开饭人员自己new对象，生命周期都是开发人员自己负责。
    b)把对象的创建，对象的初始化，对象的生命周期全部交给Spring容器的管理(工厂)
    c)bean的得到了统一的管理
3、对象的创建
```

### 2、 怎么理解 Spring 中的依赖注入(DI)？

```text
1、DI指的是依赖注入，某个bean依赖了spring容器中的bean
2、bean和benan之间的依赖关系
```

### 3、 怎么理解 Spring 中的AOP？

```text
1、AOP是Spring中的另一个核心思想
2、AOP的思想面向切面编程
    a)思想：在不改变的代码的情况下，动态的在某个方法之前或者之后干点事情。
    b)实现
        a)动态代理
            1)jdk
            2)cglib
3、AOP的使用场景
     a)日志记录，事务的管理，权限的控制，异常的处理。。。。
```

### 4、 Spring 通知类型有哪些？

```text
1、前置通知
2、后置通知(出现异常会调用)
3、环绕通知
4、抛出异常通知
5、后置通知(出现异常不调用)
```

### 5、 @Value 注解的作用是什么？

```text
1、给变量赋值
2、根据key读取属性文件
```

### 6、 Spring 中 bean 的作用域有几种类型？

```text
1、singleton(单列，默认值)，整个容器中只有一个实例
2、prototype(原生)，每次从容器中获取都会创建一个实例
--------在web环境下有作用------------
3、request：代表每次一个请求都会创建一个实例
4、session:每个session对象创建一个实例
```

### 7、 @Component 和 @Bean 有什么区别？

```text
1、相同点都可以实例化一个bean，放入到IOC容器中
2、区别
    a)作用域不一样
        a)@Component是放到类类上面的，表示把这个bean交给IOC容器管理，默认bean的id是类名是类名首字母小写。
        b)@Bean:是放在方法上面的，表示把方法得分返回值放入IOC容器中，方法的名称就是bean的id
```

### 8、 Spring 注入方式有哪些？

```text
1、配置文件
    a)手动注入<proerpty name="userDao" ref="userDao"> -->set方式注入
    b)构造器注入
    c)自动注入 -- set方式注入
    d)静态工厂注入:直接使用类名调用就可以
    e)非静态工厂注入:先要实例化工厂，然后在调用
2、注解
    a)使用注解
3、总结
    a)set方式注入
    b)构造器注入
    c)注解注入(官方推荐)
```

### 9、 在 Spring 中如何操作数据库？

```text
1、JdbcTemplate(工具类):spring操作数据库的模板类
2、SpringDataJPA:操作数据库的框架，它是基于JPA(基于一套注解实现的)实现的。
    a)getUserById(); getUserByUsernameOrPassword("admin","admin");
```

### 10、Spring 有几种实现事务的方式？

```text
1、编程式事务:写代码来控制事务提交和回滚，处理事务的代码和处理业务逻辑的代码耦在一起了。
2、声明式事务:利用AOP了的思想
    a)xml方式
    b)注解方式
3、spring-tx.jar
```

### 11、 Spring 的 JdbcTemplate 对象和 JDBC 有什么区别？

```text
1、JDBC是Java操作数据的一个规范
2、JdbcTemplate对JDBC做了一封装，调用起来更加的简单
3、JdbcTemplate封装了JDBC后的好处有哪些？
    a)提高了开发效率
    b)使用的时候需要传递数据源
    c)线程安全的
    d)会自动的释放资源(jdbcTemplate.udpate("sql","",""))
```

### 12、 Spring 事务隔离级别有哪些？

```text
        a)事务概念
		1)数据库操作的最小工作单元
	b)事务的特性
		a)原子性:最小的操作，不能在拆分
		b)一致性:事务提前之前和之后的状态保持一致
		c)隔离性:事务和事务之间的隔离级别
		c)持久性:事务一旦提交，对数据的修改是永久性的
	c)事务的隔离级别(理解)
		a)读未提交
		b)可重复读:在一个事务中读取结果不一样
		c)读已提交
		d)序列化
	d)事务的隔离级别不同会出现一下几种情况
		a)脏读:读到了另一个事务没有提交的数据
		b)幻读:幻读是事务非独立执行时发生的一种现象,一个事务在做所有列的修改，另一个事务在做插入。
		c)不可重复读：在同一个事务中多次读取数据结果不一致
	e)什么情况下会考虑到事务
		a)在一个业务方法中多次对数据库进行修改
	f)事务的传播属性：
		1)所谓spring事务的传播属性，就是定义在存在多个事务同时存在的时候，spring应该如何处理这些事务的行为
		2)Propagation.REQUIRED（required）：支持当前事务，如果当前有事务， 那么加入事务， 如果当前没有事务则新建一个(默认情况)
		3)Propagation.NOT_SUPPORTED（not_supported) ： 以非事务方式执行操作，如果当前存在事务就把当前事务挂起，执行完后恢复事务（忽略当前事务）；
		4)Propagation.SUPPORTS (supports) ：如果当前有事务则加入，如果没有则不用事务。
		5)Propagation.MANDATORY (mandatory) ：支持当前事务，如果当前没有事务，则抛出异常。（当前必须有事务）
		6)PROPAGATION_NEVER (never) ：以非事务方式执行，如果当前存在事务，则抛出异常。（当前必须不能有事务）
		7)Propagation.REQUIRES_NEW (requires_new) ：支持当前事务，如果当前有事务，则挂起当前事务，然后新创建一个事务，如果当前没有事务，则自己创建一个事务。
		8)Propagation.NESTED (nested 嵌套事务) ：如果当前存在事务，则嵌套在当前事务中。如果当前没有事务，则新建一个事务自己执行（和required一样）。嵌套的事务使用保存点作为回滚点，当内部事务回滚时不会影响外部事物的提交；但是外部回滚会把内部事务一起回滚回去。（这个和新建一个事务的区别）
```



![img](https://pic2.zhimg.com/80/v2-845903c2a3b581c9365db831e32562b1_1440w.jpg)

### 13、 Spring 中的 Bean 是线程安全的吗？

```text
1)要明白什么线程安全的问题
	a)商品的超卖问题，已经卖出去了100个，结果库存才减少了1个
2)线程安全问题是怎么导致的
	a)多线程情况下会出现多个线程操作同一个资源(取值，计算，赋值不是原子性)
3)锁就是用来解决线程安全的问题(并发的问题)
4)因为Spring创建的Bean默认是单列
	a)如果是数据是放在在成员变量的(类中的属性)，线程是不安全的
	b)如果数据是放在局部(方法中)，线程是安全的
```

### 14 、 Spring 有哪些优点?

```text
1、两大核心思想AOP，IOC，解决了bean的创建和依赖的关系，aop帮助我们实现解耦。
2、Spring对事务的支持也是非常的好
3、Spring整合第三方框架也是非常的简单
4、使用Spring后可以降低调用API的难度
5、Spring这个大家族对Web，数据库，权限，微服务都有支持
```

### 15、 Spring、SpringBoot、SpringCloud 的区别是什么

```text
1、spring是framework下面的项目，提供了最基础的服务。
2、SpringMVC是Spring提供对Web的支持
3、SpringBoot:快速的搭建Spring应用的程序，里面的思想就是约定大于配置，主要就是解决springmvc中配置文件太多的情况。
4、SpringCloud:是Spring提供对微服务的支持，里面提供了一整套的解决方案。
5、SpringSecurity:是Spring提供的一个安全的框架
```

### 16、 Spring 中使用的设计模式有哪些

```text
1)你了解设计模式吗?设计模式有什么作用？
	a)了解
	b)项目的架构变的非常的清晰，后期需求发送变化后只需要修改很少的代码即可完成。
	b)面(架构就非常的清晰)和点(写代码非常的麻烦，一个方法可以搞定的事情要写3各类)的关系
2)你知道的设计模式有那些？
	a)设计模式总共为23中分为3类
	b)结构性
		a)适配，代理，门面，装饰
	c)创建性
		1)工厂，单列
	c)行为性
		a)观察者，模板
3)你项目中用当过设计模式？或者你熟悉的框架中都用了那些设计模式
	a)Spring
	    1)工厂，代理，单列，模板
	b)SpringMVC
	    2)责任链模式
```

### 17、 解释SpringJDBC，SpringORM，SpringWeb模块作用

```text
1、SpringJDBC:spring对JDBC的支持，提供里面了一个模板，使用模板的方式来操作数据库。(JdbcTemplate)
2、SpringORM:Spring提供对JPA层框架的整合。
    a)ORM:对象关系映射
    b)JPA:基于一套注解和面向对象的思想去操作的数据
        1)getUserByUsernameAndPassword();
3、SpringWeb:spring对web的支持
4、spring-tx:sprig提供对事务的支持
5、spring-aop:切面编程的支持
6、spring-beans:bean的工厂的创建都在这个模块里面
7、spring-core:提供IOC支持
8、spring-test:和单元测试的支持
9、spring-exprexxx：
```

![img](https://pic2.zhimg.com/80/v2-81c964abb40b3a2ed626b8f0093acdb1_1440w.jpg)

### 18、 ApplicationContext实现类有哪些？

```text
1、ClasspathXmlApplicationContext("classpath:beas.xml")
    a)从classpath中读取spring配置文件
2、FileSystemXmlApplicationContext("d:/beans.xml")
    a)从决定路径中读取spring的配置文件
3、WebApplicationContext：在Web环境下初始化Spring容器
4、Web中监听器
    a)对Web容器的监听
        a)web容器创建和销毁：ServletContextListener
        b)web作用域：ServletContextAttributeListener
    b)对requset监听
        a)request创建和销毁
        b)request作用域
    c)对session监听
        a)session创建和销毁
        b)session作用域
```

### **BeanFactory和ApplicationContext的区别?**

```text
 BeanFactory：是Spring里面最低层的接口，提供了最简单的容器的功能，只提供了实例化对象和拿对象的功能；
 ApplicationContext：应用上下文，继承BeanFactory接口，它是Spring的一各更高级的容器，提供了更多的有用的功能；
     1) 国际化（MessageSource）
     2) 访问资源，如URL和文件（ResourceLoader）
     3) 载入多个（有继承关系）上下文 ，使得每一个上下文都专注于一个特定的层次，比如应用的web层  
     4) 消息发送、响应机制（ApplicationEventPublisher）
     5) AOP（拦截器）
```

利用BeanFactory获取bea

```java
 //XmlBeanFactory是典型的BeanFactory。
  BeanFactory factory = new XmlBeanFactory("XXX.xml");
  //获取一个叫做mdzz的bean。在这个时候进行实例化。
  factory.getBean("java");
```

重点：当我们使用BeanFactory去获取Bean的时候，我们只是实例化了该容器，而该容器中的bean并没有被实例化。当我们getBean的时候，才会实时实例化该bean对象。

利用ApplicationContext获取bean

```java
 //当我们实例化XXX.xml的时候，该文件中配置的bean都会被实例化。（该bean scope是singleton）
 ApplicationContext appContext = new ClassPathXmlApplicationContext("XXX.xml");
```

重点：当我们使用ApplicationContext去获取bean的时候，在加载XXX.xml的时候，会创建所有的配置bean。

区别总结

```text
 <1>如果使用ApplicationContext，如果配置的bean是singleton，那么不管你有没有或想不想用它，它都会被实例化。好处是可以预先加载，坏处是浪费内存。
 <2>BeanFactory，当使用BeanFactory实例化对象时，配置的bean不会马上被实例化，而是等到你使用该bean的时候（getBean）才会被实例化。好处是节约内存，坏处是速度比较慢。多用于移动设备的开发。
 <3>没有特殊要求的情况下，应该使用ApplicationContext完成。因为BeanFactory能完成的事情，ApplicationContext都能完成，并且提供了更多接近现在开发的功能。
```



### 19、 Spring框架中的单例bean是线程安全的吗？

```text
不安全的
```

# Spring MVC

### 20、 简述一下 Spring MVC 的执行流程？

```text
1、DispatcherServlet:前端控制器，所有的请求都要经常前端控制器处理
2、HandlerMapping: 根据请求获得HandlerMapping对象
3、HandlerExecutionChain:这在对象包含要执行的拦截器和Controller
4、HandlerAdapter:真真要调用的conroller
5、调用拦截器中的前置方法
6、调用后端处理器(Contrller),返回ModelAndView对象
7、ModelAndView:调用后端处理器后返回ModelAndView对象,在这个对象中包含了要返回的视图名称，Model数据
8、调用拦截器中Controller执行之后的方法
9、ViewResolver：视图解析器，根据视图名称解析视对象
    a)从MV中获取视图名称
    b)根据视图视图名称获取视图对象
    c)渲染视图(把Model中的数据填充到视图中，然后把视图的HTML响应出去)
10、调用拦截器中的视图解析之完成的方法
```

### 21、 如何实现跨域访问？

```text
1、为什么会出现跨域？
    a)同源策略：协议相同，域名相同，端口相同
    b)浏览器必须先要满足同源后才能接收到这个请求返回到的响应
    c)JavaScript基于安全的考虑
2、前端解决方式
    a)<script>标签是不受跨域影响,只要herf,src属性的标签都不收跨域的影响
    b)利用JSONP
        a)实现JSONP能实现的跨域的原理
            1)底层利用script实现，发送请求的传递callback的参数
            2)服务端可以到这个参数，给这个参数加上一个()然后直接返回给浏览器
            3)浏览器接收到返回的内容后就会解析成一个js的函数调用，前提先要定义这个函数
3、后端解决的方式
    a)@CrossOrigin：给响应头这添加一个地址
    b)后端统一在网关中解决跨域问题
    c)使用SpringBoot一个CrosFilter，原理就是给响应头中设置了一个属性
```

### 22、 以下代码访问地址该怎么写？

```java
@RequestMapping(value="/list"params={"age=10"}
public String list(){
   // do something
}
url: xxxxxx/list?age=10
   @RequestMapping(
            value= "/login", // 映射地址
            method = RequestMethod.GET, // 青青方式
            params = {"age=10"}, // url必须要携带的参数
            headers = "applciatin/json", // 请求头中必须要携带的参数
            produces = "text/htm;charset=utf-8", // 服务端响应的数据的类型以及编码
            consumes = "applciatino/json" // 我只能接收json的数据
    )
```

### 23、访问以下接口不传递任何参数的情况下，执行的结果是？

```java
@RequestMapping(value="/list")
@ResponseBody
public String list(int id){
  return "id="+id;
}
在方法list接口没有传递的情况下，参数时null值，因为方法接收的是int类型，所以无法赋值。
```

### 24、 Spring MVC 的常用注解有哪些？

```text
1、@Controller
2、RestController
3、RequsetMapping
4、ResponseBody
5、RequsetParam
6、RequsetBody
7、CookieValue("name") // 修改的形参
public String login(CookieValue("username")String token);
```

### 25、 拦截器的使用场景有哪些？

```text
1、日志的记录
2、权限的校验
3、登录认证
4、性能测试
```

### 26、 什么是RestFUL的风格

```text
1、概念
    a)restFul风格是一种新的软件架构模式，基于HTTP请求
    b)资源定位
        a)url:资源的地址
    b)资源的操作
        a)method:
            1)GET:查询
            2)POST:修改
            3)PUT：添加
            d)DELETE:删除
    c)SpringMVC中支持的，ES支持的
2、例子
    a)url: http://localhost:8888/emp/12
    b)method:get
```

### 27、 Spring容器和SpirngMVC容器有什么关系

```text
1、spring容器
    a)是一个父容器，spring相关的bean都父容器中管理
    b)父容器不能访问子容器，子容器可以访问父容器
        1)因为一个请求过来后先到Controller中，COntroller中需要访问Service，但是service父容器中管理的
        2)父子容器的扫描的范围，不要把bean重复创建了。
    c)管理的bean有哪些？
        a)server，dao
        b)数据源，事务的控制，第三方的框架的整合，代理
2、springmvc容器
    a)是一个子容器，springmvc相关的bena都在子容器中
    b)管理那些bean？
        a)controller
        b)视图解析器，拦截器，JSON转换器，静态资源忽略
```

### 28、 Spring MVC 中如何在后端代码中实现页面跳转？

```text
1、直接返回视图名称，试图解析器会自动添加前缀和后缀
    a)return "ok"
2、方法返回特殊的字符串
    a)retrun "forward:ok.jsp/getUserPage"
    b)return "redirect:ok.jsp/getUserPage"
```

### 29、 SpirngMVC对异常的处理方式有哪些？

```text
1、注解实现的全局的异常的处理
2、配置全局全局的异常处理
    a)使用xml配置，在xml中配置一个bean
    b)自定义一个类实现对应的接口
3、底层基于AOP思想的实现
```

### 30、 请说明一下@Controller和@RestController的区别是什么？

```text
1、@Controller表示的web层，用这个注解修饰IOC容器会管理这个bean。
2、@RestController:@Controller+@ResponceBody
```

### 31、 autowired 和resource区别是什么？

```text
1、相同点
    a)都可以完成自己注入，都是按照类型注入的
    b)如果存在多个实例，默认的注入的bean的名字变量的名称。
2、 不同点
    a)存在多个beand情况下，指定注入那个bean@Resource通过name属性指定。
    b)存在多个bean的情况下，指定注入那个bean需要通过Qualifier指定
3、匹配到多个bean的情况可以设置@Primary注解来表示这是一个主，优先选择主的bean注入
```

### 32、 请说明一下springmvc和spring-boot区别是什么？

```text
sboot:主要是快速搭建spring应用程序，减少的不必要的配置，里面的约定大于配置的思想。
```

# SpringBoot

### 33、 SpringBoot有几种启动方式，打包方式

```text
1、main方法启动
2、打成jar包，根据jar命令运行jar文件 java -jar xxxx.jar
3、maven插件
4、打成war包运行
    a)忽略自带的tomcat
    b)学一个启动类，extends对应的类，复写里面的方法
        a)tomcat启动的时候就会调用这个方法
```

### 34、 Spring Initializr 是创建 Spring Boot Projects 的唯一方法吗？

```text
1、使用idea创建
2、通过地址:https://start.spring.io/
    a)写项目的信息
    b)添加依赖
    c)下载
```

### 35、 Springboot读取配置文件的方式

```text
1、application.yml:严格按照yml语法，多一层少一层意义完全不一样
2、application.properteis ：接收key-value形式的
2、bootstrap.yml :优先于application.yml加载
```

### 36、Spring boot的如何整合第三方技术(比如ES，MQ）

```text
1、添加依赖
2、配置
3、主启动类开启xxxx
```

### 37、SpringBoot自动配置的原理

```text
SpringBoot自动配置的原理
	a)SpringBootApplication
	b)EnableAutoConfiguration
		a)@Import(AutoConfigurationImportSelector.class)
		b)导入(把AutoConfigurationImportSelector的配置包含进来)
	c)selectImports() -->getAutoConfigurationEntry()-->getCandidateConfigurations()
	d)SpringFactoriesLoader:SPI机制(扫描项目依赖中所有的META-INF/spring.factories)
		a)在spring.factories中配置了很多的bean，这个bean就是SpringBoot需要初始化
	e)依赖
		1)spring-boot-starter ：SpringBoot官方提供
			a)META-INF/spring.factories
		2)mybats-sprinb-boot-starter：第三方提供的
			xb)META-INF/spring.factories
```

# MyBatis

### 38、mbyatis-plus-boot-start-启动的原理

```text
 mbyatis-plus-boot-start-启动的原理
     a)Spring容器你启动
     b)SPI机制扫描jar包的配置文件，会扫描到MyBatisPlusAutoConration
     c)初始化SqlSessionFactory
 请说说MyBatis的工作原理
     a)给Mapper创建一个代理(MapperProxy,MybatisMapperProxy)
     b)MybatisMapperMethod中判断SQL的类型，调用sqlSession中对应的方法
     c)sqlSessionProxy调用对应的方法
     d)MappedStatement:对调用Mapper方法的一个封装
     e)调用Executor开始执行，传递MappedStatement
     f)得到StatementHandler(包含了sql语句)
     g)使用PrepareStatement执行SQL语句
```



### 39、 为什么说Mybatis是半自动ORM映射工具？它与全自动的区别在哪里？

```text
1、什么是ORM？
    a)对象的关系映射
    b)一个对象在数据库中的一个映射关系
2、全自动--- Hibernate
    a)Hibernate是一个全自动的ORM框架，它是重量级框架，对JDBC封装的太多了
    b)session.save(user); -- sql都不用自己写
3、半自动 --MyBatis
    a)SQL是让用户自己的编写的
    b)对SQL没有太多的封装
```

### 40、 MyBatis编程步骤是什么样的？

```text
1、添加依赖
2、创建SQLSessionFactory
    a)需要传入配置文件的流
3、通过SQLSessionFactory获取SQLSession
4、通过SQLSession获取Mapper
5、通过代理调用方法
6、关闭资源
```

### 41、 请说说MyBatis的工作原理

```text
1、核心对象
    a)SQLSessionFactory:负责初始化的操作
        a)Configuration:MyBatisXml配置相关的类
    b)SQLSession:和数据库建立了连接，存在事务，还有拦截器插件
    c)MappedStatement:Dao层每个方法都会对应一个MappedStatement
    d)Executor:负责执行对应的MappedStatement
    e)BoundSql:封装和SQL相关的信息
    f)StatementHandler：负责执行Statement
```

### 42、 JDBC编程有哪些不足之处，MyBatis是如何解决这些问题的？

\~~~ 1、频繁创建，销毁连接对象，MyBatis中通过连接池解决 2、SQL和Java耦合在了一起，MyBatis中通过XML来封装SQL语句 3、结果集的封装需要手动转换，MyBatis自动转换 ~~~

### 43、 为什么需要预编译

```text
1、安全
    a)避免程出现SQL注入的问题
2、速度
    a)编译一次，可以执行多次的
```

### 45、 Mybatis是否支持延迟加载？

```text
1、支持延迟加载
2、查询一个员工，员工关联部门
    a)查询员工姓名的时候只查询员工表
    b)都用户有用到部门的时候才会发送sql语句查询部门表
3、底层怎么实现？
    a)动态代理
```

### 46、 #{}和${}的区别

```text
1、#
    a)#号最终被解析为占位符了
    b)获取到方法的形参
    c)不会出现SQL注入的问题
    d)#号一般用在条件查询
2、$
    a)可以获取到方法的形参的
    b)直接拼接到sql语句中，所以会出现SQL注入的问题
    d)$符号一般用在动态表的查询
```

### 47、 MyBatis中模糊查询like语句该怎么写

```text
select * from t_user where like concat("%","#{xxxx}","%")
```

### 48、 在mapper中如何传递多个参数

```text
1、方法直接传递对象--》通过属性名称获取
2、可以通过索引获取
    a)#{param1},#{param2}
    b)#{arg0},
3、方法传递Map---》通过key获取
4、通过注解设置别名--》通过别名获取
```

### 49、 Mybatis如何执行批量操作

```text
<foreach>
    a)open：开始调用，调用一次
    b)close:接收调用，调用一次
    d)item:当前遍历的对象
    e)collection:需要遍历的集合
    f)index:集合索引
    g)sxxxx:每次循环都要用调用
```

### 50、 如何获取生成的主键

```text
1、设置主键自动回填
    a)开启主键回填
    b)设置回填的到那个属性
2、使用<selectKey>来完成
    a)之后
        a)调用last_insert_Id()获取最新的主键
        b)在回填的对象的id属性中
    b)之前
        a)先调用sequence获取id
        b)在设置到对象的id属性
        c)在插入表
```

### 51、 当实体类中的属性名和表中的字段名不一样 ，怎么办

```text
1、设置as别名 user_name as usernmae
2、里面ResultMap建议映射关系
```

### 52、 什么是MyBatis的接口绑定？有哪些实现方式？

```text
1、什么是接口绑定
    指定的就是自定义的Mapper接口和Sql绑定的关系
2、如何实现的
    MyBatis最终会使用JDK代理得分方式给Mapper接口创建一个代理，在这个代理中对接口中所有的方法进行拦截，拦截到后把所有的处理交给MapperStaement，由这个对象负责执行sql语句。这样实现方式会比直接调用SQLSession中的方法更加方便。
3、有哪些实现方式
    a)接口中的方法和注解中的sql语句绑定
    b)接口中的方法和xml文件的sql绑定
```

### 53、 使用MyBatis的mapper接口调用时有哪些要求？

```text
1、namespace实现要和接口的全类名一直
2、节点的id要和方法的名称一致
3、方法的形参要和标签中的parameterType一直
4、方法的返回类型要和resultType一直
```

### 54、 Xml映射文件都会写一个Dao接口与之对应，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗

```text
1、实现原理
    a)使用jdk动态代理
2、在MyBatis的接口中方法不允许重载，要求节点id是唯一的。
```

### 55、 Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

```text
1、如果是一个namespace中id不允许重复
2、如果不同的namespaceid是允许重复的
```

### 56、 Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？

```text
1、别名
2、resultMap
```

### 57、 Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？

```text
1、<sql>,<if><while><term>.....
```

### 58、 Mybatis映射文件中，如果A标签通过include引用了B标签的内容，请问，B标签能否定义在A标签的后面，还是说必须定义在A标签的前面？

```text
1、可以的
2、xml解析的过来
    a)xml还是做头开始解析
    b)如果解析到了a标签，但是a标签中引用了b标签，这时会把a标签置为未解析的状态
    c)在往下去解析其他的标签，直到所有的标签都解析完毕
    d)再去解析状态是未解析的标签
```

### 59、 Mybatis动态sql是做什么的？都有哪些动态sql？能简述一下动态sql的执行原理不？

```text
1、动态SQL
    a)${sql}
    b)标签
        a)<if>
        b)<term>
        c)<foreach>
2、执行原理
    a)使用OGNL表达式来完成，OGNL底层就是一个Map
    b)通过OGNL表达式来获取参数，然后在根据参数赋值sql中
```

### 60、 Mybatis分页插件的原理是什么？

```text
实现了MyBatis体用的插件接口，这个接口拦截器，在调用sql之前对方法进行拦截，获取用户调用的sql语句，通过拼接的方式组成查询全部的sql语句，然后执行countsql，再执行分页的sql，把数据都封装到一个page对象中。
```

### 61、 Mybatis的一级、二级缓存

```text
1、一级缓存
    a)SqlSession级别的
    b)默认是开启的
2、二级缓存
    a)二级缓存SQLSessionFactory(namesapce)
    b)默认是关闭的
    c)放在二级中的对象要实现对象序列化接口
    d)二级缓存可以使用第三方的
3、MyBatis的一级缓存和二级缓存都是用PerpetualCache来实现的
4、MyBatis执行更新操作后(cud)，缓存都会被刷新。
```

# Spring Cloud

### 62、 服务注册和发现是什么意思？Spring Cloud 如何实现？

```text
1、注册：把所有的服务或者配置文件都写到统一的地方来管理。
2、发现:如果要使用服务或者配置文件到一个地方直接获取。
3、SpringCloud使用Eureka实现
```

### 63、 SpringCloud有哪组件，都解决了什么问题

```text
1、注册中心：Eureka
2、服务调用:openfeign
3、路由网关：zuul/getway
4、服务降级:Hystrix
5、配置文件:cofig-server
6、服务链路监控: 
7、调用第三方：sideacr
8、stream:对MQ封装
```