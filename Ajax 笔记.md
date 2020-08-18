## Ajax 笔记

#### 第一天

------

#### 1.1 Ajax是什么

```
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。

AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。
```

#### 1.2 使用步骤  

```js
// Ajax的使用依赖于XMLHttpRequest 对象 第一步先实例化
  var xhr = new XMLHttpRequest()
  // 设置请求的地址 和 方法（先记住即可）
  xhr.open('get', 'https://autumnfish.cn/api/joke')
  // xhr.open('get', 'https：//autumnfish.cn/api/joke')
  // 注册回调函数，网络请求时有很多的限制导致数据返回的时间不可控
  // 触发时机 请求响应回来之后
  xhr.onload = function() {
    // responseText 就回保存服务器响应的数据 想象成 一个数据的包裹
    console.log(xhr.responseText)
  }
  // 发送请求 输入完url地址 点击 回车
  xhr.send()

//步骤说明
1. xhr对象即XMLHttpRequest，这是ajax里的核心对象，xhr取自每个单词首字母
2. 初始化请求，我们用open方法，参数1现在就写死get，他叫做请求方法，后面再解释是什么意思，参数2代表你要请求的服务器路径（网络上那么多资源，你得给个路径告诉它找哪个对不？）
3. 发送请求，字面意思
4. 我们发请求就是为了拿到服务器给我们的结果，因此这一步就是做这个事

```

#### 1.3响应数据格式

##### 1.3.1简介

服务器返回的数据不一定是非常简单的字符串，比如在查询多日天气预报时，这时获取的数据就比较多，思考，如果是你，你希望返回什么格式的数据呢？希望是一大段拼接到一起的字符串还是一个JS数组或对象呢？

答案肯定是数组或对象，因为数组或对象操作起来更加方便。

但是不同语言之间的数组和对象语法又不同，所以服务器直接返回对应语言的数组或对象是不行的。

语言设计人员早已意识到这个问题，所以专门设计了两种数据表示格式，他们分别是`JSON`和`XML`。在服务器和浏览器之间传输数据的时候，需要先把数据转换成双方都能够识别的格式，即`JSON`和`XML`。这就犹如中国人和其他国家人交流时需要找个翻译一样。

##### 1.3.2 JSON

JSON(JavaScript Object Notation : JS对象表示法)  是一种通过普通**字符串**描述数据的手段,用于表示有结构的数据.类似于编程语言中字面量的概念,语法上跟JavaScript的字面量非常相似.

---别看JSON长得像JS中的各种数据,但是JSON的本质是字符串--

```js

```

##### 1.3.3  JSON 数据转换

```js
//JSON 转 js
//转对象
let jsonobj = '{"name":"斑马" , "age":17, "genter" : true}' //数字类型和布尔类型不要双引号
//转数组
let jsonarr = '["番茄炒鸡蛋","番茄炒鸭蛋","番茄炒鹅蛋"]'
 // JSON.parse() 方法 将json字符串 转化成对象或者数组
    // 语法 : JSON.parse(text[, reviver])
    // text:必需， 一个有效的 JSON 字符串
    // reviver: 可选，一个转换结果的函数， 将为对象的每个成员调用此函数
console.log(JSON.parse(jsonobj)) // 得到一个对象
console.log(JSON.parse(jsonarr)) // 得到一个数组

//js 转 JSON
let jsobj = {'name':'董小姐','age':17}
JSON.stringify() //js对象转换JSON格式
console.log(JSON.stringify(jsobj))
```

### 第二天

------

#### 2.1 XML 格式 (了解)

```js
XML是什么?
XML 被设计用来传输和存储数据
HTML 被设计用来显示数据

怎么看是不是XML格式?
<?xml version="1.0" encoding="UTF-8"?> 前缀 

//解析方法
XML格式的数据  不是JSON  不能用 JSON.parse()
jQuery 提供了解析方法
$('选择器',内容) 在内容中查找
console.log($('city', xhr.responseText))
console.log($('city', xhr.responseText).text())
console.log($('fengxiang', xhr.responseText).text())

// 兼容性问题
console.log(xhr.responseXML)
```

#### 2.2 art-template   模板

```js
是什么? -- art-template 是一个简约、超快的模板引擎。artTemplate 是新一代 javascript 模板引擎，它采用预编译方式让性能有了质的飞跃，并且充分利用 javascript 引擎特性，使得其性能无论在前端还是后端都有极其出色的表现。

用法: 
1.导入模板js文件
2.定义模板
<script id="tem" type="text/html"></script>
type只要不是js 或者为空基础可以
text/html的目的是看起来舒服
3.引用
 调用 template('设置好的',数据)

//格式
{{数据}}  用双大括号包裹
//相当于遍历数组
{{each 数组数据}}
$index //下标
$value //数据
{{each}}

```

#### 2.3自己封装ajax

![1597391949563](C:\Users\qcomj\AppData\Local\Temp\1597391949563.png)

重点:

1. ajax回调函数中的数据如果要传出来不能使用return 使用回调函数的方式
2. 为了避免参数过多编码不方便，参数变为对象
3. 抽取遵守的规则 
   1. 重复出现的代码抽取
   2. 不确定的东西作为参数
   3. 为了避免全局变量污染可以使用一个对象，设置为他的属性
   4. 如果要返回内容 return没有ajax 从上往下执行时可以用return




### 第三天

#### 3.1 ajax 多个参数传递

```js
使用ajax 发送请求的时候 如果有多个参数需要传递

一个参数 key = value
两个参数 key1 = value1&key2 = value2
多个参数 中间用 & 符号连接
```



#### 3.2 jQuery中的ajax

##### $.get 方法 

```js

//概述 : 一个简单的GET请求功能以取代复杂的$.ajax 请求成功时执行回调函数,如果需要在出错时执行回调函数 需要使用$.ajax
//语法: $.get({url,[data],[callback],[type]}) // 带中括号  可选参数
//url --- 待载入页面的url地址
//data --- 待发送 key/value 参数
//callback --- 载入成功时执行的回调函数
//type --- 返回内容的格式  xml, html, script, json, text, _default。 

$.get(
   'http://acg.bakayun.cn/randbg.php', // url地址
   //'Type = json&t=dfzh', //可以这么写 
   {Type : 'json', t : 'dfzh'} // 内部可以识别对象
   function(backdata){ // 请求成功时执行的回调函数
      console.log(backdata)
   }
)
```

##### $.post 方法

```js
//语法 : 
$.post(url,[data],[callback],[type]) //带中括号 可选参数
url:发送请求地址。

data:待发送 Key/value 参数。

callback:发送成功时回调函数。

type:返回内容格式，xml, html, script, json, text, _default。 

$.post(
 'http://www.tuling123.com/openapi/api', // 地址
 { key: '9fbb98effab142c9bb324f804be542ba', info: '你是不是不认识陈琳' }, //待发送的数据 
  function(backData) {    // 请求成功时执行的回调函数
     console.log(backData)
  }
)
```

##### $.ajax 方法

```js
//语法 : $ajax({url,[settings]})  // 一般建议直接传入一个对象
//url : 地址
//type: 请求方法
//data: 数据
//success : 请求成功时执行的回调函数
//dataType : 数据类型
$.ajax({
        url: 'http://www.tuling123.com/openapi/api',
        type: 'post',
        // data:'',支持key=value&key2=value2
        data: {
          key: '9fbb98effab142c9bb324f804be542ba',
          info: '许久未见，甚是想念'
        },
        // dataType:'json',如果jQuery没有帮我们自动转化 可以设置dataType为json
        success: function(backData) {
          console.log(backData)
        }
      })
```

#### 3.3 易错点

1.  没联网
2.  没加引号  key不要加引号  值要加引号
3.  检查请求网址  是否正确

### 第四天

#### 4.1 onreadystatechange(面试,笔试,了解)

比onload兼容性好   工作中jq已经解决



readyState属性

​	readyState,Ajax对象属性

有5个值

![1558410817260](C:/Users/qcomj/Downloads/Ajax/Ajax%20-%20day04/Ajax%20-%20day04/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1558410817260.png)

这5个字表示了ajax对象从创建 ，到完全获取到数据的过程

为了保证一定可以获得数据

一般会在readyState的值为4的时候获取

一般会结合onreadystatechange 一起使用

如果要兼容性好一点  可以用下面写法

```js
xhr.onreadystatechange : function(){
   //当readyState 等于四 的时候获取
   if(xhr.readyState == 4){
      console.log(xhr.responseText)
   }
}
//工作中使用$.ajax居多,实际使用,不需要考虑兼容 jq已经搞定了

```

#### 4.2 HTTP协议

HTTP协议 ---规定了浏览器在和服务器交互时的格式

组成 : 

1. 请求报文

   a.请求头

   b.请求行

   c.请求主体

   ![1597663942779](C:\Users\qcomj\AppData\Local\Temp\1597663942779.png)

2. 响应报文

   a.响应头

   b.状态行

   c.状态行

   ##### ![1597665281424](C:\Users\qcomj\AppData\Local\Temp\1597665281424.png)

   

![1597665697096](C:\Users\qcomj\AppData\Local\Temp\1597665697096.png)