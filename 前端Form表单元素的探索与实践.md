## 前端Form表单元素的探索与实践



2020年04月02日  作者: dulred  [文章链接](https://tech.meituan.com/2020/04/02/java-pooling-pratice-in-meituan.html)  15187字 31分钟阅读



> 本文详细探讨了前端的接收发送，以及后端java如何接收发送的数据处理和传输
>
> 等一系列知识点

- 提交时机
- 请求方式
- 请求地址
- 发送的数据
- .......



#### 一、前言

##### 1.1 前端交互数据的媒介是什么



##### 1.2 表单存在的必要性是什么





#### 二、表单的设计和实现

##### 2.1 提交时机

>  点击了表单中的提交按钮

   <form action="">
        <p><input type="submit" value="提交1"></p>
        <p><button type="submit">提交2</button></p>
        <p><input type="image" src="" style="width: 100px; height: 100px;"></p></form></body></html>
​    </form>

>  在js中调用了表单对象的submit方法



  <!-- js提交 -->
    <form id="f1">
        <p>账号：<input type="text" name="loginid"></p>
        <p>密码：<input type="password" name="loginpwd"></p>
        <!--下面是一个普通按钮-->
        <p><button onclick="jssubmit()">提交</button></p>
    </form>
    <script type="text/javascript">
        function jssubmit() {        //获取form表单的dom对象
            var formdom = document.getElementById('f1');  //调用对象的submit方法
            formdom.submit();
        }
    </script>



##### 2.2 触发onsubmit事件

<!-- 表单提交 行为触发，状态改变，必然可以有事件触发  触发onsubmit事件-->
<form id="f2" onsubmit="return vali()">
    <p>账号：<input type="text" name="loginid2"></p>
    <p>密码：<input type="password" name="loginpwd2"></p>
    <p><button type="submit">提交</button></p></form>
    <script type="text/javascript">
    function vali() {        //获取账号文本框
        var txtLoginId = document.getElementsByName("loginid2")[0];        //获取密码文本框
        var txtLoginPwd = document.getElementsByName("loginpwd2")[0];      
          if(txtLoginId.value == ""){
            alert("请填写账号");            return false;//返回false，阻止表单提交
        }        if(txtLoginPwd.value == ""){
            alert("请填写密码");            return false;//返回false，阻止表单提交
        }
    }</script>





##### 2.3 请求方式

​    <!-- 请求方式 -->
​    <!-- 使用form标签的method属性，可以控制form表单的提交方式，该属性可以省略，若省略，默认的提交方式是get -->

​    <!-- get -->
    <form action="/server.php" method="get">
        <p>账号：<input type="text" name="loginid"></p>
        <p>密码：<input type="password" name="loginpwd"></p>
        <p><button type="submit">提交</button></p>
    </form>
​    <!-- post -->
    <form action="/server.php" method="post">
        <p>账号：<input type="text" name="loginid"></p>
        <p>密码：<input type="password" name="loginpwd"></p>
        <p><button type="submit">提交</button></p>
    </form>

##### 2.3 请求数据


​    <!-- 多选框 -->
    <form method="post" action="test.php">
        <p>
            爱好：  <label><input type="checkox" name="like" value="football">足球</label>
            <label><input type="checkox" name="like" value="basketball">篮球</label>
            <label><input type="checkox" name="like" value="music">音乐</label>
            <label><input type="checkox" name="like" value="movie">电影</label>
            <label><input type="checkox" name="like" value="read">阅读</label>
        </p>
        <p><input type="submit" value="提交"></p></form>
 <!-- 则向服务器发送的消息体为：

like=football&like=music&like=read

仔细看上面发送的内容，你会发现出现了重复的键，http协议允许在请求时出现重复的键，无论是用哪种语言作为服务端，也都可以处理请求数据中的重复键，完全不必担心。

特别注意，发送到服务器的是选中项的value值，而不是后面的文本 -->



#### 三、表单在业务中的实践







####  四、参考资料

- [1] [Form表单详解](https://zhuanlan.zhihu.com/p/73323143)



#### 作者简介

- dulred 

#### 合作伙伴

........
				
