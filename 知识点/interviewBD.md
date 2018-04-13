 面试题目
1. flex如何垂直居中，如何水平居中
```
justify-content
align-items
<div style='display: flex; justify-content: center;'>
  <span>水平居中</span>
</div>
<div style='display: flex; align-item: center; width: 100%; height: 200px;'>
  <span>垂直居中</span>
</div>
```
- 合并两个有序数组成一个有序数组（合并两个有序队列）
```
方法一：  
var a = [1,2,3,4];
var b = [3,6,8,9,10];
c = a.concat(b).sort((x,y) => {
    return x-y;
});
方法二：
function arr(a, b) {
    var c = new Array(a.length + b.length);
    var i = 0, j = 0, k = 0;
    while(i < a.length && j < b.length) {
        if(a[i] < b[j]) {
            c[k] = a[i];
            k++;
            i++;
        }else {
            c[k] = b[j];
            k++;
            j++;
        }
    }
    while(i < a.length) {
        c[k] = a[i];
        k++;
        i++;
    }
    while(j < b.length) {
        c[k] = a[j];
        k++;
        j++;
    }
    return c;
}
```
- 写一个before函数（before(count, function)），返回一个函数，调用不超过count次。 当count已经达到时，最后一个函数调用的结果将被记住并返回。
```
_.before = function(times, func) {
    var memo;
    return function() {
      if (--times > 0) {
        memo = func.apply(this, arguments);
      }
      if (times <= 1) func = null;
      return memo;
    };
  };
```

- 使用appendChild, insertBefore实现insertAfter功能
```
if 没有节点
    then appendChild
else
    insertBefore(nextElementChild)
```

- 请描述If-Modified-Since Last-Modified字段的作用

```
`Last-Modified`与`If-Modified-Since`都是用来记录最后修改时间。当客户端访问页面时，服务器会将页面最后修改时间通过`Last-Modified`标识由服务器发往客户端，客户端记录修改时间，再次请求本地存在的cache页面时，客户端会通过`If-Modified-Since`头将先前服务器端发过来的最后修改时间戳发送回去，服务器端通过这个时间戳判断客户端的页面是否是最新的，如果不是最新的，则返回新的内容，如果是最新的，则返回`304`告诉客户端其本地`cache`的页面是最新的，客户端就可以直接读取本地本地。
```
- history.pushState与history.replaceState的区别

```
对这两个属性不太了解！`history`提供了对浏览器历史记录读取的一些方法，比如使用`back()`,`forward()`,`go()`可以在历史记录中前进和后退；从字面意思上感觉`history.pushState`可能是向`history`中插入一条记录；`history.replaceState`可能是替换更新一条记录。
```
- 使用reduce和concat实现concatAll

```
个人理解`concatAll`意思是让多个数组连接成一个数组  
function concatAll(a,...b) {
  let c = [a, ...b];
  c.reduce((x,y) => {
    return x.cancat(y);
  })
}
```
- Promise对象的then方法中怎样才能保证promise链式调用继续下去，在链式调用里面如何处理错误

```
`then`方法也会返回一个`promise`对象，所以后面可以继续链式调用下去；
`then`方法里有两个回调函数，一个用于处理满足状态，一个用于处理错误。
```
- 如何实现轮播（移动container，或者单个计算位置translate）

```
移动container:  
`div`包含`ul`，`ul`里面包含多个`li`;每个`li`包含一张图，通过定时器控制`ul`的`left`来实现轮播，每次只显示一张图。  
单个计算位置：

```
- 原型链与instanceof的原理

```
原型链：利用原型让一个引用类型继承另一个引用类型的属性和方法。
instanceof原理：查看对象B的原型指向的对象是否在对象A的原型链上。如果在，则返回true,如果不在则返回false。
```
- 解释一下同源策略与常用的跨域的办法

```
同源策略是浏览器为了安全性实施的策略；所谓同源是指URL的协议、域名、端口号都相同；常用的跨域方法有`JSONP`,`CORS`,`Proxy`,`Cookie`同源策略。
`JSONP`：`<script>`标签可以加载跨域的JavaScript脚本，并且被加载的脚本和当前文档属于同一个域，因此在文档中可以调用/访问脚本中的数据和函数。如果JavaScript脚本中的数据是动态生成的，那么只要在文档中动态创建`<script>`标签就可以实现和服务端的数据交互。JSONP就是利用`<script>`标签的跨域能力实现跨域数据访问，请求动态生成的JavaScript脚本同时带一个`callback`函数名作为参数。JSONP只支持GET请求。
`CORS`:通过在HTTP Header中添加扩展字段，服务器在相应网页头部加入字段表示允许访问domain和HTTP method，客户端检查自己的域是否在允许列表中，决定是否处理响应。
`Proxy`：把访问其他域的请求替换为本域的请求；本域的请求是服务器的动态脚本负责转发的实际请求。
`Cookie`：由于Cookie同源只关注域名、忽略协议和端口，所以可以用来跨域。
```
- position几种取值及其含义

```
`absolute`：绝对定位，相对最近一级的不是`static`的父元素进行定位；
`relative`:相对定位，相对于骑在普通流中的位置进行定位；
`fixed`：固定位置，通常相对于浏览器的窗口或iframe进行定位;
`static`:没有定位，元素出现在正常的流中；
`sticky`:生成粘性定位的元素，容器的位置根据正常文档流计算得出；
```
- CSS样式的优先级

```
1. !imporment
2. html标签中的style
3. id选择器
4. 类选择器，属性选择器，伪类选择器
5. 标签
6. 通配符
7. 继承
8. 浏览器默认属性
```
- 解释一下重绘和回流

```
当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候。在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。
当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为repaint重绘。
```

15 ==运算符判断相等的流程是怎样的

```
如果两个值类型相同，按照===比较方法进行比较
如果类型不同，使用如下规则进行比较
如果其中一个值是null，另一个是undefined，它们相等
如果一个值是数字另一个是字符串，将字符串转换为数字进行比较
如果有布尔类型，将true转换为1，false转换为0，然后用==规则继续比较
如果一个值是对象，另一个是数字或字符串，将对象转换为原始值然后用==规则继续比较
其他所有情况都认为不相等
```

16 四种常见的 Form POST 提交数据类型

```
application/x-www-form-urlencoded
multipart/form-data
application/json
text/xml
```
17 解释一下事件代理(委托)是如何实现的
```
事件委托利用了事件冒泡，只指定一个事件处理程序就可以管理某一类型的所有事件。
```

18 如何理解HTTP是无状态的协议，日常开发中运用什么技术方案弥补的
```
无状态：个人理解是浏览器给服务器发送请求，服务做出响应；当同一个浏览器再次给服务器发请求时，服务器不知道是哪个浏览器。  
常用的技术是`cookie`和`session`;
`cookie`:客户端用于存放服务端发送的特殊信息；客户端再向服务器发送请求的时候，都会把相应的Cookie再次发回至服务器
`session`：服务端用于存放用户信息，服务端将session id发到客户端；当客户端再次发送请求的时候，会将这个session id带上，服务器接受到请求之后就会根据session id找到相应的session.
```

19 call, apply还有bind的相同点与不同点
```
相同点：用来改变函数的作用域
不同点：call和apply接收的参数不同，`apply`需要将参数放入一个数组进行传递，`call`不需要；个人理解的`bind`用来改变`this`的指向,将函数绑定到某个对象  
function bind(scope) {
  var fn = this;
  return function() {
    return fn.apply(scope,arguments)
  }
}
```

20 手写代码，从100个数里面选10个不重复的数
```
function findNum(a) {
  //我把a当做数组了，里面有一百个数
  if(a.length < 10) {
    return false;
  }
  var b = [];
  while(b.length <= 10) {
    i = Math.floor(Math.random()*a.length);
    if(b.indexOf(a[i]) == -1) {
      b.push(a[i]);
      a.splice(i,1);
    }
    if(a.length == 0) {
      return false;
    }
  }
  return b;
}
``` 

21 aaabbc -> abc
```
方法一：
function deDuplication(a) {
  let set = new Set(a);
  return Array.from(set);
}
方法二：
function deDuplication(a) {
  let b = [];
  for(let i = 0; i < a.length; i++) {
    if(b.indexOf(a[i]) == -1) {
      b.push(a[i]);
    }
  }
  return b;
}
```

22 写一段代码

xiaoming().eat(‘apple’).play(‘football’);

xiaoming eat apple play football
```
//创建一个类
function Person(){};
//在原型上定义相关方法
Person.prototype ={
  name:function(who) {
    this.who = who;
    return this;
  },
  eat:function(food){
    this.food = food;
    return this;
  },
  play:function(ball){
    this.ball = ball;
    return this.who + ' eat' + ' ' + this.food + ' play' + ' ' + this.ball;
  }
}
function xiaoming() {
 var xiaoming = new Person();
 return xiaoming.name('xiaoming')
}
console.log(xiaoming().eat("apple").play("football"));
```