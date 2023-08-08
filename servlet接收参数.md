## sevlet + mvc 两种方式的收发数据探索与实践



2020年04月02日  作者: dulred  [文章链接](https://tech.meituan.com/2020/04/02/java-pooling-pratice-in-meituan.html)  15187字 31分钟阅读



> 本文详细探讨了HttpServletRequest，HttpServletResponse的接收发送
>

- 提交时机
- 请求方式
- 请求地址
- 发送的数据
- .......



#### 一、前言

##### 1.1 HttpServletRequest获取参数方法

- String getParameter(String name)：通过指定名称获取参数值；
- String[] getParameterValues(String name)：通过指定名称获取参数值数组，有可能一个名字对应多个值，例如表单中的多个复选框使用相同的name时；
- Enumeration getParameterNames()：获取所有参数的名字；
- Map getParameterMap()：获取所有参数对应的Map，其中key为参数名，value为参数值。

##### 1.2 传递参数的方式

> GET:

- 地址栏中直接给出参数：http://localhost/param/ParamServlet?p1=v1&p2=v2；
- 超链接中给出参数：<a href=” http://localhost/param/ParamServlet?p1=v1&p2=v2”>???</a>
- 表单中给出参数：<form method="GET" action="ParamServlet">…</form>
- Ajax暂不介绍

> POST

- 表单中给出参数：<form method="POST" action="ParamServlet">…</form>
- Ajax暂不介绍



#### 二、前端数据的接收和响应

##### 2.1.



#### 三、表单在业务中的实践







####  四、参考资料

- [1] [HttpServletRequest参数获取，HttpServletRequest详解](https://blog.csdn.net/stone_bk/article/details/112415575)



#### 作者简介

- dulred 

#### 合作伙伴

........
				