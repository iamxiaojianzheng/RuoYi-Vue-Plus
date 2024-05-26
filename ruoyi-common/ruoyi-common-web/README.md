## `ruoyi-common-web`学习笔记

### 实现思路

1. 基于`@ConfigurationProperties`注解实现配置类
2. 基于`@AutoConfiguration`和`@EnableConfigurationProperties`完成功能对象的实例化注入
3. 配置`META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`

### Captcha 验证码

- 基于cn.hutool.captcha.CaptchaUtil工具类完成

### XSS 过滤

- 自定义 `Filter`
- 自定义 `HttpServletRequestWrapper`，并重写`getParameterValues`和`getInputStream`方法
- 读取请求数据，通过`cn.hutool.http.HtmlUtil.cleanHtmlTag` 工具类处理异常字符

### I18n

### Cross 跨域配置

- CorsConfiguration
- UrlBasedCorsConfigurationSource
- CorsFilter

### Undertow 配置

- 自定义WebSocketDeploymentInfo配置
- 设置DeploymentInfo使用虚拟线程

### 构建可重复读InputStream的Request

- 缓存请求输入流到类字段body中
- 重写getInputStream和getReader方法，重复从body读取数据

### 全局异常处理

- `@RestControllerAdvice`
- `@ExceptionHandler`

### web接口调用时间统计

- `ThreadLocal`，一个请求一个`StopWatch`
- `StopWatch`，完成计时功能

