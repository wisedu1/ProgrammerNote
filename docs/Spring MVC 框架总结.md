---
title: Spring MVC 框架总结
top: 1
date: 2021-04-27 19:26:24
tags: Spring MVC
categories: 框架
---

# Spring MVC 框架总结

## 写在前面

最近开始接触 Spring MVC，但是零零散散，没有在大脑里形成系统的知识结构体系，于是在此进行了梳理。

## 什么是 MVC

Spring MVC 是 Spring 框架的一个模块，Spring MVC 和 Spring 无需通过中间整合层进行整合。

Spring MVC 是一个基于 MVC 的 web 框架。

**MVC** 模式是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：

* 控制器(**C**ontroller)——负责转发请求，对请求进行处理。
* 视图 (**V**iew)——界面设计人员进行图形界面设计。
* 模型 (**M**odel)——程序员编写程序应有的功能、数据库专家进行数据管理和数据库设计。

所以，MVC 模式将程序划分了三个组件，**模型 (Model)** 用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法。**视图 (View)** 负责展示数据，**控制器 (Contoller)** 处理事件并作出响应（事件包括用户的行为，比如请求）和数据 Model 上的改变。

* 用户发起 request 请求至控制器 (Controller)，控制器接收用户请求的数据，委托给模型进行处理
* 控制器通过模型处理数据并得到处理结果，模型通常是指业务逻辑
* 模型处理结果返回给控制器
* 控制器将模型数据在视图中展示，web 中模型无法将数据直接在视图上显示，需要通过控制器完成
* 控制器将视图 response 响应给用户，通过视图展示给用户要的数据或处理结果

## Spring MVC 核心架构

![](https://gitee.com/wisedu1/MyImage/raw/master/imgs/%E6%A1%86%E6%9E%B6/SpringMVC%20%E6%A0%B8%E5%BF%83%E6%9E%B6%E6%9E%84%E5%9B%BE.jpg)

1. 用户发起请求到前端控制器 (DispatcherServlet)
2. 前端控制器请求处理器映射器 HandlerMapping 查找 Handler，可以根据 xml 配置、注解进行查找
3. 处理器映射器 HandlerMapping 向前端控制器返回 Handler
4. 前端控制器调用处理器适配器 HandlerAdapter 去执行 Handler
5. 处理器适配器去执行 Handler
6. 处理器适配器向前端控制器返回 ModelAndView，它是 Spirng MVC 框架的一个底层对象，包括 Model 和 View
7. 前端控制器请求视图解析器 ViewResolver 去进行视图解析，根据逻辑视图名解析成真正的视图
8. 视图解析器 向前端控制器返回 View
9. 前端控制器进行视图渲染，视图渲染将模型数据（在 ModelAndView 对象中）填充到 request 域
10. 前端控制器向用户响应结果

通常，一个项目是由 Spring + SpringMVC + MyBatis 三大框架整合的 SSM 框架完成。

## Spring MVC 常用注解

1. @Controller

   负责注册一个 bean 到 Spring Context中。

2. @RequstMapping

   注解为控制器指定可以处理那些 URL 请求。

3. @RequstBody

   该注解用于读取 `Request` 请求的 body 部分数据，使用系统默认配置的 `HttpMessageConverter` 进行解析，然后把响应的数据绑定到要返回的对象上，再把 `HttpMessageConverter` 返回的对象数据绑定到 controller 中方法的参数上。

4. @ResponseBody

   该注解用于将 controller 的方法返回的对象通过适当的 `HttpMessageConverter` 转换成为指定格式后，写入到 `Response` 对象的 body 数据区。

5. @ModelAttribute

   在方法定义上使用 @ModelAttribute 注解：Spring MVC 在调用目标处理方法前，会先逐个调用在方法级上标注了 @ModelAttribute 的方法。

   在方法的入参前使用 @ModelAttribute 注解：可以从隐含对象中获取隐含的模型数据中获取对象，再将请求参数绑定到对象中，再传入入参将方法入参对象添加到模型中。

6. @RequstParam

   在处理方法入参处使用 @RequestParam 可以把请求参数传递给请求方法。

7. @PathVariable

   绑定 URL 占位符到入参。

8. @ExceptionHandler

   注解到方法上，出现异常时会执行该方法。

9. @ControllerAdvice

   使一个 Controller 成为全局的异常处理类，类中使用 @ExceptionHandler 注解的方法可以处理所有 Controller 发生的异常。