<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [基本](#%E5%9F%BA%E6%9C%AC)
  - [ClassPathXmlApplicationContext](#classpathxmlapplicationcontext)
    - [构造器](#%E6%9E%84%E9%80%A0%E5%99%A8)
    - [设置配置文件路径](#%E8%AE%BE%E7%BD%AE%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)
      - [Environment 接口](#environment%E6%8E%A5%E5%8F%A3)
        - [Profile](#profile)
        - [Property](#property)
      - [Environment 构造器](#environment%E6%9E%84%E9%80%A0%E5%99%A8)
        - [PropertySources 接口](#propertysources%E6%8E%A5%E5%8F%A3)
        - [PropertySource 接口](#propertysource%E6%8E%A5%E5%8F%A3)
      - [路径 Placeholder 处理](#%E8%B7%AF%E5%BE%84placeholder%E5%A4%84%E7%90%86)
        - [PropertyResolver 接口](#propertyresolver%E6%8E%A5%E5%8F%A3)
        - [解析](#%E8%A7%A3%E6%9E%90)
  - [refresh](#refresh)
    - [prepareRefresh](#preparerefresh)
      - [属性校验](#%E5%B1%9E%E6%80%A7%E6%A0%A1%E9%AA%8C)
    - [BeanFactory 创建](#beanfactory%E5%88%9B%E5%BB%BA)
      - [BeanFactory 接口](#beanfactory%E6%8E%A5%E5%8F%A3)
      - [BeanFactory 定制](#beanfactory%E5%AE%9A%E5%88%B6)
      - [Bean 加载](#bean%E5%8A%A0%E8%BD%BD)
        - [EntityResolver](#entityresolver)
        - [BeanDefinitionReader](#beandefinitionreader)
        - [路径解析（Ant）](#%E8%B7%AF%E5%BE%84%E8%A7%A3%E6%9E%90ant)
        - [配置文件加载](#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8A%A0%E8%BD%BD)
        - [Bean 解析](#bean%E8%A7%A3%E6%9E%90)
      - [默认命名空间解析](#%E9%BB%98%E8%AE%A4%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%E8%A7%A3%E6%9E%90)
        - [import](#import)
        - [alias](#alias)
        - [bean](#bean)
          - [id & name 处理](#id--name%E5%A4%84%E7%90%86)
          - [beanName 生成](#beanname%E7%94%9F%E6%88%90)
          - [bean 解析](#bean%E8%A7%A3%E6%9E%90)
          - [Bean 装饰](#bean%E8%A3%85%E9%A5%B0)
          - [Bean 注册](#bean%E6%B3%A8%E5%86%8C)
          - [BeanDefiniton 数据结构](#beandefiniton%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)
        - [beans](#beans)
      - [其它命名空间解析](#%E5%85%B6%E5%AE%83%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%E8%A7%A3%E6%9E%90)
        - [NamespaceHandler 继承体系](#namespacehandler%E7%BB%A7%E6%89%BF%E4%BD%93%E7%B3%BB)
        - [init](#init)
        - [BeanFactory 数据结构](#beanfactory%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)
    - [prepareBeanFactory](#preparebeanfactory)
      - [BeanExpressionResolver](#beanexpressionresolver)
      - [PropertyEditorRegistrar](#propertyeditorregistrar)
      - [环境注入](#%E7%8E%AF%E5%A2%83%E6%B3%A8%E5%85%A5)
      - [依赖解析忽略](#%E4%BE%9D%E8%B5%96%E8%A7%A3%E6%9E%90%E5%BF%BD%E7%95%A5)
      - [bean 伪装](#bean%E4%BC%AA%E8%A3%85)
      - [LoadTimeWeaver](#loadtimeweaver)
      - [注册环境](#%E6%B3%A8%E5%86%8C%E7%8E%AF%E5%A2%83)
    - [postProcessBeanFactory](#postprocessbeanfactory)
    - [invokeBeanFactoryPostProcessors](#invokebeanfactorypostprocessors)
    - [BeanPostProcessor 注册](#beanpostprocessor%E6%B3%A8%E5%86%8C)
    - [MessageSource](#messagesource)
    - [事件驱动](#%E4%BA%8B%E4%BB%B6%E9%A9%B1%E5%8A%A8)
      - [事件](#%E4%BA%8B%E4%BB%B6)
      - [发布者](#%E5%8F%91%E5%B8%83%E8%80%85)
        - [ApplicationEventPublisher](#applicationeventpublisher)
        - [ApplicationEventMulticaster](#applicationeventmulticaster)
      - [监听器](#%E7%9B%91%E5%90%AC%E5%99%A8)
      - [初始化](#%E5%88%9D%E5%A7%8B%E5%8C%96)
      - [事件发布](#%E4%BA%8B%E4%BB%B6%E5%8F%91%E5%B8%83)
        - [监听器获取](#%E7%9B%91%E5%90%AC%E5%99%A8%E8%8E%B7%E5%8F%96)
        - [同步/异步](#%E5%90%8C%E6%AD%A5%E5%BC%82%E6%AD%A5)
          - [全局](#%E5%85%A8%E5%B1%80)
          - [注解](#%E6%B3%A8%E8%A7%A3)
    - [onRefresh](#onrefresh)
    - [ApplicationListener 注册](#applicationlistener%E6%B3%A8%E5%86%8C)
    - [singleton 初始化](#singleton%E5%88%9D%E5%A7%8B%E5%8C%96)
      - [ConversionService](#conversionservice)
      - [StringValueResolver](#stringvalueresolver)
      - [LoadTimeWeaverAware](#loadtimeweaveraware)
      - [初始化](#%E5%88%9D%E5%A7%8B%E5%8C%96-1)
- [getBean](#getbean)
  - [beanName 转化](#beanname%E8%BD%AC%E5%8C%96)
  - [手动注册 bean 检测](#%E6%89%8B%E5%8A%A8%E6%B3%A8%E5%86%8Cbean%E6%A3%80%E6%B5%8B)
  - [检查父容器](#%E6%A3%80%E6%9F%A5%E7%88%B6%E5%AE%B9%E5%99%A8)
  - [依赖初始化](#%E4%BE%9D%E8%B5%96%E5%88%9D%E5%A7%8B%E5%8C%96)
  - [Singleton 初始化](#singleton%E5%88%9D%E5%A7%8B%E5%8C%96)
    - [getSingleton 方法](#getsingleton%E6%96%B9%E6%B3%95)
      - [是否存在](#%E6%98%AF%E5%90%A6%E5%AD%98%E5%9C%A8)
      - [bean 创建](#bean%E5%88%9B%E5%BB%BA)
        - [lookup-method 检测](#lookup-method%E6%A3%80%E6%B5%8B)
        - [InstantiationAwareBeanPostProcessor 触发](#instantiationawarebeanpostprocessor%E8%A7%A6%E5%8F%91)
        - [doCreateBean](#docreatebean)
          - [创建（createBeanInstance）](#%E5%88%9B%E5%BB%BAcreatebeaninstance)
          - [MergedBeanDefinitionPostProcessor](#mergedbeandefinitionpostprocessor)
          - [属性解析](#%E5%B1%9E%E6%80%A7%E8%A7%A3%E6%9E%90)
          - [属性设置](#%E5%B1%9E%E6%80%A7%E8%AE%BE%E7%BD%AE)
          - [初始化](#%E5%88%9D%E5%A7%8B%E5%8C%96-2)
    - [getObjectForBeanInstance](#getobjectforbeaninstance)
  - [Prototype 初始化](#prototype%E5%88%9D%E5%A7%8B%E5%8C%96)
    - [beforePrototypeCreation](#beforeprototypecreation)
    - [createBean](#createbean)
    - [afterPrototypeCreation](#afterprototypecreation)
    - [总结](#%E6%80%BB%E7%BB%93)
  - [其它 Scope 初始化](#%E5%85%B6%E5%AE%83scope%E5%88%9D%E5%A7%8B%E5%8C%96)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 基本

本部分从最基本的 Spring 开始，配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>    
<beans>    
    <bean class="base.SimpleBean"></bean>
</beans>
```

启动代码：

```java
public static void main(String[] args) {
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("config.xml");
    SimpleBean bean = context.getBean(SimpleBean.class);
    bean.send();
    context.close();
}
```

SimpleBean：

```java
public class SimpleBean {
    public void send() {
        System.out.println("I am send method from SimpleBean!");
    }
}
```

## ClassPathXmlApplicationContext

整个继承体系如下：

<img src="https://gitee.com/xlshi/blog_img/raw/master/mac/20210517230141.jpg" alt="ResourceLoader继承体系"  />

ResourceLoader 代表了**加载资源的一种方式，正是策略模式的实现**。

构造器源码：

```java
public ClassPathXmlApplicationContext(String[] configLocations, boolean refresh, ApplicationContext parent) {
    //null
    super(parent);
    setConfigLocations(configLocations);
    //默认true
    if (refresh) {
        refresh();
    }
}
```

### 构造器

首先看父类构造器，沿着继承体系一直向上调用，直到 AbstractApplicationContext：

```java
public AbstractApplicationContext(ApplicationContext parent) {
    this();
    setParent(parent);
}

public AbstractApplicationContext() {
    this.resourcePatternResolver = getResourcePatternResolver();
}
```

getResourcePatternResolver：

```java
protected ResourcePatternResolver getResourcePatternResolver() {
    return new PathMatchingResourcePatternResolver(this);
}
```

PathMatchingResourcePatternResolver 支持 Ant 风格的路径解析。

### 设置配置文件路径

即 AbstractRefreshableConfigApplicationContext.setConfigLocations：

```java
public void setConfigLocations(String... locations) {
    if (locations != null) {
        Assert.noNullElements(locations, "Config locations must not be null");
        this.configLocations = new String[locations.length];
        for (int i = 0; i < locations.length; i++) {
            this.configLocations[i] = resolvePath(locations[i]).trim();
        }
    } else {
        this.configLocations = null;
    }
}
```

resolvePath：

```java
protected String resolvePath(String path) {
    return getEnvironment().resolveRequiredPlaceholders(path);
}
```

此方法的目的在于将占位符（placeholder）解析成实际的地址。比如可以这么写：new ClassPathXmlApplicationContext("classpath:config.xml")；那么 classpath: 就是需要被解析的。

getEnvironment 方法来自于 ConfigurableApplicationContext 接口，源码很简单，如果为空就调用 createEnvironment 创建一个。AbstractApplicationContext.createEnvironment：

```java
protected ConfigurableEnvironment createEnvironment() {
    return new StandardEnvironment();
}
```

#### Environment 接口

继承体系：

![Environment继承体系](https://gitee.com/xlshi/blog_img/raw/master/mac/20210517231900.jpg)

Environmen 接口**代表了当前应用所处的环境。**从此接口的方法可以看出，其主要和 profile、Property 相关。

##### Profile

Spring Profile 特性是从 3.1 开始的，其主要是为了解决这样一种问题：线上环境和测试环境使用不同的配置或是数据库或是其它。有了 Profile 便可以在不同环境之间无缝切换。 **Spring 容器管理的所有 bean 都是和一个 profile 绑定在一起的。 **使用了 Profile 的配置文件示例： 

```xml
<beans profile="develop">  
    <context:property-placeholder location="classpath*:jdbc-develop.properties"/>  
</beans>  
<beans profile="production">  
    <context:property-placeholder location="classpath*:jdbc-production.properties"/>  
</beans>  
<beans profile="test">  
    <context:property-placeholder location="classpath*:jdbc-test.properties"/>  
</beans>
```

在启动代码中可以用如下代码设置活跃（当前使用的）Profile：

```java
context.getEnvironment().setActiveProfiles("dev");
```

当然使用的方式还有很多（比如注解），参考：

[Spring 3.1 profile 配置不同的环境](http://radiumxie.iteye.com/blog/1851919)

[Spring Profiles example](http://www.mkyong.com/spring/spring-profiles-example/)

##### Property

这里的 Property 指的是程序运行时的一些参数，引用注释：

> properties files，JVM system properties，system environment variables，JNDI，servlet context parameters，ad-hoc Properties objects，Maps，and so on.

#### Environment 构造器

```java
private final MutablePropertySources propertySources = new MutablePropertySources(this.logger);
public AbstractEnvironment() {
    customizePropertySources(this.propertySources);
}
```

#####  PropertySources 接口

继承体系：

![PropertySources继承体系](https://gitee.com/xlshi/blog_img/raw/master/mac/20210517232127.jpg)

此接口实际上是 PropertySource 的容器，默认的 MutablePropertySources 实现内部含有一个 CopyOnWriteArrayList 作为存储载体。

StandardEnvironment.customizePropertySources：

```java
/** System environment property source name: {@value} */
public static final String SYSTEM_ENVIRONMENT_PROPERTY_SOURCE_NAME = "systemEnvironment";
/** JVM system properties property source name: {@value} */
public static final String SYSTEM_PROPERTIES_PROPERTY_SOURCE_NAME = "systemProperties";
@Override
protected void customizePropertySources(MutablePropertySources propertySources) {
    propertySources.addLast(new MapPropertySource
        (SYSTEM_PROPERTIES_PROPERTY_SOURCE_NAME, getSystemProperties()));
    propertySources.addLast(new SystemEnvironmentPropertySource
        (SYSTEM_ENVIRONMENT_PROPERTY_SOURCE_NAME, getSystemEnvironment()));
}
```

##### PropertySource 接口

PropertySource 接口代表了键值对的 Property 来源，继承体系：

![PropertySource继承体系](images/PropertySource.jpg)

AbstractEnvironment.getSystemProperties：

```java
@Override
public Map<String, Object> getSystemProperties() {
    try {
        //获取全部系统属性
        return (Map) System.getProperties();
    }
    catch (AccessControlException ex) {
        return (Map) new ReadOnlySystemAttributesMap() {
            @Override
            protected String getSystemAttribute(String attributeName) {
                try {
                    //如果组织获取全部的系统属性，尝试获取单个属性，如果还不行就会抛异常
                    return System.getProperty(attributeName);
                }
                catch (AccessControlException ex) {
                    if (logger.isInfoEnabled()) {
                        logger.info(format("Caught AccessControlException when accessing system " +
                                "property [%s]; its value will be returned [null]. Reason: %s",
                                attributeName, ex.getMessage()));
                    }
                    return null;
                }
            }
        };
    }
}
```

这里的实现很有意思，如果安全管理器阻止获取全部的系统属性，那么会尝试获取单个属性的可能性，如果还不行就抛异常了。

getSystemEnvironment 方法也是一个套路，不过最终调用的是 System.getenv，可以获取 JVM 和 OS 的一些版本信息。

#### 路径 Placeholder 处理

AbstractEnvironment.resolveRequiredPlaceholders：

```java
@Override
public String resolveRequiredPlaceholders(String text) throws IllegalArgumentException {
    //text 即配置文件路径，比如 classpath:config.xml
    return this.propertyResolver.resolveRequiredPlaceholders(text);
}
```

propertyResolver 是一个 PropertySourcesPropertyResolver 对象：

```java
private final ConfigurablePropertyResolver propertyResolver =
            new PropertySourcesPropertyResolver(this.propertySources);
```

##### PropertyResolver 接口

PropertyResolver 继承体系（排除 Environment 分支）：

![PropertyResolver继承体系](images/PropertyResolver.jpg)

此接口正是用来解析 PropertyResource。

##### 解析

AbstractPropertyResolver.resolveRequiredPlaceholders：

```java
@Override
public String resolveRequiredPlaceholders(String text) throws IllegalArgumentException {
    if (this.strictHelper == null) {
        this.strictHelper = createPlaceholderHelper(false);
    }
    return doResolvePlaceholders(text, this.strictHelper);
}
```

```java
private PropertyPlaceholderHelper createPlaceholderHelper(boolean ignoreUnresolvablePlaceholders) {
    //三个参数分别是 '${'、'}'、':'
    return new PropertyPlaceholderHelper(this.placeholderPrefix, this.placeholderSuffix,
        this.valueSeparator, ignoreUnresolvablePlaceholders);
}
```

doResolvePlaceholders：

```java
private String doResolvePlaceholders(String text, PropertyPlaceholderHelper helper) {
    //PlaceholderResolver 接口依然是策略模式的体现
    return helper.replacePlaceholders(text, new PropertyPlaceholderHelper.PlaceholderResolver() {
        @Override
        public String resolvePlaceholder(String placeholderName) {
            return getPropertyAsRawString(placeholderName);
        }
    });
}
```

其实代码执行到这里的时候还没有进行 xml 配置文件的解析，那么这里的解析 placeHolder 是什么意思呢，原因在于可以这么写：

```java
System.setProperty("spring", "classpath");
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("${spring}:config.xml");
SimpleBean bean = context.getBean(SimpleBean.class);
```

这样就可以正确解析。placeholder 的替换其实就是字符串操作，这里只说一下正确的属性是怎么来的。实现的关键在于PropertySourcesPropertyResolver.getProperty：

```java
@Override
protected String getPropertyAsRawString(String key) {
    return getProperty(key, String.class, false);
}
protected <T> T getProperty(String key, Class<T> targetValueType, boolean resolveNestedPlaceholders) {
    if (this.propertySources != null) {
        for (PropertySource<?> propertySource : this.propertySources) {
            Object value = propertySource.getProperty(key);
            return value;
        }
    }
    return null;
}
```

很明显了，就是从 System.getProperty 和 System.getEnv 获取，但是由于环境变量是无法自定义的，所以其实此处只能通过 System.setProperty 指定。

注意，classpath:XXX 这种写法的 classpath 前缀到目前为止还没有被处理。

## refresh

Spring bean 解析就在此方法，所以单独提出来。

AbstractApplicationContext.refresh:

```java
@Override
public void refresh() throws BeansException, IllegalStateException {
    synchronized (this.startupShutdownMonitor) {
        // Prepare this context for refreshing.
        prepareRefresh();
        // Tell the subclass to refresh the internal bean factory.
        ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();
        // Prepare the bean factory for use in this context.
        prepareBeanFactory(beanFactory);
        try {
            // Allows post-processing of the bean factory in context subclasses.
            postProcessBeanFactory(beanFactory);
            // Invoke factory processors registered as beans in the context.
            invokeBeanFactoryPostProcessors(beanFactory);
            // Register bean processors that intercept bean creation.
            registerBeanPostProcessors(beanFactory);
            // Initialize message source for this context.
            initMessageSource();
            // Initialize event multicaster for this context.
            initApplicationEventMulticaster();
            // Initialize other special beans in specific context subclasses.
            onRefresh();
            // Check for listener beans and register them.
            registerListeners();
            // Instantiate all remaining (non-lazy-init) singletons.
            finishBeanFactoryInitialization(beanFactory);
            // Last step: publish corresponding event.
            finishRefresh();
        } catch (BeansException ex) {
            // Destroy already created singletons to avoid dangling resources.
            destroyBeans();
            // Reset 'active' flag.
            cancelRefresh(ex);
            // Propagate exception to caller.
            throw ex;
        } finally {
            // Reset common introspection caches in Spring's core, since we
            // might not ever need metadata for singleton beans anymore...
            resetCommonCaches();
        }
    }
}
```

### prepareRefresh

```java
protected void prepareRefresh() {
    this.startupDate = System.currentTimeMillis();
    this.closed.set(false);
    this.active.set(true);
    // Initialize any placeholder property sources in the context environment
    //空实现，用于扩展插件
    initPropertySources();
    // Validate that all properties marked as required are resolvable
    // see ConfigurablePropertyResolver#setRequiredProperties
    getEnvironment().validateRequiredProperties();
    // Allow for the collection of early ApplicationEvents,
    // to be published once the multicaster is available...
    this.earlyApplicationEvents = new LinkedHashSet<ApplicationEvent>();
}
```

#### 属性校验

AbstractEnvironment.validateRequiredProperties：

```java
@Override
public void validateRequiredProperties() throws MissingRequiredPropertiesException {
    this.propertyResolver.validateRequiredProperties();
}
```

AbstractPropertyResolver.validateRequiredProperties：

```java
@Override
public void validateRequiredProperties() {
    MissingRequiredPropertiesException ex = new MissingRequiredPropertiesException();
    for (String key : this.requiredProperties) {
        if (this.getProperty(key) == null) {
            ex.addMissingRequiredProperty(key);
        }
    }
    if (!ex.getMissingRequiredProperties().isEmpty()) {
        throw ex;
    }
}
```

requiredProperties 是通过 setRequiredProperties 方法设置的，保存在一个 list 里面，默认是空的，也就是不需要校验任何属性。

### BeanFactory 创建

由 obtainFreshBeanFactory 调用 AbstractRefreshableApplicationContext.refreshBeanFactory：

```java
@Override
protected final void refreshBeanFactory() throws BeansException {
    //如果已经存在，那么销毁之前的
    if (hasBeanFactory()) {
        destroyBeans();
        closeBeanFactory();
    }
    //创建了一个 DefaultListableBeanFactory 对象
    DefaultListableBeanFactory beanFactory = createBeanFactory();
    beanFactory.setSerializationId(getId());
    customizeBeanFactory(beanFactory);
    loadBeanDefinitions(beanFactory);
    synchronized (this.beanFactoryMonitor) {
        this.beanFactory = beanFactory;
    }
}
```

#### BeanFactory 接口

此接口实际上就是 Bean 容器，其继承体系：

![BeanFactory继承体系](images/BeanFactory.jpg)

#### BeanFactory 定制

AbstractRefreshableApplicationContext.customizeBeanFactory 方法用于给子类提供一个自由配置的机会，默认实现：

```java
protected void customizeBeanFactory(DefaultListableBeanFactory beanFactory) {
    if (this.allowBeanDefinitionOverriding != null) {
        //默认 false，不允许覆盖
        beanFactory.setAllowBeanDefinitionOverriding(this.allowBeanDefinitionOverriding);
    }
    if (this.allowCircularReferences != null) {
        //默认 false，不允许循环引用
        beanFactory.setAllowCircularReferences(this.allowCircularReferences);
    }
}
```

#### Bean 加载

AbstractXmlApplicationContext.loadBeanDefinitions，这个便是核心的 bean 加载了：

```java
@Override
protected void loadBeanDefinitions(DefaultListableBeanFactory beanFactory) {
    // Create a new XmlBeanDefinitionReader for the given BeanFactory.
    XmlBeanDefinitionReader beanDefinitionReader = new XmlBeanDefinitionReader(beanFactory);
    // Configure the bean definition reader with this context's
    // resource loading environment.
    beanDefinitionReader.setEnvironment(this.getEnvironment());
    beanDefinitionReader.setResourceLoader(this);
    beanDefinitionReader.setEntityResolver(new ResourceEntityResolver(this));
    // Allow a subclass to provide custom initialization of the reader,
    // then proceed with actually loading the bean definitions.
    //默认空实现
    initBeanDefinitionReader(beanDefinitionReader);
    loadBeanDefinitions(beanDefinitionReader);
}
```

##### EntityResolver

此处只说明用到的部分继承体系：

![EntityResolver继承体系](images/EntityResolver.jpg)

EntityResolver 接口在 org.xml.sax 中定义。DelegatingEntityResolver 用于 schema 和 dtd 的解析。

##### BeanDefinitionReader

继承体系：

![BeanDefinitionReader继承体系](images/BeanDefinitionReader.jpg)



##### 路径解析（Ant）

```java
protected void loadBeanDefinitions(XmlBeanDefinitionReader reader) {
    Resource[] configResources = getConfigResources();
    if (configResources != null) {
        reader.loadBeanDefinitions(configResources);
    }
    String[] configLocations = getConfigLocations();
    //here，用于路径解析
    if (configLocations != null) {
        reader.loadBeanDefinitions(configLocations);
    }
}
```

AbstractBeanDefinitionReader.loadBeanDefinitions：

```java
@Override
public int loadBeanDefinitions(String... locations) throws BeanDefinitionStoreException {
    Assert.notNull(locations, "Location array must not be null");
    int counter = 0;
    for (String location : locations) {
        counter += loadBeanDefinitions(location);
    }
    return counter;
}
```

之后调用：

```java
//第二个参数为空
public int loadBeanDefinitions(String location, Set<Resource> actualResources) {
    ResourceLoader resourceLoader = getResourceLoader();
    //参见 ResourceLoader 类图，ClassPathXmlApplicationContext 实现了此接口
    if (resourceLoader instanceof ResourcePatternResolver) {
        // Resource pattern matching available.
        try {
            Resource[] resources = ((ResourcePatternResolver) resourceLoader).getResources(location);
            int loadCount = loadBeanDefinitions(resources);
            if (actualResources != null) {
                for (Resource resource : resources) {
                    actualResources.add(resource);
                }
            }
            return loadCount;
        }
        catch (IOException ex) {
            throw new BeanDefinitionStoreException(
                    "Could not resolve bean definition resource pattern [" + location + "]", ex);
        }
    }
    else {
        // Can only load single resources by absolute URL.
        Resource resource = resourceLoader.getResource(location);
        int loadCount = loadBeanDefinitions(resource);
        if (actualResources != null) {
            actualResources.add(resource);
        }
        return loadCount;
    }
}
```

getResource 的实现在 AbstractApplicationContext：

```java
@Override
public Resource[] getResources(String locationPattern) throws IOException {
    //构造器中初始化，PathMatchingResourcePatternResolver 对象
    return this.resourcePatternResolver.getResources(locationPattern);
}
```

PathMatchingResourcePatternResolver 是 ResourceLoader 继承体系的一部分。

```java
@Override
public Resource[] getResources(String locationPattern) throws IOException {
    Assert.notNull(locationPattern, "Location pattern must not be null");
    // classpath:*
    if (locationPattern.startsWith(CLASSPATH_ALL_URL_PREFIX)) {
        // a class path resource (multiple resources for same name possible)
        // matcher 是一个 AntPathMatcher 对象
        if (getPathMatcher().isPattern(locationPattern
            .substring(CLASSPATH_ALL_URL_PREFIX.length()))) {
            // a class path resource pattern
            return findPathMatchingResources(locationPattern);
        } else {
            // all class path resources with the given name
            return findAllClassPathResources(locationPattern
                .substring(CLASSPATH_ALL_URL_PREFIX.length()));
        }
    } else {
        // Only look for a pattern after a prefix here
        // (to not get fooled by a pattern symbol in a strange prefix).
        int prefixEnd = locationPattern.indexOf(":") + 1;
        if (getPathMatcher().isPattern(locationPattern.substring(prefixEnd))) {
            // a file pattern
            return findPathMatchingResources(locationPattern);
        }
        else {
            // a single resource with the given name
            return new Resource[] {getResourceLoader().getResource(locationPattern)};
        }
    }
}
```

isPattern：

```java
@Override
public boolean isPattern(String path) {
    return (path.indexOf('*') != -1 || path.indexOf('?') != -1);
}
```

可以看出配置文件路径是支持 ant 风格的，也就是可以这么写：

```java
new ClassPathXmlApplicationContext("con*.xml");
```

具体怎么解析 ant 风格的就不写了。

##### 配置文件加载

入口方法在 AbstractBeanDefinitionReader 的 217 行：

```java
//加载
Resource[] resources = ((ResourcePatternResolver) resourceLoader).getResources(location);
//解析
int loadCount = loadBeanDefinitions(resources);
```

最终逐个调用 XmlBeanDefinitionReader 的 loadBeanDefinitions 方法：

```java
@Override
public int loadBeanDefinitions(Resource resource) {
    return loadBeanDefinitions(new EncodedResource(resource));
}
```

Resource 是代表一种资源的接口，其类图：

![Resource类图](images/Resource.jpg)

EncodedResource 扮演的其实是一个装饰器的模式，为 InputStreamSource 添加了字符编码（虽然默认为 null）。这样为我们自定义 xml 配置文件的编码方式提供了机会。

之后关键的源码只有两行：

```java
public int loadBeanDefinitions(EncodedResource encodedResource) throws BeanDefinitionStoreException {
    try (InputStream inputStream = encodedResource.getResource().getInputStream()) {
			InputSource inputSource = new InputSource(inputStream);
			return doLoadBeanDefinitions(inputSource, encodedResource.getResource());
		}
}
```

InputSource 是 org.xml.sax 的类。

doLoadBeanDefinitions：

```java
protected int doLoadBeanDefinitions(InputSource inputSource, Resource resource) {
    try {
			Document doc = doLoadDocument(inputSource, resource);
			int count = registerBeanDefinitions(doc, resource);
			if (logger.isDebugEnabled()) {
				logger.debug("Loaded " + count + " bean definitions from " + resource);
			}
			return count;
		}
}
```

doLoadDocument：

```java
protected Document doLoadDocument(InputSource inputSource, Resource resource) {
    return this.documentLoader.loadDocument(inputSource, getEntityResolver(), this.errorHandler,
        getValidationModeForResource(resource), isNamespaceAware());
}
```

documentLoader 是一个 DefaultDocumentLoader 对象，此类是 DocumentLoader 接口的唯一实现。getEntityResolver 方法返回 ResourceEntityResolver，上面说过了。errorHandler 是一个 SimpleSaxErrorHandler 对象。

校验模型其实就是确定 xml 文件使用 xsd 方式还是 dtd 方式来校验。Spring 会通过读取 xml 文件的方式判断应该采用哪种。

NamespaceAware 默认 false，因为默认配置了校验为 true。

DefaultDocumentLoader.loadDocument：

```java
@Override
public Document loadDocument(InputSource inputSource, EntityResolver entityResolver,
    ErrorHandler errorHandler, int validationMode, boolean namespaceAware) {
    //这里就是老套路了，可以看出，Spring 还是使用了 dom 的方式解析，即一次全部 load 到内存
    DocumentBuilderFactory factory = createDocumentBuilderFactory(validationMode, namespaceAware);
	if (logger.isTraceEnabled()) {
		logger.trace("Using JAXP provider [" + factory.getClass().getName() + "]");
	}
	DocumentBuilder builder = createDocumentBuilder(factory, entityResolver, errorHandler);
	return builder.parse(inputSource);
}
```

createDocumentBuilderFactory 比较有意思：

```java
protected DocumentBuilderFactory createDocumentBuilderFactory(int validationMode, boolean namespaceAware{
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    factory.setNamespaceAware(namespaceAware);
    if (validationMode != XmlValidationModeDetector.VALIDATION_NONE) {
        //此方法设为 true 仅对 dtd 有效，xsd(schema) 无效
        factory.setValidating(true);
        if (validationMode == XmlValidationModeDetector.VALIDATION_XSD) {
            // Enforce namespace aware for XSD...
             //开启 xsd(schema)支持
            factory.setNamespaceAware(true);
             //这个也是 Java 支持 Schema 的套路
            factory.setAttribute(SCHEMA_LANGUAGE_ATTRIBUTE, XSD_SCHEMA_LANGUAGE);
        }
    }
    return factory;
}
```

##### Bean 解析

XmlBeanDefinitionReader.registerBeanDefinitions：

```java
public int registerBeanDefinitions(Document doc, Resource resource) {
    BeanDefinitionDocumentReader documentReader = createBeanDefinitionDocumentReader();
    int countBefore = getRegistry().getBeanDefinitionCount();
    documentReader.registerBeanDefinitions(doc, createReaderContext(resource));
    return getRegistry().getBeanDefinitionCount() - countBefore;
}
```

createBeanDefinitionDocumentReader：

```java
protected BeanDefinitionDocumentReader createBeanDefinitionDocumentReader() {
    //反射机制	
	return BeanUtils.instantiateClass(this.documentReaderClass);
}
```

documentReaderClass 默认是 DefaultBeanDefinitionDocumentReader，这其实也是策略模式，通过 setter 方法可以更换其实现。

createReaderContext：

```java
public XmlReaderContext createReaderContext(Resource resource) {
    return new XmlReaderContext(resource, this.problemReporter, this.eventListener,
        this.sourceExtractor, this, getNamespaceHandlerResolver());
}
```

problemReporter 是一个 FailFastProblemReporter 对象。

eventListener 是 EmptyReaderEventListener 对象，此类里的方法都是空实现。

sourceExtractor 是 NullSourceExtractor 对象，直接返回空，也是空实现。

getNamespaceHandlerResolver 默认返回 DefaultNamespaceHandlerResolver 对象，用来获取 xsd 对应的处理器。

XmlReaderContext 的作用感觉就是这一堆参数的容器，糅合到一起传给 DocumentReader，并美其名为 Context。可以看出，Spring 中到处都是策略模式，大量操作被抽象成接口。

DefaultBeanDefinitionDocumentReader.registerBeanDefinitions：

```java
@Override
public void registerBeanDefinitions(Document doc, XmlReaderContext readerContext) {
	this.readerContext = readerContext;
	doRegisterBeanDefinitions(doc.getDocumentElement());
}
```

doRegisterBeanDefinitions：

```java
protected void doRegisterBeanDefinitions(Element root) {
    BeanDefinitionParserDelegate parent = this.delegate;
    this.delegate = createDelegate(getReaderContext(), root, parent);
    //默认的命名空间即
    //http://www.springframework.org/schema/beans
    if (this.delegate.isDefaultNamespace(root)) {
        //检查 profile 属性
        String profileSpec = root.getAttribute(PROFILE_ATTRIBUTE);
        if (StringUtils.hasText(profileSpec)) {
            //profile 属性可以分割
            String[] specifiedProfiles = StringUtils.tokenizeToStringArray(
                    profileSpec, BeanDefinitionParserDelegate.MULTI_VALUE_ATTRIBUTE_DELIMITERS);
            if (!getReaderContext().getEnvironment().acceptsProfiles(specifiedProfiles)) {
                return;
            }
        }
    }
    preProcessXml(root);
    parseBeanDefinitions(root, this.delegate);
    postProcessXml(root);
    this.delegate = parent;
}
```

delegate 的作用在于处理 beans 标签的嵌套，其实 Spring 配置文件是可以写成这样的：

```xml
<?xml version="1.0" encoding="UTF-8"?>    
<beans>    
    <bean class="base.SimpleBean"></bean>
    <beans>
        <bean class="java.lang.Object"></bean>
    </beans>
</beans>
```

xml（schema）的命名空间其实类似于 Java 的报名，命名空间采用 URL，比如 Spring 的是这样：

```xml
<?xml version="1.0" encoding="UTF-8"?>    
<beans xmlns="http://www.springframework.org/schema/beans"></beans>
```

xmlns 属性就是 xml 规范定义的用来设置命名空间的。这样设置了之后其实里面的 bean 元素全名就相当于http://www.springframework.org/schema/beans:bean，可以有效的防止命名冲突。命名空间可以通过规范定义的 org.w3c.dom.Node.getNamespaceURI 方法获得。

注意一下 profile 的检查，AbstractEnvironment.acceptsProfiles：

```java
//这个方法已经被标记为 Deprecated
@Override
public boolean acceptsProfiles(String... profiles) {
    Assert.notEmpty(profiles, "Must specify at least one profile");
    for (String profile : profiles) {
        if (StringUtils.hasLength(profile) && profile.charAt(0) == '!') {
            if (!isProfileActive(profile.substring(1))) {
                return true;
            }
        } else if (isProfileActive(profile)) {
            return true;
        }
    }
    return false;
}
```

原理很简单，从源码可以看出，**profile 属性支持取反**。

preProcessXml 方法是个空实现，供子类去覆盖，**目的在于给子类一个把我们自定义的标签转为 Spring 标准标签的机会**。

DefaultBeanDefinitionDocumentReader.parseBeanDefinitions：

```java
protected void parseBeanDefinitions(Element root, BeanDefinitionParserDelegate delegate) {
    if (delegate.isDefaultNamespace(root)) {
        NodeList nl = root.getChildNodes();
        for (int i = 0; i < nl.getLength(); i++) {
            Node node = nl.item(i);
            if (node instanceof Element) {
                Element ele = (Element) node;
                if (delegate.isDefaultNamespace(ele)) {
                    parseDefaultElement(ele, delegate);
                } else {
                    delegate.parseCustomElement(ele);
                }
            }
        }
    } else {
        delegate.parseCustomElement(root);
    }
}
```

可见，对于非默认命名空间的元素交由 delegate 处理。

#### 默认命名空间解析

即 import、alias、bean，嵌套的 beans 四种元素。DefaultBeanDefinitionDocumentReader.parseDefaultElement：

```java
private void parseDefaultElement(Element ele, BeanDefinitionParserDelegate delegate) {
    //"import"
    if (delegate.nodeNameEquals(ele, IMPORT_ELEMENT)) {
        importBeanDefinitionResource(ele);
    }
    //"alias"
    else if (delegate.nodeNameEquals(ele, ALIAS_ELEMENT)) {
        processAliasRegistration(ele);
    }
    //"bean"
    else if (delegate.nodeNameEquals(ele, BEAN_ELEMENT)) {
        processBeanDefinition(ele, delegate);
    }
    else if (delegate.nodeNameEquals(ele, NESTED_BEANS_ELEMENT)) {
        // recurse
        doRegisterBeanDefinitions(ele);
    }
}
```

##### import

写法示例：

```xml
<import resource="CTIContext.xml" />
<import resource="customerContext.xml" />
```

importBeanDefinitionResource 套路和之前的配置文件加载完全一样，**不过注意被 import 进来的文件是先于当前文件被解析的。**

##### alias

加入有一个 bean 名为 componentA-dataSource，但是另一个组件想以 componentB-dataSource 的名字使用，就可以这样定义

```xml
<alias name="componentA-dataSource" alias="componentB-dataSource"/>
```

processAliasRegistration 核心源码：

```java
protected void processAliasRegistration(Element ele) {
    String name = ele.getAttribute(NAME_ATTRIBUTE);
    String alias = ele.getAttribute(ALIAS_ATTRIBUTE);
    getReaderContext().getRegistry().registerAlias(name, alias);
    getReaderContext().fireAliasRegistered(name, alias, extractSource(ele));
}
```

从前面的源码可以发现，registry 其实就是 DefaultListableBeanFactory，它实现了 BeanDefinitionRegistry 接口。registerAlias 方法的实现在 SimpleAliasRegistry：

```java
@Override
public void registerAlias(String name, String alias) {
    Assert.hasText(name, "'name' must not be empty");
    Assert.hasText(alias, "'alias' must not be empty");
    //名字和别名一样
    if (alias.equals(name)) {
        //ConcurrentHashMap
        this.aliasMap.remove(alias);
    } else {
        String registeredName = this.aliasMap.get(alias);
        if (registeredName != null) {
            if (registeredName.equals(name)) {
                // An existing alias - no need to re-register
                return;
            }
            if (!allowAliasOverriding()) {
                throw new IllegalStateException
                    ("Cannot register alias '" + alias + "' for name '" +
                    name + "': It is already registered for name '" + registeredName + "'.");
            }
        }
        checkForAliasCircle(name, alias);
        this.aliasMap.put(alias, name);
    }
}
```

所以别名关系的保存使用 Map 完成，key 为别名，value 为原始名字。

##### bean

bean 节点是 Spring 最最常见的节点了。

DefaultBeanDefinitionDocumentReader.processBeanDefinition：

```java
protected void processBeanDefinition(Element ele, BeanDefinitionParserDelegate delegate) {
    BeanDefinitionHolder bdHolder = delegate.parseBeanDefinitionElement(ele);
    if (bdHolder != null) {
        bdHolder = delegate.decorateBeanDefinitionIfRequired(ele, bdHolder);
        try {
            // Register the final decorated instance.
            BeanDefinitionReaderUtils.registerBeanDefinition
                (bdHolder, getReaderContext().getRegistry());
        }
        catch (BeanDefinitionStoreException ex) {
            getReaderContext().error("Failed to register bean definition with name '" +
                    bdHolder.getBeanName() + "'", ele, ex);
        }
        // Send registration event.
        getReaderContext().fireComponentRegistered(new BeanComponentDefinition(bdHolder));
    }
}
```

###### id & name 处理

最终调用 BeanDefinitionParserDelegate.parseBeanDefinitionElement(Element ele, BeanDefinition containingBean)，源码较长，分部分说明。

首先获取到 id 和 name 属性，**name 属性支持配置多个，以逗号分隔，如果没有指定 id，那么将以第一个 name 属性值代替。id 必须是唯一的，name 属性其实是 alias 的角色，可以和其它的 bean 重复，如果 name 也没有配置，那么其实什么也没做**。

```java
String id = ele.getAttribute(ID_ATTRIBUTE);
String nameAttr = ele.getAttribute(NAME_ATTRIBUTE);
List<String> aliases = new ArrayList<String>();
if (StringUtils.hasLength(nameAttr)) {
    //按逗号分隔
    String[] nameArr = StringUtils.tokenizeToStringArray
        (nameAttr, MULTI_VALUE_ATTRIBUTE_DELIMITERS);
    aliases.addAll(Arrays.asList(nameArr));
}
String beanName = id;
if (!StringUtils.hasText(beanName) && !aliases.isEmpty()) {
    //name 的第一个值作为 id
    beanName = aliases.remove(0);
}
//默认 null
if (containingBean == null) {
    //校验 id 是否已重复，如果重复直接抛异常
    //校验是通过内部一个 HashSet 完成的，出现过的 id 都会保存进此 Set
    checkNameUniqueness(beanName, aliases, ele);
}
```

###### beanName 生成

如果 name 和 id 属性都没有指定，那么 Spring 会自己生成一个，BeanDefinitionParserDelegate.parseBeanDefinitionElement：

```java
beanName = this.readerContext.generateBeanName(beanDefinition);
String beanClassName = beanDefinition.getBeanClassName();
aliases.add(beanClassName);
```

可见，Spring 同时会把类名作为其别名。

最终调用的是 BeanDefinitionReaderUtils.generateBeanName：

```java
public static String generateBeanName(
        BeanDefinition definition, BeanDefinitionRegistry registry, boolean isInnerBean) {
    String generatedBeanName = definition.getBeanClassName();
    if (generatedBeanName == null) {
        if (definition.getParentName() != null) {
            generatedBeanName = definition.getParentName() + "$child";
             //工厂方法产生的 bean
        } else if (definition.getFactoryBeanName() != null) {
            generatedBeanName = definition.getFactoryBeanName() + "$created";
        }
    }
    String id = generatedBeanName;
    if (isInnerBean) {
        // Inner bean: generate identity hashcode suffix.
        id = generatedBeanName + GENERATED_BEAN_NAME_SEPARATOR + 
            ObjectUtils.getIdentityHexString(definition);
    } else {
        // Top-level bean: use plain class name.
        // Increase counter until the id is unique.
        int counter = -1;
         //用类名#自增的数字命名
        while (counter == -1 || registry.containsBeanDefinition(id)) {
            counter++;
            id = generatedBeanName + GENERATED_BEAN_NAME_SEPARATOR + counter;
        }
    }
    return id;
}
```

###### bean 解析

还是分部分说明（parseBeanDefinitionElement）。

首先获取到 bean 的 class 属性和 parent 属性，配置了 parent 之后，当前 bean 会继承父 bean 的属性。之后根据 class 和 parent 创建 BeanDefinition 对象。

```java
String className = null;
if (ele.hasAttribute(CLASS_ATTRIBUTE)) {
    className = ele.getAttribute(CLASS_ATTRIBUTE).trim();
}
String parent = null;
if (ele.hasAttribute(PARENT_ATTRIBUTE)) {
    parent = ele.getAttribute(PARENT_ATTRIBUTE);
}
AbstractBeanDefinition bd = createBeanDefinition(className, parent);
```

BeanDefinition 的创建在 BeanDefinitionReaderUtils.createBeanDefinition：

```java
public static AbstractBeanDefinition createBeanDefinition(
        String parentName, String className, ClassLoader classLoader) {
    GenericBeanDefinition bd = new GenericBeanDefinition();
    bd.setParentName(parentName);
    if (className != null) {
        if (classLoader != null) {
            bd.setBeanClass(ClassUtils.forName(className, classLoader));
        }
        else {
            bd.setBeanClassName(className);
        }
    }
    return bd;
}
```

之后是解析 bean 的其它属性，其实就是读取其配置，调用相应的 setter 方法保存在 BeanDefinition 中：

```java
parseBeanDefinitionAttributes(ele, beanName, containingBean, bd);
```

之后解析 bean 的 decription 子元素：

```xml
<bean id="b" name="one, two" class="base.SimpleBean">
    <description>SimpleBean</description>
</bean>
```

就仅仅是个描述。

然后是 meta 子元素的解析，meta 元素在 xml 配置文件里是这样的：

```xml
<bean id="b" name="one, two" class="base.SimpleBean">
    <meta key="name" value="skywalker"/>
</bean>
```

注释上说，这样可以将任意的元数据附到对应的 bean definition 上。解析过程源码：

```java
public void parseMetaElements(Element ele, BeanMetadataAttributeAccessor attributeAccessor) {
    NodeList nl = ele.getChildNodes();
    for (int i = 0; i < nl.getLength(); i++) {
        Node node = nl.item(i);
        if (isCandidateElement(node) && nodeNameEquals(node, META_ELEMENT)) {
            Element metaElement = (Element) node;
            String key = metaElement.getAttribute(KEY_ATTRIBUTE);
            String value = metaElement.getAttribute(VALUE_ATTRIBUTE);
             //就是一个key、value的载体
            BeanMetadataAttribute attribute = new BeanMetadataAttribute(key, value);
             //sourceExtractor 默认是 NullSourceExtractor，返回的是空
            attribute.setSource(extractSource(metaElement));
            attributeAccessor.addMetadataAttribute(attribute);
        }
    }
}
```

AbstractBeanDefinition 继承自 BeanMetadataAttributeAccessor 类，底层使用了一个 LinkedHashMap 保存 metadata。

lookup-method 解析：

此标签的作用在于当一个 bean 的某个方法被设置为 lookup-method 后，**每次调用此方法时，都会返回一个新的指定 bean 的对象**。用法示例：

```xml
<bean id="apple" class="cn.com.willchen.test.di.Apple" scope="prototype"/>
<!--水果盘-->
<bean id="fruitPlate" class="cn.com.willchen.test.di.FruitPlate">
    <lookup-method name="getFruit" bean="apple"/>
</bean>
```

数据保存在 Set 中，对应的类是 MethodOverrides。可以参考：

[Spring - lookup-method 方式实现依赖注入](http://www.cnblogs.com/ViviChan/p/4981619.html)

replace-mothod 解析：

此标签用于替换 bean 里面的特定的方法实现，替换者必须实现 Spring 的 MethodReplacer 接口，有点像 AOP 的意思。

配置文件示例：

```xml
<bean name="replacer" class="springroad.deomo.chap4.MethodReplace" />  
<bean name="testBean" class="springroad.deomo.chap4.LookupMethodBean">
    <replaced-method name="test" replacer="replacer">
        <arg-type match="String" />
    </replaced-method>  
</bean> 
```

arg-type 的作用是指定替换方法的参数类型，因为接口的定义参数都是 Object 的。参考：[SPRING.NET 1.3.2 学习20--方法注入之替换方法注入](http://blog.csdn.net/lee576/article/details/8725548)

解析之后将数据放在 ReplaceOverride 对象中，里面有一个 LinkedList<String> 专门用于保存 arg-type。

构造参数（constructor-arg）解析：

作用一目了然，使用示例：

```xml
<bean class="base.SimpleBean">
    <constructor-arg>
        <value type="java.lang.String">Cat</value>
    </constructor-arg>
</bean>
```

type 一般不需要指定，除了泛型集合那种。除此之外，constructor-arg 还支持 name、index、ref 等属性，可以具体的指定参数的位置等。构造参数解析后保存在BeanDefinition 内部一个 ConstructorArgumentValues 对象中。如果设置了 index 属性，那么以 Map<Integer, ValueHolder> 的形式保存，反之，以 List<ValueHolder> 的形式保存。

property 解析：

非常常用的标签，用来为 bean 的属性赋值，支持 value 和 ref 两种形式，示例：

```xml
<bean class="base.SimpleBean">
    <property name="name" value="skywalker" />
</bean>
```

value 和 ref 属性不能同时出现，如果是 ref，那么将其值保存在不可变的 RuntimeBeanReference 对象中，其实现了 BeanReference 接口，此接口只有一个 getBeanName 方法。如果是 value，那么将其值保存在 TypedStringValue 对象中。最终将对象保存在 BeanDefinition 内部一个 MutablePropertyValues 对象中（内部以 ArrayList 实现）。

qualifier 解析：

配置示例：

```xml
<bean class="base.Student">
    <property name="name" value="skywalker"></property>
    <property name="age" value="12"></property>
    <qualifier type="org.springframework.beans.factory.annotation.Qualifier" value="student" />
</bean>	
<bean class="base.Student">
    <property name="name" value="seaswalker"></property>
    <property name="age" value="15"></property>
    <qualifier value="student_2"></qualifier>
</bean>
<bean class="base.SimpleBean" />
```

SimpleBean 部分源码：

```java
@Autowired
@Qualifier("student")
private Student student;
```

此标签和 @Qualifier，@Autowired 两个注解一起使用才有作用。@Autowired 注解采用按类型查找的方式进行注入，如果找到多个需要类型的 bean 便会报错，有了 @Qualifier 标签就可以再按照此注解指定的名称查找。两者结合相当于实现了按类型+名称注入。type 属性可以不指定，因为默认就是那个。qualifier 标签可以有 attribute 子元素，比如：

```xml
<qualifier type="org.springframework.beans.factory.annotation.Qualifier" value="student">
    <attribute key="id" value="1"/>
</qualifier>
```

貌似是用来在 qualifier 也区分不开的时候使用。attribute 键值对保存在 BeanMetadataAttribute 对象中。整个 qualifier 保存在 AutowireCandidateQualifier 对象中。

###### Bean 装饰

这部分是针对其它 schema 的属性以及子节点，比如：

```xml
<bean class="base.Student" primary="true">
    <context:property-override />
</bean>
```

###### Bean 注册

BeanDefinitionReaderUtils.registerBeanDefinition：

```java
public static void registerBeanDefinition(
    BeanDefinitionHolder definitionHolder, BeanDefinitionRegistry registry) {
    // Register bean definition under primary name.
    String beanName = definitionHolder.getBeanName();
    registry.registerBeanDefinition(beanName, definitionHolder.getBeanDefinition());
    // Register aliases for bean name, if any.
    String[] aliases = definitionHolder.getAliases();
    if (aliases != null) {
        for (String alias : aliases) {
            registry.registerAlias(beanName, alias);
        }
    }
}
```

registry 其实就是 DefaultListableBeanFactory 对象，registerBeanDefinition 方法主要就干了这么两件事：

```java
@Override
public void registerBeanDefinition(String beanName, BeanDefinition beanDefinition) {
    this.beanDefinitionMap.put(beanName, beanDefinition);
    this.beanDefinitionNames.add(beanName);
}
```

一个是 Map，另一个是 List，一目了然。registerAlias 方法的实现在其父类 SimpleAliasRegistry，就是把键值对放在了一个 ConcurrentHashMap 里。

ComponentRegistered 事件触发：

默认是个空实现，前面说过了。

###### BeanDefiniton 数据结构

BeanDefiniton 数据结构如下图：

![BeanDefinition数据结构](images/BeanDefinition.jpg)

##### beans

beans 元素的嵌套直接递归调用 DefaultBeanDefinitionDocumentReader.parseBeanDefinitions。

#### 其它命名空间解析

入口在 DefaultBeanDefinitionDocumentReader.parseBeanDefinitions->BeanDefinitionParserDelegate.parseCustomElement（第二个参数为空）：

```java
public BeanDefinition parseCustomElement(Element ele, BeanDefinition containingBd) {
    String namespaceUri = getNamespaceURI(ele);
    NamespaceHandler handler = this.readerContext.getNamespaceHandlerResolver().resolve(namespaceUri);
    return handler.parse(ele, new ParserContext(this.readerContext, this, containingBd));
}
```

NamespaceHandlerResolver 由 XmlBeanDefinitionReader 初始化，是一个 DefaultNamespaceHandlerResolver 对象，也是 NamespaceHandlerResolver 接口的唯一实现。

其 resolve 方法：

```java
@Override
public NamespaceHandler resolve(String namespaceUri) {
    Map<String, Object> handlerMappings = getHandlerMappings();
    Object handlerOrClassName = handlerMappings.get(namespaceUri);
    if (handlerOrClassName == null) {
        return null;
    } else if (handlerOrClassName instanceof NamespaceHandler) {
        return (NamespaceHandler) handlerOrClassName;
    } else {
        String className = (String) handlerOrClassName;
        Class<?> handlerClass = ClassUtils.forName(className, this.classLoader);
        NamespaceHandler namespaceHandler = (NamespaceHandler) BeanUtils.instantiateClass(handlerClass);
        namespaceHandler.init();
        handlerMappings.put(namespaceUri, namespaceHandler);
        return namespaceHandler;
    }
}
```

容易看出，Spring 其实使用了一个 Map 了保存其映射关系，key 就是命名空间的 uri，value 是 **NamespaceHandler 对象或是 Class 完整名，如果发现是类名，那么用反射的方法进行初始化，如果是 NamespaceHandler 对象，那么直接返回**。

NamespaceHandler 映射关系来自于各个 Spring jar 包下的 META-INF/spring.handlers 文件，以 spring-context 包为例：

```html
http\://www.springframework.org/schema/context=org.springframework.context.config.ContextNamespaceHandler
http\://www.springframework.org/schema/jee=org.springframework.ejb.config.JeeNamespaceHandler
http\://www.springframework.org/schema/lang=org.springframework.scripting.config.LangNamespaceHandler
http\://www.springframework.org/schema/task=org.springframework.scheduling.config.TaskNamespaceHandler
http\://www.springframework.org/schema/cache=org.springframework.cache.config.CacheNamespaceHandler
```

##### NamespaceHandler 继承体系

![NamespaceHandler继承体系](images/NamespaceHandler.jpg)

##### init

resolve 中调用了其 init 方法，此方法用以向 NamespaceHandler 对象注册 BeanDefinitionParser 对象。**此接口用以解析顶层（beans 下）的非默认命名空间元素，比如`<context:annotation-config />`**。

所以这样逻辑就很容易理解了： **每种子标签的解析仍是策略模式的体现，init 负责向父类 NamespaceHandlerSupport 注册不同的策略，由父类的 NamespaceHandlerSupport.parse 方法根据具体的子标签调用相应的策略完成解析的过程**。

##### BeanFactory 数据结构

BeanDefinition 在 BeanFactory 中的主要数据结构如下图：

![Beanfactory数据结构](images/Beanfactory_structure.jpg)

### prepareBeanFactory

此方法负责对 BeanFactory 进行一些特征的设置工作，"特征"包含这么几个方面：

#### BeanExpressionResolver

此接口只有一个实现：StandardBeanExpressionResolver。接口只含有一个方法：

```java
Object evaluate(String value, BeanExpressionContext evalContext)
```

prepareBeanFactory 将一个此对象放入 BeanFactory：

```java
beanFactory.setBeanExpressionResolver(new 						 			StandardBeanExpressionResolver(beanFactory.getBeanClassLoader()));
```

StandardBeanExpressionResolver 对象内部有一个关键的成员：SpelExpressionParser，其整个类图：

![ExpressionParser继承体系](images/ExpressionParser.jpg)

这便是 Spring3.0 开始出现的 Spel 表达式的解释器。

#### PropertyEditorRegistrar

此接口用于向 Spring 注册 java.beans.PropertyEditor，只有一个方法：

```java
registerCustomEditors(PropertyEditorRegistry registry)
```

实现也只有一个：ResourceEditorRegistrar。

在编写 xml 配置时，我们设置的值都是字符串形式，所以在使用时肯定需要转为我们需要的类型，PropertyEditor 接口正是定义了这么个东西。

prepareBeanFactory：

```java
beanFactory.addPropertyEditorRegistrar(new ResourceEditorRegistrar(this, getEnvironment()));
```

BeanFactory 也暴露了 registerCustomEditors 方法用以添加自定义的转换器，所以这个地方是组合模式的体现。

我们有两种方式可以添加自定义 PropertyEditor：

- 通过`context.getBeanFactory().registerCustomEditor`

- 通过 Spring 配置文件：

  ```xml
  <bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="customEditors">
            <map>
                <entry key="base.Cat" value="base.CatEditor" /> 
        </map>
    </property>
  </bean>
  ```

参考: [深入理解 JavaBean（2）：属性编辑器 PropertyEditor](http://blog.csdn.net/zhoudaxia/article/details/36247883)

#### 环境注入

在 Spring 中我们自己的 bean 可以通过实现 EnvironmentAware 等一系列 Aware 接口获取到 Spring 内部的一些对象。prepareBeanFactory：

```java
beanFactory.addBeanPostProcessor(new ApplicationContextAwareProcessor(this));
```

ApplicationContextAwareProcessor 核心的 invokeAwareInterfaces 方法：

```java
private void invokeAwareInterfaces(Object bean) {
    if (bean instanceof Aware) {
        if (bean instanceof EnvironmentAware) {
            ((EnvironmentAware) bean).setEnvironment(this.applicationContext.getEnvironment());
        }
        if (bean instanceof EmbeddedValueResolverAware) {
            ((EmbeddedValueResolverAware) bean).setEmbeddedValueResolver(this.embeddedValueResolver);
        }
        //....
    }
}
```

此部分设置哪些接口在进行依赖注入的时候应该被忽略：

```java
beanFactory.ignoreDependencyInterface(ResourceLoaderAware.class);
beanFactory.ignoreDependencyInterface(ApplicationEventPublisherAware.class);
beanFactory.ignoreDependencyInterface(MessageSourceAware.class);
beanFactory.ignoreDependencyInterface(ApplicationContextAware.class);
beanFactory.ignoreDependencyInterface(EnvironmentAware.class);
```

#### bean 伪装

有些对象并不在 BeanFactory 中，但是我们依然想让它们可以被装配，这就需要伪装一下：

```java
beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);
beanFactory.registerResolvableDependency(ResourceLoader.class, this);
beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);
beanFactory.registerResolvableDependency(ApplicationContext.class, this);
```

伪装关系保存在一个 Map<Class<?>, Object> 里。

#### LoadTimeWeaver

如果配置了此 bean，那么：

```java
if (beanFactory.containsBean(LOAD_TIME_WEAVER_BEAN_NAME)) {
    beanFactory.addBeanPostProcessor(new LoadTimeWeaverAwareProcessor(beanFactory));
    // Set a temporary ClassLoader for type matching.
    beanFactory.setTempClassLoader(new ContextTypeMatchClassLoader(beanFactory.getBeanClassLoader()));
}
```

这个东西具体是干什么的在后面 context:load-time-weaver 中说明。

#### 注册环境

源码：

```java
if (!beanFactory.containsLocalBean(ENVIRONMENT_BEAN_NAME)) {
    beanFactory.registerSingleton(ENVIRONMENT_BEAN_NAME, getEnvironment());
}
if (!beanFactory.containsLocalBean(SYSTEM_PROPERTIES_BEAN_NAME)) {
    beanFactory.registerSingleton(SYSTEM_PROPERTIES_BEAN_NAME, getEnvironment().getSystemProperties());
}
if (!beanFactory.containsLocalBean(SYSTEM_ENVIRONMENT_BEAN_NAME)) {
    beanFactory.registerSingleton(SYSTEM_ENVIRONMENT_BEAN_NAME, getEnvironment().
        getSystemEnvironment());
}
```

containsLocalBean 特殊之处在于不会去父 BeanFactory 寻找。

### postProcessBeanFactory

此方法允许子类在所有的 bean 尚未初始化之前注册 BeanPostProcessor，空实现且没有子类覆盖。

### invokeBeanFactoryPostProcessors

BeanFactoryPostProcessor 接口允许我们在 bean 正式初始化之前改变其值。此接口只有一个方法：

```java
protected void invokeBeanFactoryPostProcessors(ConfigurableListableBeanFactory beanFactory);
```

有两种方式可以向 Spring 添加此对象：

- 通过代码的方式：

  ```java
  context.addBeanFactoryPostProcessor
  ```

- 通过 xml 配置的方式：

  ```xml
  <bean class="base.SimpleBeanFactoryPostProcessor" />
  ```

注意此时尚未进行 bean 的初始化工作，初始化是在后面的 finishBeanFactoryInitialization 进行的，所以在 BeanFactoryPostProcessor 对象中获取 bean 会导致提前初始化。

此方法的关键源码：

```java
protected void invokeBeanFactoryPostProcessors(ConfigurableListableBeanFactory beanFactory) {
    PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(beanFactory,
        getBeanFactoryPostProcessors());
}
```

getBeanFactoryPostProcessors 获取的就是 AbstractApplicationContext 的成员 beanFactoryPostProcessors(ArrayList)，但是很有意思，**只有通过context.addBeanFactoryPostProcessor 这种方式添加的才会出现在这个 List 里，所以对于 xml 配置方式，此 List 其实没有任何元素。玄机就在PostProcessorRegistrationDelegate 里**。

核心思想就是使用 BeanFactory 的 getBeanNamesForType 方法获取相应的 BeanDefinition 的 name 数组，之后逐一调用 getBean 方法获取到 bean（初始化），getBean 方法后面再说。

注意此处有一个优先级的概念，如果你的 BeanFactoryPostProcessor 同时实现了 Ordered 或者是 PriorityOrdered 接口，那么会被首先执行。

### BeanPostProcessor 注册

此部分实质上是在 BeanDefinitions 中寻找 BeanPostProcessor，之后调用 BeanFactory.addBeanPostProcessor 方法保存在一个 List 中，注意添加时仍然有优先级的概念，优先级高的在前面。

### MessageSource

此接口用以支持 Spring 国际化。继承体系如下：

![MessageSource继承体系](images/MessageSource.jpg)

AbstractApplicationContext的initMessageSource() 方法就是在 BeanFactory 中查找 MessageSource 的 bean，如果配置了此 bean，那么调用 getBean 方法完成其初始化并将其保存在 AbstractApplicationContext 内部 messageSource 成员变量中，用以处理 ApplicationContext 的 getMessage 调用，因为从继承体系上来看，ApplicationContext 是 MessageSource 的子类，此处是委托模式的体现。如果没有配置此 bean，那么初始化一个 DelegatingMessageSource 对象，此类是一个空实现，同样用以处理 getMessage 调用请求。

参考: [学习 Spring 必学的 Java 基础知识（8）----国际化信息](http://stamen.iteye.com/blog/1541732)

### 事件驱动

此接口代表了 Spring 的事件驱动（监听器）模式。一个事件驱动包含三部分：

#### 事件

Java 的所有事件对象一般都是 java.util.EventObject 的子类，Spring 的整个继承体系如下：

![EventObject继承体系](images/EventObject.jpg)

#### 发布者

##### ApplicationEventPublisher

![ApplicationEventPublisher继承体系](images/ApplicationEventPublisher.jpg)

一目了然。

##### ApplicationEventMulticaster

ApplicationEventPublisher 实际上正是将请求委托给 ApplicationEventMulticaster 来实现的。其继承体系：

![ApplicationEventMulticaster继承体系](images/ApplicationEventMulticaster.jpg)

#### 监听器

所有的监听器是 JDK EventListener 的子类，这是一个 mark 接口。继承体系：

![EventListener继承体系](images/EventListener.jpg)

可以看出 SmartApplicationListener 和 GenericApplicationListener 是高度相似的，都提供了事件类型检测和顺序机制，而后者是从 Spring4.2 加入的，Spring 官方文档推荐使用后者代替前者。

#### 初始化

前面说过 ApplicationEventPublisher 是通过委托给 ApplicationEventMulticaster 实现的，所以 refresh 方法中完成的是对 ApplicationEventMulticaster 的初始化：

```java
// Initialize event multicaster for this context.
initApplicationEventMulticaster();
```

initApplicationEventMulticaster 则首先在 BeanFactory 中寻找 ApplicationEventMulticaster 的 bean，如果找到，那么调用 getBean 方法将其初始化，如果找不到那么使用 SimpleApplicationEventMulticaster。

#### 事件发布

AbstractApplicationContext.publishEvent 核心代码：

```java
protected void publishEvent(Object event, ResolvableType eventType) {
    getApplicationEventMulticaster().multicastEvent(applicationEvent, eventType);
}
```

SimpleApplicationEventMulticaster.multicastEvent：

```java
@Override
public void multicastEvent(final ApplicationEvent event, ResolvableType eventType) {
    ResolvableType type = (eventType != null ? eventType : resolveDefaultEventType(event));
    for (final ApplicationListener<?> listener : getApplicationListeners(event, type)) {
        Executor executor = getTaskExecutor();
        if (executor != null) {
            executor.execute(new Runnable() {
                @Override
                public void run() {
                    invokeListener(listener, event);
                }
            });
        } else {
            invokeListener(listener, event);
        }
    }
}
```

##### 监听器获取

获取当然还是通过 beanFactory 的 getBean 来完成的，值得注意的是 Spring 在此处使用了缓存（ConcurrentHashMap）来加速查找的过程。

##### 同步/异步

可以看出，如果 executor 不为空，那么监听器的执行实际上是异步的。那么如何配置同步/异步呢?

###### 全局

```xml
<task:executor id="multicasterExecutor" pool-size="3"/>
<bean class="org.springframework.context.event.SimpleApplicationEventMulticaster">
    <property name="taskExecutor" ref="multicasterExecutor"></property>
</bean>
```

task schema 是 Spring 从 3.0 开始加入的，使我们可以不再依赖于 Quartz 实现定时任务，源码在 org.springframework.core.task 包下，使用需要引入 schema：

```xml
xmlns:task="http://www.springframework.org/schema/task"
xsi:schemaLocation="http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd"
```

可以参考: [Spring 定时任务的几种实现](http://gong1208.iteye.com/blog/1773177)

###### 注解

开启注解支持：

```xml
<!-- 开启@AspectJ AOP代理 -->  
<aop:aspectj-autoproxy proxy-target-class="true"/>  
<!-- 任务调度器 -->  
<task:scheduler id="scheduler" pool-size="10"/>  
<!-- 任务执行器 -->  
<task:executor id="executor" pool-size="10"/>  
<!--开启注解调度支持 @Async @Scheduled-->  
<task:annotation-driven executor="executor" scheduler="scheduler" proxy-target-class="true"/>  
```

在代码中使用示例：

```java
@Component  
public class EmailRegisterListener implements ApplicationListener<RegisterEvent> {  
    @Async  
    @Override  
    public void onApplicationEvent(final RegisterEvent event) {  
        System.out.println("注册成功，发送确认邮件给：" + ((User)event.getSource()).getUsername());  
    }  
}  
```

参考: [详解 Spring 事件驱动模型](http://jinnianshilongnian.iteye.com/blog/1902886)

### onRefresh

这又是一个模版方法，允许子类在进行 bean 初始化之前进行一些定制操作。默认空实现。

### ApplicationListener 注册

registerListeners 方法干的，没什么好说的。

### singleton 初始化

finishBeanFactoryInitialization：

```java
protected void finishBeanFactoryInitialization(ConfigurableListableBeanFactory beanFactory) {
    if (beanFactory.containsBean(CONVERSION_SERVICE_BEAN_NAME) &&
            beanFactory.isTypeMatch(CONVERSION_SERVICE_BEAN_NAME, ConversionService.class)) {
        beanFactory.setConversionService(
                beanFactory.getBean(CONVERSION_SERVICE_BEAN_NAME, ConversionService.class));
    }
    if (!beanFactory.hasEmbeddedValueResolver()) {
        beanFactory.addEmbeddedValueResolver(new StringValueResolver() {
            @Override
            public String resolveStringValue(String strVal) {
                return getEnvironment().resolvePlaceholders(strVal);
            }
        });
    }
    String[] weaverAwareNames = beanFactory.getBeanNamesForType
        (LoadTimeWeaverAware.class, false, false);
    for (String weaverAwareName : weaverAwareNames) {
        getBean(weaverAwareName);
    }
    // Allow for caching all bean definition metadata, not expecting further changes.
    beanFactory.freezeConfiguration();
    // Instantiate all remaining (non-lazy-init) singletons.
    beanFactory.preInstantiateSingletons();
}
```

分部分说明。

#### ConversionService

此接口用于类型之间的转换，在 Spring 里其实就是把配置文件中的 String 转为其它类型，从 3.0 开始出现，目的和 JDK 的 PropertyEditor 接口是一样的，参考 ConfigurableBeanFactory.setConversionService 注释：

> Specify a Spring 3.0 ConversionService to use for converting
> property values, as an alternative to JavaBeans PropertyEditors.
> @since 3.0

#### StringValueResolver

用于解析注解的值。接口只定义了一个方法：

```java
String resolveStringValue(String strVal);
```

#### LoadTimeWeaverAware

实现了此接口的 bean 可以得到 LoadTimeWeaver，此处仅仅初始化。

#### 初始化

DefaultListableBeanFactory.preInstantiateSingletons：

```java
@Override
public void preInstantiateSingletons() throws BeansException {
    List<String> beanNames = new ArrayList<String>(this.beanDefinitionNames);
    for (String beanName : beanNames) {
        RootBeanDefinition bd = getMergedLocalBeanDefinition(beanName);
        if (!bd.isAbstract() && bd.isSingleton() && !bd.isLazyInit()) {
            if (isFactoryBean(beanName)) {
                final FactoryBean<?> factory = (FactoryBean<?>) getBean(FACTORY_BEAN_PREFIX 
                    + beanName);
                boolean isEagerInit;
                if (System.getSecurityManager() != null && factory instanceof SmartFactoryBean) {
                    isEagerInit = AccessController.doPrivileged(new PrivilegedAction<Boolean>() {
                        @Override
                        public Boolean run() {
                            return ((SmartFactoryBean<?>) factory).isEagerInit();
                        }
                    }, getAccessControlContext());
                }
                else {
                    isEagerInit = (factory instanceof SmartFactoryBean &&
                            ((SmartFactoryBean<?>) factory).isEagerInit());
                }
                if (isEagerInit) {
                    getBean(beanName);
                }
            }
            else {
                getBean(beanName);
            }
        }
    }

    // Trigger post-initialization callback for all applicable beans...
    for (String beanName : beanNames) {
        Object singletonInstance = getSingleton(beanName);
        if (singletonInstance instanceof SmartInitializingSingleton) {
            final SmartInitializingSingleton smartSingleton = 
                (SmartInitializingSingleton) singletonInstance;
            if (System.getSecurityManager() != null) {
                AccessController.doPrivileged(new PrivilegedAction<Object>() {
                    @Override
                    public Object run() {
                        smartSingleton.afterSingletonsInstantiated();
                        return null;
                    }
                }, getAccessControlContext());
            }
            else {
                smartSingleton.afterSingletonsInstantiated();
            }
        }
    }
}
```

首先进行 Singleton 的初始化，其中如果 bean 是 FactoryBean 类型（注意，只定义了 factory-method 属性的普通 bean 并不是 FactoryBean），并且还是 SmartFactoryBean 类型，那么需要判断是否需要 eagerInit（isEagerInit 是此接口定义的方法）。

# getBean

这里便是 bean 初始化的核心逻辑。源码比较复杂，分开说。以 getBean(String name) 为例。AbstractBeanFactory.getBean：

```java
@Override
public Object getBean(String name) throws BeansException {
    return doGetBean(name, null, null, false);
}
```

第二个参数表示 bean 的 Class 类型，第三个表示创建 bean 需要的参数，最后一个表示不需要进行类型检查。

## beanName 转化

```java
final String beanName = transformedBeanName(name);
```

这里是将 FactoryBean 的前缀去掉以及将别名转为真实的名字。

## 手动注册 bean 检测

前面注册环境一节说过，Spring 其实手动注册了一些单例 bean。这一步就是检测是不是这些 bean。如果是，那么再检测是不是工厂 bean，如果是返回其工厂方法返回的实例，如果不是返回 bean 本身。 

```java
Object sharedInstance = getSingleton(beanName);
if (sharedInstance != null && args == null) {
    bean = getObjectForBeanInstance(sharedInstance, name, beanName, null);
}
```

## 检查父容器

如果父容器存在并且存在此 bean 定义，那么交由其父容器初始化：

```java
BeanFactory parentBeanFactory = getParentBeanFactory();
if (parentBeanFactory != null && !containsBeanDefinition(beanName)) {
    // Not found -> check parent.
    //此方法其实是做了前面 beanName 转化的逆操作，因为父容器同样会进行转化操作
    String nameToLookup = originalBeanName(name);
    if (args != null) {
        // Delegation to parent with explicit args.
        return (T) parentBeanFactory.getBean(nameToLookup, args);
    } else {
        // No args -> delegate to standard getBean method.
        return parentBeanFactory.getBean(nameToLookup, requiredType);
    }
}
```

## 依赖初始化

bean 可以由 depends-on 属性配置依赖的 bean。Spring 会首先初始化依赖的 bean。

```java
String[] dependsOn = mbd.getDependsOn();
if (dependsOn != null) {
    for (String dependsOnBean : dependsOn) {
         //检测是否存在循环依赖
        if (isDependent(beanName, dependsOnBean)) {
            throw new BeanCreationException(mbd.getResourceDescription(), beanName,
            "Circular depends-on relationship between '" + beanName + "' and '" + dependsOnBean + "'");
        }
        registerDependentBean(dependsOnBean, beanName);
        getBean(dependsOnBean);
    }
}
```

registerDependentBean 进行了依赖关系的注册，这么做的原因是 Spring 在即进行 bean 销毁的时候会首先销毁被依赖的 bean。依赖关系的保存是通过一个 ConcurrentHashMap<String, Set<String>> 完成的，key 是 bean 的真实名字。

## Singleton 初始化

虽然这里大纲是 Singleton 初始化，但是 getBean 方法本身是包括所有 scope 的初始化，在这里一次说明了。

```java
if (mbd.isSingleton()) {
    sharedInstance = getSingleton(beanName, new ObjectFactory<Object>() {
        @Override
        public Object getObject() throws BeansException {
            return createBean(beanName, mbd, args);
        }
    });
    bean = getObjectForBeanInstance(sharedInstance, name, beanName, mbd);
}
```

### getSingleton 方法

#### 是否存在

首先会检测是否已经存在，如果存在，直接返回：

```java
synchronized (this.singletonObjects) {
    Object singletonObject = this.singletonObjects.get(beanName);
}
```

所有的单例 bean 都保存在这样的数据结构中：`ConcurrentHashMap<String, Object>`。

#### bean 创建

源码位于 AbstractAutowireCapableBeanFactory.createBean，主要分为几个部分：

##### lookup-method检测

此部分用于检测 lookup-method 标签配置的方法是否存在：

```java
RootBeanDefinition mbdToUse = mbd;
mbdToUse.prepareMethodOverrides();
```

prepareMethodOverrides：

```java
public void prepareMethodOverrides() throws BeanDefinitionValidationException {
    // Check that lookup methods exists.
    MethodOverrides methodOverrides = getMethodOverrides();
    if (!methodOverrides.isEmpty()) {
        Set<MethodOverride> overrides = methodOverrides.getOverrides();
        synchronized (overrides) {
            for (MethodOverride mo : overrides) {
                prepareMethodOverride(mo);
            }
        }
    }
}
```

prepareMethodOverride：

```java
protected void prepareMethodOverride(MethodOverride mo)  {
    int count = ClassUtils.getMethodCountForName(getBeanClass(), mo.getMethodName());
    if (count == 0) {
        throw new BeanDefinitionValidationException(
                "Invalid method override: no method with name '" + mo.getMethodName() +
                "' on class [" + getBeanClassName() + "]");
    } else if (count == 1) {
        // Mark override as not overloaded, to avoid the overhead of arg type checking.
        mo.setOverloaded(false);
    }
}
```

##### InstantiationAwareBeanPostProcessor 触发

在这里触发的是其 postProcessBeforeInitialization 和 postProcessAfterInstantiation 方法。

```java
Object bean = resolveBeforeInstantiation(beanName, mbdToUse);
if (bean != null) {
    return bean;
}
Object beanInstance = doCreateBean(beanName, mbdToUse, args);
return beanInstance;
```

继续：

```java
protected Object resolveBeforeInstantiation(String beanName, RootBeanDefinition mbd) {
    Object bean = null;
    if (!Boolean.FALSE.equals(mbd.beforeInstantiationResolved)) {
        // Make sure bean class is actually resolved at this point.
        if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
            Class<?> targetType = determineTargetType(beanName, mbd);
            if (targetType != null) {
                bean = applyBeanPostProcessorsBeforeInstantiation(targetType, beanName);
                if (bean != null) {
                    bean = applyBeanPostProcessorsAfterInitialization(bean, beanName);
                }
            }
        }
        mbd.beforeInstantiationResolved = (bean != null);
    }
    return bean;
}
```

从这里可以看出，**如果 InstantiationAwareBeanPostProcessor 返回的不是空，那么将不会继续执行剩下的 Spring 初始化流程，此接口用于初始化自定义的 bean，主要是在 Spring 内部使用**。

##### doCreateBean

同样分为几部分。

###### 创建（createBeanInstance）

关键代码：

```java
BeanWrapper instanceWrapper = null;
if (instanceWrapper == null) {
    instanceWrapper = createBeanInstance(beanName, mbd, args);
}
```

createBeanInstance 的创建过程又分为以下几种情况：

- 工厂 bean：

  调用 instantiateUsingFactoryMethod 方法：

  ```java
  protected BeanWrapper instantiateUsingFactoryMethod(
    String beanName, RootBeanDefinition mbd, Object[] explicitArgs) {
    return new ConstructorResolver(this).instantiateUsingFactoryMethod(beanName, mbd, explicitArgs);
  }
  ```

  注意，此处的工厂 bean 指的是配置了 factory-bean/factory-method 属性的 bean，不是实现了 FacrotyBean 接口的 bean。如果没有配置 factory-bean 属性，那么 factory-method 指向的方法必须是静态的。此方法主要做了这么几件事：

  - 初始化一个 BeanWrapperImpl 对象。

  - 根据设置的参数列表使用反射的方法寻找相应的方法对象。

  - InstantiationStrategy：

    bean 的初始化在此处又抽成了策略模式，类图：

    ![InstantiationStrategy类图](images/InstantiationStrategy.jpg)

    instantiateUsingFactoryMethod 部分源码：

    ```java
    beanInstance = this.beanFactory.getInstantiationStrategy().instantiate(
        mbd, beanName, this.beanFactory, factoryBean, factoryMethodToUse, argsToUse);
    ```

    getInstantiationStrategy 返回的是 CglibSubclassingInstantiationStrategy 对象。此处 instantiate 实现也很简单，就是调用工厂方法的 Method 对象反射调用其 invoke 即可得到对象，SimpleInstantiationStrategy：

    instantiate 核心源码：

    ```java
    @Override
    public Object instantiate(RootBeanDefinition bd, String beanName, BeanFactory owner,
        Object factoryBean, final Method factoryMethod, Object... args) {
        return factoryMethod.invoke(factoryBean, args);
    }
    ```

- 构造器自动装配

  createBeanInstance 部分源码：

  ```java
  // Need to determine the constructor...
  Constructor<?>[] ctors = determineConstructorsFromBeanPostProcessors(beanClass, beanName);
  if (ctors != null ||
    mbd.getResolvedAutowireMode() == RootBeanDefinition.AUTOWIRE_CONSTRUCTOR ||
      //配置了<constructor-arg>子元素
    mbd.hasConstructorArgumentValues() || !ObjectUtils.isEmpty(args))  {
    return autowireConstructor(beanName, mbd, ctors, args);
  }
  ```

  determineConstructorsFromBeanPostProcessors 源码：

  ```java
  protected Constructor<?>[] determineConstructorsFromBeanPostProcessors(Class<?> beanClass, String beanName) {
    if (beanClass != null && hasInstantiationAwareBeanPostProcessors()) {
        for (BeanPostProcessor bp : getBeanPostProcessors()) {
            if (bp instanceof SmartInstantiationAwareBeanPostProcessor) {
                SmartInstantiationAwareBeanPostProcessor ibp = 
                    (SmartInstantiationAwareBeanPostProcessor) bp;
                Constructor<?>[] ctors = ibp.determineCandidateConstructors(beanClass, beanName);
                if (ctors != null) {
                    return ctors;
                }
            }
        }
    }
    return null;
  }
  ```

  可见是由 SmartInstantiationAwareBeanPostProcessor 决定的，默认是没有配置这种东西的。

  之后就是判断 bean 的自动装配模式，可以通过如下方式配置：

  ```xml
  <bean id="student" class="base.Student" primary="true" autowire="default" />
  ```

  autowire 共有以下几种选项：

  - no：默认的，不进行自动装配。在这种情况下，只能通过 ref 方式引用其它 bean。
  - byName：根据 bean 里面属性的名字在 BeanFactory 中进行查找并装配。
  - byType：按类型。
  - constructor：以 byType 的方式查找 bean 的构造参数列表。
  - default：由父 bean 决定。

  参考: [Spring - bean 的 autowire 属性（自动装配）](http://www.cnblogs.com/ViviChan/p/4981539.html)

  autowireConstructor 调用的是 ConstructorResolver.autowireConstructor，此方法主要做了两件事：

  - 得到合适的构造器对象。

  - 根据构造器参数的类型去 BeanFactory 查找相应的 bean：

    入口方法在 ConstructorResolver.resolveAutowiredArgument：

    ```java
    protected Object resolveAutowiredArgument(
            MethodParameter param, String beanName, Set<String> autowiredBeanNames, 
            TypeConverter typeConverter) {
        return this.beanFactory.resolveDependency(
                new DependencyDescriptor(param, true), beanName, 
                autowiredBeanNames, typeConverter);
    }
    ```

  最终调用的还是 CglibSubclassingInstantiationStrategy.instantiate 方法，关键源码：

  ```java
  @Override
  public Object instantiate(RootBeanDefinition bd, String beanName, BeanFactory owner,
        final Constructor<?> ctor, Object... args) {
    if (bd.getMethodOverrides().isEmpty()) {
             //反射调用
        return BeanUtils.instantiateClass(ctor, args);
    } else {
        return instantiateWithMethodInjection(bd, beanName, owner, ctor, args);
    }
  }
  ```

  可以看出，如果配置了 lookup-method 标签，**得到的实际上是用 Cglib 生成的目标类的代理子类**。

  CglibSubclassingInstantiationStrategy.instantiateWithMethodInjection：

  ```java
  @Override
  protected Object instantiateWithMethodInjection(RootBeanDefinition bd, String beanName, BeanFactory 	owner,Constructor<?> ctor, Object... args) {
    // Must generate CGLIB subclass...
    return new CglibSubclassCreator(bd, owner).instantiate(ctor, args);
  }
  ```

- 默认构造器

  一行代码，很简单：

  ```java
  // No special handling: simply use no-arg constructor.
  return instantiateBean(beanName, mbd);
  ```

###### MergedBeanDefinitionPostProcessor

触发源码：

```java
synchronized (mbd.postProcessingLock) {
    if (!mbd.postProcessed) {
        applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
        mbd.postProcessed = true;
    }
}
```

此接口也是 Spring 内部使用的，不管它了。

###### 属性解析

入口方法：AbstractAutowireCapableBeanFactory.populateBean，它的作用是：根据 autowire 类型进行 autowire by name，by type 或者是直接进行设置，简略后的源码：

```java
protected void populateBean(String beanName, RootBeanDefinition mbd, BeanWrapper bw) {
    //所有<property>的值
    PropertyValues pvs = mbd.getPropertyValues();

    if (mbd.getResolvedAutowireMode() == RootBeanDefinition.AUTOWIRE_BY_NAME ||
            mbd.getResolvedAutowireMode() == RootBeanDefinition.AUTOWIRE_BY_TYPE) {
        MutablePropertyValues newPvs = new MutablePropertyValues(pvs);

        // Add property values based on autowire by name if applicable.
        if (mbd.getResolvedAutowireMode() == RootBeanDefinition.AUTOWIRE_BY_NAME) {
            autowireByName(beanName, mbd, bw, newPvs);
        }

        // Add property values based on autowire by type if applicable.
        if (mbd.getResolvedAutowireMode() == RootBeanDefinition.AUTOWIRE_BY_TYPE) {
            autowireByType(beanName, mbd, bw, newPvs);
        }

        pvs = newPvs;
    }
    //设值
    applyPropertyValues(beanName, mbd, bw, pvs);
}
```

autowireByName 源码：

```java
protected void autowireByName(
        String beanName, AbstractBeanDefinition mbd, BeanWrapper bw, MutablePropertyValues pvs) {
    //返回所有引用(ref="XXX")的bean名称
    String[] propertyNames = unsatisfiedNonSimpleProperties(mbd, bw);
    for (String propertyName : propertyNames) {
        if (containsBean(propertyName)) {
             //从BeanFactory获取
            Object bean = getBean(propertyName);
            pvs.add(propertyName, bean);
            registerDependentBean(propertyName, beanName);
        }
    }
}
```

autowireByType 也是同样的套路，所以可以得出结论：**autowireByName和autowireByType 方法只是先获取到引用的 bean，真正的设值是在 applyPropertyValues 中进行的。**

###### 属性设置

Spring 判断一个属性可不可以被设置（存不存在）是通过 java bean 的内省操作来完成的，也就是说，属性可以被设置的条件是**此属性拥有 public 的 setter 方法，并且注入时的属性名应该是 setter 的名字**。

###### 初始化

此处的初始化指的是 bean 已经构造完成，执行诸如调用其 init 方法的操作。相关源码：

```java
// Initialize the bean instance.
Object exposedObject = bean;
try {
    populateBean(beanName, mbd, instanceWrapper);
    if (exposedObject != null) {
        exposedObject = initializeBean(beanName, exposedObject, mbd);
    }
}
```

initializeBean：

```java
protected Object initializeBean(final String beanName, final Object bean, RootBeanDefinition mbd) {
    if (System.getSecurityManager() != null) {
        AccessController.doPrivileged(new PrivilegedAction<Object>() {
            @Override
            public Object run() {
                invokeAwareMethods(beanName, bean);
                return null;
            }
        }, getAccessControlContext());
    }
    else {
        invokeAwareMethods(beanName, bean);
    }

    Object wrappedBean = bean;
    if (mbd == null || !mbd.isSynthetic()) {
        wrappedBean = applyBeanPostProcessorsBeforeInitialization(wrappedBean, beanName);
    }

    invokeInitMethods(beanName, wrappedBean, mbd);

    if (mbd == null || !mbd.isSynthetic()) {
        wrappedBean = applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName);
    }
    return wrappedBean;
}
```

主要的操作步骤一目了然。

- Aware 方法触发：

  我们的 bean 有可能实现了一些 XXXAware 接口，此处就是负责调用它们：

  ```java
  private void invokeAwareMethods(final String beanName, final Object bean) {
    if (bean instanceof Aware) {
        if (bean instanceof BeanNameAware) {
            ((BeanNameAware) bean).setBeanName(beanName);
        }
        if (bean instanceof BeanClassLoaderAware) {
            ((BeanClassLoaderAware) bean).setBeanClassLoader(getBeanClassLoader());
        }
        if (bean instanceof BeanFactoryAware) {
            ((BeanFactoryAware) bean).setBeanFactory(AbstractAutowireCapableBeanFactory.this);
        }
    }
  }
  ```

- BeanPostProcessor 触发，没什么好说的

- 调用 init 方法：

  在 XML 配置中，bean 可以有一个 init-method 属性来指定初始化时调用的方法。从原理来说，其实就是一个反射调用。不过注意这里有一个 InitializingBean 的概念。

  此接口只有一个方法：

  ```java
  void afterPropertiesSet() throws Exception;
  ```

  如果我们的 bean 实现了此接口，那么此方法会首先被调用。此接口的意义在于：当此 bean 的所有属性都被设置（注入）后，给 bean 一个利用现有属性重新组织或是检查属性的机会。感觉和 init 方法有些冲突，不过此接口在 Spring 被广泛使用。

### getObjectForBeanInstance

位于 AbstractBeanFactory，此方法的目的在于如果 bean 是 FactoryBean，那么返回其工厂方法创建的 bean，而不是自身。

## Prototype 初始化

AbstractBeanFactory.doGetBean 相关源码：

```java
else if (mbd.isPrototype()) {
    // It's a prototype -> create a new instance.
    Object prototypeInstance = null;
    try {
        beforePrototypeCreation(beanName);
        prototypeInstance = createBean(beanName, mbd, args);
    }
    finally {
        afterPrototypeCreation(beanName);
    }
    bean = getObjectForBeanInstance(prototypeInstance, name, beanName, mbd);
}
```

### beforePrototypeCreation

此方法用于确保在同一时刻只能有一个此 bean 在初始化。

### createBean

和单例的是一样的，不在赘述。

### afterPrototypeCreation

和 beforePrototypeCreation 对应的。

### 总结

可以看出，初始化其实和单例是一样的，只不过单例多了一个是否已经存在的检查。

## 其它 Scope 初始化

其它就指的是 request、session。此部分源码：

```java
else {
    String scopeName = mbd.getScope();
    final Scope scope = this.scopes.get(scopeName);
    if (scope == null) {
        throw new IllegalStateException("No Scope registered for scope name '" + scopeName + "'");
    }
    Object scopedInstance = scope.get(beanName, new ObjectFactory<Object>() {
        @Override
        public Object getObject() throws BeansException {
            beforePrototypeCreation(beanName);
            try {
                return createBean(beanName, mbd, args);
            }
            finally {
                afterPrototypeCreation(beanName);
            }
        }
    });
    bean = getObjectForBeanInstance(scopedInstance, name, beanName, mbd);
}
```

scopes 是一个 LinkedHashMap<String, Scope>，可以调用 ConfigurableBeanFactory 定义的 registerScope 方法注册其值。

Scope 接口继承体系：

![Scope继承体系](images/Scope.jpg)

根据 socpe.get 的注释，此方法如果找到了叫做 beanName的bean，那么返回，如果没有，将调用 ObjectFactory 创建之。Scope 的实现参考类图。







