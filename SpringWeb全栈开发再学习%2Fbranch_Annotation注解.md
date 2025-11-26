#### 1、Target

`java.lang.annotation.Target` 自身也是一个注解，它只有一个数组属性，用于设定该注解的目标范围，比如说可以作用于类或者方法等。因为是数组，所以可以同时设定多个范围

具体可以作用的类型配置在 `java.lang.annotation.ElementType` 枚举类中，我们说几个常用的

- ElementType.TYPE

  > 可以作用于 类、接口类、枚举类上

- ElementType.FIELD

  > 可以作用于类的属性上

- ElementType.METHOD

  > 可以作用于类的方法上

- ElementType.PARAMETER

  > 可以作用于类的参数

如果想要同时作用于类和方法上，那么你就可以

```
@Target({ElementType.TYPE,ElementType.METHOD})
```

> 如果某个 Annotation 的 Target 设定为 METHOD ，那么你就只能在方法前面上面引用它，其他的地方都不行,其他 Target 值也类似这个规则

我们再看几个例子来区分一下，

##### 1.1 ElementType.TYPE

```
@Service
public class MessageServiceImpl implements MessageService{

    public String getMessage() {
         return "Hello World!";
    }

}
```

##### 1.2 ElementType.METHOD

```
public class MessageServiceImpl implements MessageService{

    @ResponseBody
    public String getMessage() {
         return "Hello World!";
    }

}
```

##### 1.3 ElementType.FIELD

```
public class MessageServiceImpl implements MessageService{

    @Autowired
    private WorkspaceService workspaceService;

}
```

##### 1.4 ElementType.PARAMETER

```
public class MessageServiceImpl implements MessageService{

    public String getMessage(@RequestParam("msg")String msg) {
         return "Hello "+msg;
    }

}
```

大家暂时只要关注语法就好了，具体的注解类的含义，我们后面会逐步学习到的

#### 2、Retention

`java.lang.annotation.Retention` 自身也是一个注解，它用于声明该注解的生命周期，简单的来说就是在 Java 编译、运行的哪个环节有效，它的值定义在`java.lang.annotation.RetentionPolicy`枚举类中，有三个值可以选择

1.SOURCE: 也就是说是纯注释作用 2.CLASS: 也就是在编译阶段是有效的 3.RUNTIME: 在运行时有效

```
@Retention(RetentionPolicy.RUNTIME)
```

这个代码表示的就是在运行期间有效

> 如果是我们自己定义的 Annotation ，一般我们都会设置成 `RUNTIME`

#### 3、Documented

`java.lang.annotation.Documented` 自身也是一个注解，它的作用是将注解中的元素包含到 JavaDoc 文档中，一般情况下，都会添加这个注解的。

#### 4、@interface

`@interface`就是声明当前的 Java 类型是 Annotation，固定语法，就是这样写就好

#### 5、Annotation 属性

```
String value() default "";
```

Annotation 的属性有点像类的属性一样，它约定了属性的类型(这个类型是基础类型：String、boolean、int、long)，和属性名称（默认名称是 value ，在引用的时候可以省略），default 代表的是默认值。

有了这个属性，我们就可以正式的引用一个 Annotation 啦，比如

```
import org.springframework.stereotype.Service;

@Service
public class Demo {

}
```

注意，Annotation 也是 Java 类，所以一样需要 import 的

上面的`@Service` 也可以写成

```
import org.springframework.stereotype.Service;

@Service(value="Demo")
public class Demo {

}
```

因为我们说过 value 是默认属性名称是可以缩写的，所以上面的代码等同于

```
import org.springframework.stereotype.Service;

@Service("Demo")
public class Demo {

}
```

> Annotation 属性是可以有多个的，比如下面的一个注解类

```
@Target(ElementType.PARAMETER)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface RequestParam {

    @AliasFor("name")
    String value() default "";


    @AliasFor("value")
    String name() default "";


    boolean required() default true;

    String defaultValue() default ValueConstants.DEFAULT_NONE;
}
```

在属性的代码上，我们看到`@AliasFor("name")`这个是别名的意思，就是说这个属性用这个别名也可以访问到，所以下面的代码是一样的意思

```
@RequestParam("key")
```

```
@RequestParam(value="key")
```

```
@RequestParam(name="key")
```

代码演示

具体的代码如下：

```java
package com.youkeda.service.impl;

import com.youkeda.service.MessageService;
import org.springframework.stereotype.Service;

@Service
public class MessageServiceImpl implements MessageService{

    public String getMessage() {
         return "Hello World!";
    }

}
```