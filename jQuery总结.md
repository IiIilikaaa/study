# jQuery总结

### 第一天

### 1.jQuery定义

------

**jQuery是一个快速,小巧,功能丰富的js库,里面封装了很多的js方法**.

它使HTML文档遍历和操作,事件处理,动画,Ajax等操作变得更加简单

因为它提供了一个易于使用的API,可以跨多种浏览器工作

jQuery结合了通用性和可扩展性,改变了数百万人编写JavaScript的方式

#### 1.1 使用步骤

------

①---引入jQuery文件

②---入口函数 ( 三种写法 ) 

```js
//jquery的入口函数。  1.文档加载完毕，图片不加载的时候就可以执行这个函数。
    $(document).ready(function () {
        alert(1);
    })
    //jquery的入口函数。  2.文档加载完毕，图片不加载的时候就可以执行这个函数。
    $(function () {
        alert(1);
    });
    //jquery的入口函数。  3.文档加载完毕，图片加载完毕的时候在执行这个函数。
    $(window).ready(function () {
        alert(1);
    })
```

③---获取想操作的元素,调用方法操作

#### 1.2 dom对象和jQuery对象的相互转化

------

dom对象 ---> jQuery对象	

```js
//花钱转

     var one = document.querySelector('#one');

     var $one = $(one);//保存jQuery变量时 要用$开头 代码规范

     console.log($one);

```

jQuery ---> dom对象

```js
//使用下标转换
     let $one = $('#one');
     let one = $one[0];
     console.log(one);
//使用jQuery的get方法
    let $div = $('div');
    let div = $divs.get(0);
    console.log(div);
```

#### 1.3 选择器及其优先级

```js
jQuery选择器和css中的选择器是一样的
    id选择器      ↓    $('#one')
    类名选择器    ↓    $('.one')
    标签选择器    ↓    $('div')
    并集选择器    ↓    $('.one,.two')中间用逗号隔开
    交集选择器    ↓    $('.one.two')中间不能有空格
    优先级从上到下 递减
```

#### 1.4 设置和获取文本

```js
$('p').text('需要设置的文本内容')  加参数就是设置文本,不给参数就是获取
```

#### 1.5 设置和获取css样式

```js
$('div').css({}) 方法里面可以放一个对象同时设置多个属性
//给参数就是设置 不给就是获取
```

#### 1.6 mouseenter 和 mouseleave

```js
//和  mouseover mouseout  一样都是鼠标移入,移出事件 
//二者区别 : 前者不会冒泡 后者会冒泡
```

### 第二天

------

#### 2.1class操作

```js
//1.添加类. addClass(类名);
    $('#addClass').click(function () {
      //1.1 给id为div1的元素添加类.
      //$('#div1').addClass('width200');
      //$('#div1').addClass('width200 height200');

      //1.2 给div元素添加类.
      $('div').addClass('width200 height200'); //隐式迭代
    });
    
    //2.移除类. removeClass();
    $('#removeClass').click(function () {
      //2.1 给id为div1的元素移除类.
      //$('#div1').removeClass('width200');
      //$('#div1').removeClass('width200 height200');
      //$('#div1').removeClass();//随意可以删掉所有的,但是不推荐使用.

      //2.2 给div元素移除类.
      $('div').removeClass('width200 height200'); //隐式迭代
    });


    //3.判断类  hasClass();
    //判断元素有没有某个类,如果有就返回true,否则返回false.
    $('#hasClass').click(function () {
      console.log($('#div1').hasClass('width200'));
    });


    //4.切换类. toggleClass();
    //元素有某个类就删除这个类,没有这个类就添加这个类.
    $('#toggleClass').click(function () {
      $('#div1').toggleClass('width200');
    });
```

#### 2.2 动画效果

```js
        //--------显示与隐藏----------
        //可以设置执行动画的时间
        show() 可以控制元素的显示
        hide() 控制元素的隐藏
        //元素如果是 显示 就 隐藏   是 隐藏 就 显示
        //------滑入和滑出-------
        //可以设置执行动画的时间
        slideDown() 控制元素的滑出 
        slideUp() 控制元素的滑出
        slideToggle() 切换滑入滑出效果
        //--------淡入淡出--------
        //设置时间控制动画执行速度
        fadeIn()  淡入
        fadeOut() 淡出
        fadeTo() 淡出到什么程度
        fadeToggle() 切换效果
        

```

#### 2.3 自定义动画

```js
//自定义动画  animate(参数一prop,参数二speed,参数三easing,参数四callback)
//参数一 : 必填,是一个对象,表示动画执行时 有哪些属性改变
//参数二 : 必填,动画时长
//参数三 : 选填,jQuery提供了 'linear'匀速 , 'swing'缓速  默认时缓速
//参数四 : 选填,动画执行完的回调函数

```

#### 2.5动画队列

```js
stop(参数一,参数二)//停止动画 
//参数一 : 是否清除队列
//参数二 : 是否跳转到当前动画的最终效果
//默认情况 两个参数都是false
```



#### 2.6 each() 方法

```
$().each(callback(回调函数)) //通用遍历方法,可用于遍历对象和数组
//回调函数中有两个参数 
function( index, ele ){
   console.log(index) //遍历对象的下标
   console.log(ele)   //ele == this
}
```

#### 2.7 创建元素

```  js
回顾js中创建元素的方法 : document.wirte()  document.createElement()  innerHTML  
//jQuery 中创建元素的方法  html() $()
html() 方法 
$().html() //不设置参数  就是获取调用方法的标签内容
//设置参数 就是给标签添加内容
//注意 : 如果参数中有标签  会自动解析出来  
//       会覆盖原有的内容
$().html('我是设置的内容<a href="https://www.baidu.com">新闻</a>')

$() 方法  //也会自动解析标签  但是创建出来的元素之存在内存中  需要配合 append()方法追加到页面中
let $a = $('<a href="https://www.baidu.com">新闻</a>');
      //console.log($a);
$('#div').append($a);
```

### 第三天

------

#### 3.1 添加节点的五种方法

```js
    //jQuery 添加节点的五种方式
    //----------01----------
    //append()  语法 : 父元素.append(子元素) 作为最后一个子元素添加到父元素

    //-----------02------------
    //prepend()  语法: 父元素.prepend(子元素)  作为第一个子元素添加到父元素

    //------------03------------
    //before()  语法 : 兄弟元素A.before(兄弟元素B)  将B元素 插入到A元素的前面  作为兄弟元素添加
    //如果是两个本来就有的兄弟元素 那么他们调换位置 

    //------------04------------
    //after() 语法 : 兄弟元素A.after(兄弟元素B)  将B元素 插入到A元素后面  作为兄弟元素添加
    //如果是两个本来就有的兄弟元素 那么他们调换位置 

    //------------05------------
    //appendTo() 语法 : 子元素.appendTo(父元素)  作为最后一个子元素添加

```

#### 3.2 清空节点  和  移出节点

```js
  //$('#div').html(""); //虽然可以达到效果,但是推荐不要使用. 因为他只会清空标签,不会清除标签上的事件.

  //$('#div').empty(); //推荐使用的清空元素的方法, 因为他不仅清空标签,还会清空标签上的事件.

  //2.删除某个元素. remove(); "自杀"

```

#### 3.3  克隆节点

```js
//回顾原生js 克隆节点的方法
//cloneNode() 方法 
//参数 : 为true时 深克隆 会克隆标签的内容
//      为false时 浅可隆 不会克隆标签内容

//jQuery 克隆节点
//clone() 
//克隆的节点只存在于内存  在页面显示需要追加  append()
//不管有没有参数都会克隆后代元素 
//参数为 true : 会克隆事件
//      false : 不会克隆事件
```

#### 3.4   获取和设置表单元素的 value 值

```js
//回顾原生js中 获取和设置表单元素value值得方法

//jQuery 中 val() 获取和设置表单元素的value值
// 没有参数就是获取   有参数就是设置
```

#### 3.5  操作属性

```js
//回顾原生js中  操作属性的方法: getAttribute() //获取
//									 setAttribute() //设置
//									 removeAttribute() //删除

//jQuery操作属性  attr() 获取和设置  removeAttr() 删除
// attr('src') //获取src的值  如果参数是一个不存在的属性会返回undefined
// attr('src','1.png') //src属性如果有值 就替换  没有就添加

//removeAttr('需要删除的属性名')
```

#### 3.6  操作布尔类型的属性

```js
//回顾: 布尔类型的属性 ( checked selected disable ),在元素身上加了就有效果 没加就没有效果
    //操作方法  给属性设置 true 或者  false

    //原生js
    // document.getElementById('btn').onclick = function () {
    // document.getElementById('checkbox').checked = false//true 就选中单选框 false就取消选中
    // document.getElementById('checkbox').disabled = true//true 就禁用单选框 false就取消禁用
    // selected 配合 <select></select> 下拉列表使用
    // }

//jQuery 1.6版本之后 对于Boolean类型的属性来说 不能用attr()方法
// prop() 操作布尔类型的方法
prop('checked') //获取
prop('checked',true) // 将checked 设置为true
```

#### 3.7 获取元素宽高

```js
		//下面方法 给参数就是设置  不给就是获取
      //1.css();
      //console.log($('#one').css('width')); //'200px'
      //console.log($('#one').css('height'));//'200px'
		//2.width(); height();
      //获取元素的内容宽高
      //3.innerWidth()/innerHeight()
      //方法返回元素的宽度/高度（包括内边距）。
      //4.outerWidth()/outerHeight()
      //方法返回元素的宽度/高度（包括内边距和边框）。
      //5.outerWidth(true)/outerHeight(true)
      //方法返回元素的宽度/高度（包括内边距、边框和外边距）。

```

### 第四天

------

#### 4.1 offset() 和 position()

```js
//回顾原生js中 三大家族  offset家族  scroll家族  client家族
//offset家族----offsetWidth offsetHeight  offsetLeft  offsetTop offsetparent() 

//jQuery中 offset() 和js中的不同
//offset() 返回的是一个对象 里面有left 和 top
//offset() 方法获取元素到document的距离
//给参数就是设置  不给就时获取
// 注意 : 如果元素原本没有定位 系统会给它一个相对定位


//position()方法
//获取的是元素相对于父元素的定位 返回的也是一个对象 里面有left 和 top
// !!!!只能获取 不能设置!!!!!

```

#### 4.2  scrollTop()  和  scrollLeft()

```js
//原生js中scroll家族: scrollLeft  scrollTop  scrollWidth  scrollHeight

//1.jQuery中也有scrollLeft()和scrollTop();
//和原生js中的scrollLeft和scrollTop是一样的,都表示内容滚出去的距离.

//jQuery中没有scrollWidth()和scrollHeight();
//如果要获取元素内容的宽高,可以把他转成dom对象调用原生的scrollWidth/scrollHeight属性.
//console.log($('div').scrollWidth() +" : "+ $('div').scrollHeight()); //报错了
//需要设置 先将jQuery对象转化为dom对象
      
//滚动事件 scroll
$(window).on('scroll', function () {
    console.log($(window).scrollLeft() +" : "+ $(window).scrollTop());
});

```

#### 4.3 事件注册和解绑

```js
//回忆下原生js中如何解绑事件的:
    // document.getElementById("one").onclick = function () {
    // };//注册
    // document.getElementById("one").onclick = null;
    // ie8 之前不兼容
    // document.getElementById("one").addEventListener();//注册
    // document.getElementById("one").removeEventListener();
	 // ie8 之前适用
    // document.getElementById("one").attachEvent();//注册
    // document.getElementById("one").detachEvent();

//jQuery 事件注册
//简单注册  
$('#div').on('click',function(){
   console.log('我是简单注册事件')
})
//委托注册
$('body').on('click','div',function(){
   console.log('我是委托注册事件')
})
function test(){
   console.log('我是test函数')
}
$('body').on('clicl','div',test) // 调用先前声明的函数

//事件解绑
//简单事件解绑
$('#div').off() //不给参数 解绑所有参数
$('#div').off('click')  //给参数 解绑所有参数
//委托事件解绑
$('body').off()//不给参数 解绑所有参数
$('body').off('click')//给参数 解绑所有参数

//注意 : 必须保证注册的事件处理程序和解绑的事件处理程序要一样.
```

#### 4.4 事件触发  和  注册自定义事件

```js
//触发器trigger();
      //1.用代码的方式来触发事件.
      //2.用来触发自定义事件.
//注册自定义事件
$('#div').on('auto',function(){
   console.log('我是自定义事件')
})
//可以设定条件然后调用 trigger()方法触发
```

#### 4.5 jQuery的事件对象

```js
//回忆一下原生js中事件对象:
    //不管那个事件被触发,系统都会有一个事件对象产生,这个对象就记录这个事件触发时候的一些信息. 比如有没有按住alt键,比如触发时候的坐标....
    //原生js中用事件参数e来获取事件对象. 原生js中事件对象有兼容性.
    // document.getElementById("one").onclick = function (e) {
    //   e = e || window.event;
    //   console.log(e);
    //   //console.log("pageX :"+e.pageX + "-" + e.pageY); //原生js事件对象中的pageX/pageY有兼容性.
    // };

//jQuery中也有事件对象,jQuery中的事件对象其实就是原生js中的事件对象的一个封装.
//帮你处理好了兼容性.

//事件对象中有三个常用坐标.
//和原生js中的一模一样.
console.log("screenX :"+e.screenX + "-" + e.screenY); //屏幕左上角 距离触发事件的那一点的距离
console.log("clientX :"+e.clientX + "-" + e.clientY); //页面可视区左上角距离触发事件的那一点之间的距离.
console.log("pageX :"+e.pageX + "-" + e.pageY);//页面左上角 距离触发事件那一点之间的距离.

      e.stopPropagation();阻止事件冒泡
      e.preventDefault();//阻止跳转(浏览器默认行为)


//委托注册的第三个参数是需要传递的 数据, 用事件对象e.data获取,一般不用
    // $('body').on('click','div','我是传递的数据', function (e) {
    //   console.log(e.data);
    // });
```

#### 4.6 end() 方法

```js
//有些时候调用方法返回的确实是一个jQuery对象,但是不是我们想要的jQuery对象. 达不到我们想要实现的效果.
//end()方法可以返回到上一层的那个对象那里.
```

### 第五天

------

#### 5.1 多库共存问题

```js
//--------------01---------------
//如何查看引入的jQuery文件的版本
//文件名一般有注明版本号 但有时候 不靠谱
// 通过源码 可以知道
// jQuery 可以看成 $  prototype 可以看成 fn
// 所以打印版本号的方法有
// console.log(jQuery.prototype.jquery);
// console.log(jQuery.fn.jquery);
// console.log($.fn.jquery);
// console.log($.prototype.jquery);

//--------------02-------------
//当同一个页面中我们引入了多个jQuery文件时 这个时候$符号是哪一个jQuery版本中的?
//此时的$是最后一个引入的jQuery版本中的

//---------------03--------------
//当我们引入多个jQuery文件 这是的$属于最后面引入的jQuery文件 这是我们想要调用前面引入的jQuery文件的内容 
// $.noConflict() 方法可以释放$的控制权  用返回值来代替原来的 --$--
//只是替代了$
let _$one = $.noConflist() //调用该方法 返回的是释放前的$  

//--------------04--------------
//如果我们已经用一个$写了很多代码  现在又需要释放控制权 用前面的$书写代码


(function ($) {
//代码体  这里我们就可以愉快的使用$了
// console.log($.fn.jquery)
console.log($.fn.jquery);
}(_$one))
```

#### 5.2 插件的使用

```js
jq22.com  //插件网址  里面有各种jQuery  插件
//使用插件  先引入jQuery文件 在引入插件文件
```

#### 5.3 自己封装插件

```js
//jQuery插件封装
//原理 : 就是给jQuery的原型中添加方法 jQuery的兑现就可以调用这个方法了 

//新建一个js文件
//自执行函数  
(function($){
   $.fn.函数名(一般和插件名字一样) = function(){
   //插件代码
   }
}(jQuery))
```

#### 5.4  not() 方法

```js
not(expr|ele|fn)
//从匹配元素的集合中删除与指定表达式匹配的元素
//参数:
exp
一个选择器字符串。

element  
一个DOM元素

function(index)
一个用来检查集合中每个元素的函数。this是当前的元素。
```

