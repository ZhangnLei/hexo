---
title: 后端开发 - SpringBoot项目名中如何处理service层的异常？
date: 2020-05-04 11:07:19
tags: 
- springboot
- 异常处理
---



# 后端开发 - SpringBoot项目名中如何处理service层的异常？



[toc]

先说自己犯的错误：

```java
		try {
      /**
       * 非常一长串逻辑代码
       **/
			...
      ...
		} catch (Exception e) {
			logger.error(">>>className.methodsName,异常原因：{}", e.getMessage());
			return CommonMsgUtils.getErrorCommonMsg(commonMsg, ErrorCodeEnum.DATABASE_EXCEPTION);
		}
```



阿里巴巴编码规范 第二章 - 异常处理：

> /3. 【强制】catch 时请分清稳定代码和非稳定代码，稳定代码指的是无论如何不会出错的代码。 对于非稳定代码的 catch 尽可能进行区分异常类型，再做对应的异常处理。 说明:对大段代码进行 try-catch，使程序无法根据不同的异常做出正确的应激反应，也不利 于定位问题，这是一种不负责任的表现。 正例:用户注册的场景中，如果用户输入非法字符，或用户名称已存在，或用户输入密码过于 简单，在程序上作出分门别类的判断，并提示给用户。





> /4. 【强制】捕获异常是为了处理它，不要捕获了却什么都不处理而抛弃之，如果不想处理它，请 将该异常抛给它的调用者。最外层的业务使用者，必须处理异常，将其转化为用户可以理解的 内容。



> /5. 【强制】有 try 块放到了事务代码中，catch 异常后，如果需要回滚事务，一定要注意手动回 滚事务。





> /6)  级联调用obj.getA().getB().getC();一连串调用，易产生NPE。
>
> 正例:使用 JDK8 的 Optional 类来防止 NPE 问题。



日志：

> /4. 【强制】对 trace/debug/info 级别的日志输出，必须使用条件输出形式或者使用占位符的方 式。
>
> ```java
> //说明(反例):
> logger.debug("Processing trade with id: " + id + " and symbol: " + symbol);
> ```
>
>  如果日志级别是 warn，上述日志不会打印，但是会执行字符串拼接操作，如果 symbol 是对象， 会执行 toString()方法，浪费了系统资源，执行了上述操作，最终日志却没有打印。 
>
> 建设采用如下方式:
>
> ```java
> // 正例1:(条件)
> if (logger.isDebugEnabled()) {
> 	logger.debug("Processing trade with id: " + id + " and symbol: " + symbol);
> }
> ```
>
> ```java
> // 正例2:(占位符)
> logger.debug("Processing trade with id: {} and symbol : {} ", id, symbol);
> ```







参考：

[https://www.cnblogs.com/gujiazhouwang/p/12028713.html](https://www.cnblogs.com/gujiazhouwang/p/12028713.html)