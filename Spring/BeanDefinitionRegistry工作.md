Spring BeanDefinitionRegistry
===

`Spring`中，对于`BeanDefinitionRegistry`创建`Bean`在大致过程如下：
1. 通过读取`xml`或`javaConfig`中的`Bean`信息，来创建配置`BeanDefinition`,`BeanDefinition`中有这个`Bean`的所有信息，包括了`Bean`实例的引用，其中的关键概信息如下：
  ``` java
  // Bean实例
  private volatile Object beanClass;
  //Bean中的属性，可以是另一个Bean
  private MutablePropertyValues propertyValues;
  ```
可像如下设置属性：

  ``` java
  MutablePropertyValues propertyValues = new MutablePropertyValues();
  propertyValues.add("username", "tom");
  propertyValues.add("password", "123");
  beanDefinition.setPropertyValues(propertyValues);
  ```

2. 当`BeanDefinition`设置完成以后，通过`BeanDefinitionRegistry`来注册`Bean`,如下：
  ``` java
  //注册Bean
  registry.registerBeanDefinition("user",beanDefinition);
  ```
  其中第一个参数是`Bean`名称，第二个是`Bean`的定义信息

3. 通过上面的准备后，最后的目的是获取到注入的`Bean`,由于我们注册`Bean`是使用的`BeanDefinitionRegistry`接口，其中`DefaultListableBeanFactory`是他的实现，通过实例化`DefaultListableBeanFactory`来注册`Bean`，由于`DefaultListableBeanFactory`同时也继承了`AbstractAutowireCapableBeanFactory`,而`AbstractAutowireCapableBeanFactory`又继承了`AbstractBeanFactory`，可以通过强转把`BeanDefinitionRegistry`转化为`BeanFactory`，因为`AbstractBeanFactory`是`BeanFactory`的实现，通过调用`getBean()`方法，`AbstractBeanFactory`中的`getBean()`去创建出`Bean`最终返回`Bean`

完整代码如下：
``` java
BeanDefinitionRegistry registry = new DefaultListableBeanFactory();
AbstractBeanDefinition beanDefinition = new RootBeanDefinition(User.class);
MutablePropertyValues propertyValues = new MutablePropertyValues();
propertyValues.add("username", "tom");
propertyValues.add("password", "123");
beanDefinition.setPropertyValues(propertyValues);
registry.registerBeanDefinition("user",beanDefinition);
BeanFactory beanFactory = (BeanFactory) registry;
User user  = (User) beanFactory.getBean("user");
```
