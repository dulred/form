## 前端Form表单元素的探索与实践



2020年04月02日  作者: dulred  [文章链接](https://tech.meituan.com/2020/04/02/java-pooling-pratice-in-meituan.html)  15187字 31分钟阅读



> 本文详细探讨了前端的接收发送 等一系列知识点
>

- 提交时机
- 请求方式
- 请求地址
- 发送的数据
- .......







#### 一、前言

##### 1.1 前端交互数据的媒介是什么









##### 1.2 表单存在的必要性是什么







#### 二、表单请求数据

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

```
1. get获取的数据会附在url后（就是把数据放置在http协议的头中），以?分割url和传输数据，参数之间以&相连。post把提交的数据则放置在http包的包体中。
2. get方式提交的数据最多只能是1024字节。而post没有限制，可以传输较大量的数据
3. post的安全性比get的安全性要高。例如：通过get提交数据，用户名和密码将明文出现在url上，因为登录界面有可能被浏览器缓存，其他人查看浏览器的历史记录就可以拿到你的账户和密码了。
另外，get是向服务器发送索取数据的一种请求，post是向服务器提交数据的一种请求。
```

​    <!-- get -->
​    <form action="/server.php" method="get">
​        <p>账号：<input type="text" name="loginid"></p>
​        <p>密码：<input type="password" name="loginpwd"></p>
​        <p><button type="submit">提交</button></p>
​    </form>
​    <!-- post -->
​    <form action="/server.php" method="post">
​        <p>账号：<input type="text" name="loginid"></p>
​        <p>密码：<input type="password" name="loginpwd"></p>
​        <p><button type="submit">提交</button></p>
​    </form>

##### 2.3 请求数据

​    <!-- 多选框 -->
​    <form method="post" action="test.php">
​        <p>
​            爱好：  <label><input type="checkox" name="like" value="football">足球</label>
​            <label><input type="checkox" name="like" value="basketball">篮球</label>
​            <label><input type="checkox" name="like" value="music">音乐</label>
​            <label><input type="checkox" name="like" value="movie">电影</label>
​            <label><input type="checkox" name="like" value="read">阅读</label>
​        </p>
​        <p><input type="submit" value="提交"></p></form>
 <!-- 则向服务器发送的消息体为：

like=football&like=music&like=read

仔细看上面发送的内容，你会发现出现了重复的键，http协议允许在请求时出现重复的键，无论是用哪种语言作为服务端，也都可以处理请求数据中的重复键，完全不必担心。

特别注意，发送到服务器的是选中项的value值，而不是后面的文本 -->

##### 2.4 常用的请求类型

**2.4.1常用的表单标签上传**

- type="text"：
   用于输入文本。
   <input name="username" type="text" placeholder="用户名" maxlength=10 />
   placeholder属性（可选）展示的是输入框里的提示，maxlength（可选）限制最大输入长度；
- type="password"：
   用于输入密码，输入的内容显示为星号。
   <input name="password" type="password" placeholder="密码" />
- type="radio"：
   单选圆圈按钮。注意：name要相同才能实现单选，value要有值。
   <input type="radio" name="sex" value="male" /> 男
   <input type="radio" name="sex" value="female" /> 女
- type="checkbox"：
   复选框。加checked属性会默认选上。提交时，如果选中（如bike），则bike=on
   <input type="checkbox" name="bike"  checked/>自行车
   <input type="checkbox" name="car" />汽车
- type="hidden"：
   隐藏域，用户看不到，用于暂存数据。或者安全性校验
   <input name="url_delete" type="hidden" value="/delete.php" />
   <input name="csrf_token" type="hidden" value="a23dafd23444" />

**2.4.1.1 input里，name 的作用**
 name给表单命名，告诉服务器提交的是哪个表单的数据。
 name属性必须有，否则表单数据无法提交到服务器。

**2.4.1.2 type=hidden隐藏域的作用**

- 隐藏域在页面中对于用户是不可见的，在表单中插入隐藏域的目的在于收集或发送信息，以利于被处理表单的程序所使用。浏览者单击发送按钮发送表单的时候，隐藏域的信息也被一起发送到服务器。

- 有些时候我们要给用户一信息，让他在提交表单时提交上来以确定用户身份，如sessionkey，等等．当然这些东西也能用cookie实现，但使用隐藏域就简单的多了．而且不会有浏览器不支持，用户禁用cookie的烦恼。

-  有些时候一个form里有多个提交按钮，怎样使程序能够分清楚到底用户是按那一个按钮提交上来的呢？我们就可以写一个隐藏域，然后在每一个按钮处加上`onclick=”document.form.command.value=”xx”“`然后我们接到数据后先检查command的值就会知道用户是按的那个按钮提交上来的。

-  有时候一个网页中有多个form，我们知道多个form是不能同时提交的，但有时这些form确实相互作用，我们就可以在form中添加隐藏域来使它们联系起来。

- javascript不支持全局变量，但有时我们必须用全局变量，我们就可以把值先存在隐藏域里，它的值就不会丢失了。

- 还有个例子，比如按一个按钮弹出四个小窗口，当点击其中的一个小窗口时其他三个自动关闭．可是IE不支持小窗口相互调用，所以只有在父窗口写个隐藏域，当小窗口看到那个隐藏域的值是close时就自己关掉。

##### 2.4.1.3 表单的高级用法

- 隐藏域 **<input type="hidden" name="" value="" />**

- 只读和隐藏  特点1：readonly代表不可编辑  特点2：disabled代表置灰效果且不可编辑

  <input type="text" value="" readonly="readonly" />

  <input type="text" value="" readonly="disabled" />

- 表单元素的标注  特点1：在input标签中加入id=“XX”  特点2：在label标签中加入for=”XX”

  **<label for="XX">   </label><input type="radio" name="" value="" id="XX">**



**2.4.2 常见文件类型上传**



**2.4.2 常见图片类型上传**



**2.4.2 常见视频类型上传**



**2.4.2 常见音频类型上传**











#### 三、接收响应数据







#### 四、表单验证(请求和接收的验证)







#### 五、常见业务实践








####  六、参考资料

- [1] [Form表单详解](https://zhuanlan.zhihu.com/p/73323143)



#### 作者简介

- dulred 

#### 合作伙伴

........
				
