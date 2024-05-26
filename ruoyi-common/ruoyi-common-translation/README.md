## `ruoyi-common-translation`学习笔记

### 设计思路

通过`@JacksonAnnotationsInside`、`@JsonSerialize`两个注解组合一个新的Jackson序列化注解，这里是整个功能的实现上的重点。

Jackson在序列化过程中，通过检测`@JsonSerialize`注解并判断其中设置的属性，如`using`。来决定是否将序列化工作交给赋值给`using`属性的接口。

该接口需要继承`@JsonSerializer`，并重写`serialize`方法。

实现`ContextualSerializer`，并重写`createContextual`方法为可选操作，用途是判断被序列化的字段是否包含`@Translation`注解，并将注解对象回填给`TranslationHandler`的对象属性`translation`。

然后在`serialize`方法中获取`@Translation`注解的相关属性值，完成序列化功能。

其次需要关注的点是`META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`文件

它的作用是将`TranslationInterface`接口的实现类注入到Ioc容器中，然后`TranslationConfig.list`字段就可以获取到这些实现类。

再添加到`TranslationHandler.TRANSLATION_MAPPER`。

`TranslationBeanSerializerModifier`的功能是单一独立的，属于可选操作。

### 扩展新的翻译功能

1. 实现`TranslationInterface`接口并添加`@@TranslationType`注解
2. 在`translation`方法中完成翻译功能
3. 将实现类添加到`META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`文件中
