## 什么是 BeanDefinition？

 BeanDefinition 表示 Bean 定义，Spring 根据 BeanDefinition 来创建 Bean 对象，BeanDefinition 有很多的属性用来描述 Bean，BeanDefinition 是 Spring 中非常核心的概念。

### beanClass

表示一个 bean 的类型，比如：UserService.class、OrderService.class，Spring 在创建 Bean 的过程中会根据此属性来实例化得到对象。

### scope

表示一个 bean 的作用域，比如：scope 等于 singleton，该 bean 就是一个单例 Bean；scope 等于 prototype，该 bean 就是一个原型 Bean。

### isLazy

表示一个 bean 是不是需要懒加载，原型 bean 的 isLazy 属性不起作用，懒加载的单例 bean，会在第一次 getBean 的时候生成该 bean，非懒加载的单例 bean，则会在 Spring 启动过程中直接生成好。

### dependsOn

表示一个 bean 在创建之前所依赖的其他 bean，在一个 bean 创建之前，它所依赖的这些 bean 得先全部创建好。

### primary

表示一个 bean 是主 bean，在 Spring 中一个类型可以有多个 bean 对象，在进行依赖注入时，如果根据类型找到了多个 bean，此时会判断这些 bean 中是否存在一个主 bean，如果存在，则直接将这个 bean 注入给属性。

### initMethodName

表示一个 bean 的初始化方法，一个 bean 的生命周期过程中有一个步骤叫初始化，Spring 会在这个步骤中去调用 bean 的初始化方法，初始化逻辑由程序员自己控制，表示程序员可以自定义逻辑对 bean 进行加工。

**@Component、@Bean 和 `<bean/>` 这些都会解析为 BeanDefinition。**

## 什么是 BeanFactory？

BeanFactory 是一种"Spring 容器"，BeanFactory 翻译过来就是 Bean 工厂，顾名思义，它可以用来创建 Bean、获取 Bean，BeanFactory 是 Spring 中非常核心的组件。

BeanFactory 将利用 BeanDefinition 来生成 Bean 对象，BeanDefinition 相当于 BeanFactory 的原材料，Bean 对象就相当于 BeanFactory 所生产出来的产品。

BeanFactory 的核心子接口和实现类：

-   ListableBeanFactory

-   ConfigurableBeanFactory

-   AutowireCapableBeanFactory

-   AbstractBeanFactory

-   DefaultListableBeanFactory

DefaultListableBeanFactory 支持单例 Bean、支持 Bean 别名、支持父子 BeanFactory、支持 Bean 类型转化、支持 Bean 后置处理、支持 FactoryBean、支持自动装配等。

## 什么是 Bean 生命周期？

Bean 生命周期描述的是 Spring 中一个 Bean 创建过程和销毁过程中所经历的步骤，其中 Bean 创建过程是重点。程序员可以利用 Bean 生命周期机制对 Bean 进行自定义加工。

### 核心步骤：

1.  BeanDefinition：Bean 定义

    BeanDefinition 表示 Bean 定义，它定义了某个 Bean 的类型，Spring 就是利用 BeanDefinition 来创建 Bean 的，比如需要利用 BeanDefinition 中 beanClass 属性确定 Bean 的类型，从而实例化出来对象。

2.  构造方法推断：选出一个构造方法

    一个 Bean 中可以有多个构造方法，此时就需要 Spring 来判断到底使用哪个构造方法，这个过程是比较复杂的。通过构造方法推断之后确定一个构造方法后，就可以利用构造方法实例化得到一个对象了。

3.  实例化：构造方法反射得到对象

    通过构造方法反射得到一个实例化对象，在 Spring 中，可以通过 BeanPostProcessor 机制对实例化进行干预。

4.  属性填充：给属性进行自动填充

    实例化所得到的对象，是"不完整"的对象，"不完整"的意思是该对象中的某些属性还没有进行属性填充，也就是 Spring 还没有自动给某些属性赋值，属性填充就是我们通常说的自动注入、依赖注入。

5.  初始化：对其他属性赋值、校验

    在一个对象的属性填充后，Spring 提供了初始化机制，程序员可以利用初始化机制对 Bean 进行自定义加工，比如可以利用 initializingBean 接口来对 Bean 中的其他属性进行赋值，或对 Bean 中的某些属性进行校验。

6.  初始化后：AOP、生成代理对象

    初始化后是 Bean 创建生命周期中最后一个步骤，我们常说 AOP 机制，就是在这个步骤中通过 BeanPostProcessor 机制实现的，初始化之后得到的对象才是真正的 Bean 对象。

## @Autowired 是如何工作的？

@Autowired 表示某个属性是否需要进行依赖注入，可以写在属性和方法上。注解中的 required 属性默认为 ture，表示如果没有对象可以注入给属性则拋异常。

```java
@Service
public class OrderService {
    @Autowired
    private UserService userService;
}
```

@Autowired 加在某个属性上，Spring 在进行 Bean 的生命周期过程中，在属性填充这一步,会基于实例化出来的对象，对该对象中加了 @Autowired 的属性自动给属性赋值。Spring 会先根据属性的类型去 Spring 容器中找出该类型所有的 Bean 对象，如果找出来多个则再根据属性的名字从多个中再确定一个。如果 required 属性为 true，并且根据属性信息找不到对象，则直接抛异常。

```java
@Service
public class OrderService {
    private UserService userServcie;

    @Autowired
    public void setUserService(UserService userService) {
      this.userService = userService;
    }
}
```

当 @Autowired 注解写在某个方法上时，Spring 在 Bean 生命周期的属性填充阶段，会根据方法的参数类型、参数名字从 Spring 容器找到对象当做方法入参自动反射调用该方法。

```java
@Service
public class OrderService {
    private UserService userServcie;

    @Autowired
    public void setUserService(UserService userService) {
      this.userService = userService;
    }

    public OrderService(UserService userService, UserService userService1) {
      this.userService = userService;
    }
}
```

@Autowired 加在构造方法.上时，Spring 会在推断构造方法阶段，选择该构造方法来进行实例化，在反射调用构造方法之前，会先根据构造方法参数类型、参数名从 Spring 容器中找到 Bean 对象，当做构造方法入参。

## @Resource 是如何工作的？

@Resource 注解与 @Autowired 类似，也是用来进行依赖注入的，@Resource 是 Java 层面所提供的注解，@Autowired 是 Spring 所提供的注解，它们依赖注入的底层实现逻辑也不同。

@Resource 注解中有一个 name 属性，针对 name 属性是否有值，@Resource 的依赖注入底层流程是不同的。

@Reousrce 如果 name 属性有值，那么 Spring 会直接根据所指定的 name 值去 Spring 容器找 Bean 对象，如果找到了则成功，如果没有找到，则报错。

如果 @Resource 中的 name 属性没有值，则：

1.  先判断该属性名字在 Spring 容器中是否存在 Bean 对象。
2.  如果存在，则成功找到 Bean 对象进行注入。
3.  如果不存在，则根据属性类型去 Spring 容器找 Bean 对象，找到一个则进行注入。

## @Value 是如何工作的？

@Value 注解和 @Resource、@Autowired 类似也是用来对属性进行依赖注入的，只不过 @Value 是用来从 Properties 文件中来获取值的，并且 @Value 可以解析SpEL（Spring 表达式）。

```java 
@Value("zhouyu")
```

直接将字符串"zhouyu"赋值给属性，如果属性类型不是 String，或无法进行类型转换，则报错。

```java
@Value("${zhouyu}")
```

将会把`${}`中的字符串当做 key，从 Properties 文件中找出对应的 value 赋值给属性，如果没找到，则会把​`${zhouyu}`当做普通字符串注入给属性。

```java
@Value("#{zhouyu}")
```

会将`#{}`中的字符串当做 Spring 表达式进行解析，Spring 会把"zhouyu"当做 beanName，并从 Spring 容器中找对应 bean，如果找到则进行属性注入，没找到则报错。

## 什么是 FactoryBean？

FactoryBean 是 Spring 所提供的一种较灵活的创建 Bean 的方式，可以通过实现 FactoryBean 接口中的 getObject() 方法来返回一个对象，这个对象就是最终的 Bean 对象。

### FactoryBean 接口中的方法

-   Object getObject()：返回的是 Bean 对象
-   boolean isSingleton()：返回的是否是单例 Bean 对象
-   Class getObjectType()：返回的是 Bean 对象的类型

```java
@Component("zhouyu")
public class ZhouyuFactoryBean implements FactoryBean {
    //Bean 对象
    @Override
    public Object getObject() throws Exception {
        return new User();
    }
    
    //Bean 对象的类型
    @Override
    public Class<?> getObjectType() {
        return User.class;
    }
    
    //所定义的 Bean 是单例还是原型
    @Override
    public boolean isSingleton() {
        return true;
    }
}
```

### FactoryBean 的特殊点

上述代码，实际上对应了两个 Bean 对象：

1.  beanName 为"zhouyu"，bean 对象为 getObject 方法所返回的 User 对象。
2.  beanName 为"&zhouyu" ，bean 对象为 ZhouyuFactoryBean 类的实例对象。

FactoryBean 对象本身也是一个 Bean，同时它相当于一个小型工厂，可以生产出另外的 Bean。

BeanFactory 是一个 Spring 容器，是一个大型工厂，它可以生产出各种各样的 Bean。

FactoryBean 机制被广泛的应用在 Spring 内部和 Spring 与第三方框架或组件的整合过程中。

## 什么是 ApplicationContext？

ApplicationContext 是比 BeanFactory 更加强大的 Spring 容器，它既可以创建 bean、获取 bean，还支持国际化、事件广播、获取资源等 BeanFactory 不具备的功能。

### ApplicationContext 所继承的接口

-   EnvironmentCapable

    ApplicationContext 继承了这个接口，表示拥有了获取环境变量的功能，可以通过 ApplicationContext 获取操作系统环境变量和 JVM 环境变量。

-   ListableBeanFactory

    ApplicationContext 继承了这个接口，就拥有了获取所有 beanNames、判断某个 beanName 是否存在 beanDefinition 对象、统计 BeanDefinition 个数、获取某个类型对应的所有 beanNames 等功能。

-   HierarchicalBeanFactory

    ApplicationContext 继承了这个接口，就拥有了获取父 BeanFactory、判断某个 name 是否存在 bean 对象的功能。

-   MessageSource

    ApplicationContext 继承了这个接口，就拥有了国际化功能，比如可以直接利用 MessageSource 对象获取某个国际化资源（比如不同国家语言所对应的字符）。

-   ApplicationEventPublisher

    ApplicationContext 继承了这个接口，就拥有了事件发布功能，可以发布事件，这是 ApplicationContext 相对于 BeanFactory 比较突出、常用的功能。

-   ResourcePatternResolver

    ApplicationContext 继承了这个接口，就拥有了加载并获取资源的功能，这里的资源可以是文件，图片等某个 URL 资源都可以。

## 什么是 BeanPostProcessor？

BeanPostProcessor 是 Spring 所提供的一种扩展机制，可以利用该机制对 Bean 进行定制化加工，在 Spring 底层源码实现中，也广泛的用到了该机制， BeanPostProcessor 通常也叫做 Bean 后置处理器。

BeanPostProcessor 在 Spring 中是一个接口，我们定义一个后置处理器，就是提供一个类实现该接口，在 Spring 中还存在一些接口继承了 BeanPostProcessor，这些子接口是在 BeanPostProcessor 的基础上增加了一些其他的功能。

### BeanPostProcessor 中的方法

-   postProcessBeforelnitialization()：初始化前方法，表示可以利用这个方法来对 Bean 在初始化前进行自定义加工。
-   postProcessAfterlnitialization()：初始化后方法，表示可以利用这个方法来对 Bean 在初始化后进行自定义加工。

### InstantiationAwareBeanPostProcessor

BeanPostProcessor 的一个子接口。

-   postProcessBeforelnstantiation()：实例化前
-   postProcessAfterlnstantiation()：实例化后
-   postProcessProperties()：属性注入后

## AOP 是如何工作的？

AOP 就是面向切面编程，是一种非常适合在无需修改业务代码的前提下，对某个或某些业务增加统一的功能，比如日志记录、权限控制、事务管理等，能很好的使得代码解耦，提高开发效率。

### AOP 中的核心概念

-   Advice

    Advice 可以理解为通知、建议，在 Spring 中通过定义 Advice 来定义代理逻辑。

-   Pointcut

    Pointcut 是切点，表示 Advice 对应的代理逻辑应用在哪个类、哪个方法上。

-   Advisor

    Advisor 等于 Advice + Pointcut，示代理逻辑和切点的一个整体，程序员可以通过定义或封装个 Advisor，来定义切点和代理逻辑。

-   Weaving

    Weaving 表示织入，将 Advice 代理逻辑在源代码级别嵌入到切点的过程，就叫做织入。

-   Target

    Target 表示目标对象，也就是被代理对象，在 AOP 生成的代理对象中会持有目标对象。

-   Join Point

    Join Point 表示连接点，在 Spring AOP 中，就是方法的执行点。

### AOP 的工作原理

AOP 是发生在 Bean 的生命周期过程中的：

1.  Spring 生成 bean 对象时，先实例化出来一个对象，也就是 target 对象
2.  再对 target 对象进行属性填充
3.  在初始化后步骤中，会判断 target 对象有没有对应的切面
4.  如果有切面，就表示当前 target 对象需要进行 AOP
5.  通过 Cglib 或 JDK 动态代理机制生成一个代理对象，作为最终的 bean 对象
6.  代理对象中有一个 target 属性指向了 target 对象

## 你知道哪几种定义 Bean 的方式？