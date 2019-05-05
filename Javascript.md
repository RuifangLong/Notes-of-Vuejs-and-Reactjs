<h1>Interesting JS Points</h1>

<h6>Author: Ruifang Long</h6>

<h3>跨域解决方案：Cross-Domain Solution</h3>

1:产生跨域的原因(The reason )

*协议

*域名/主机

*端口

2：为什么有跨域？？？

3：跨域解决方案

1：自己的服务器

​	*jsonp

​	原理：<script>标签可以获取任何js代码的特点，在本地定义一个callback，回调函数以res.query的形式传给API,获取远程API的数据，一定一定要满足输出数据是JSON格式，供回调函数调用？

​	（注意：在API端返回的是callback(JSON.stringify(data)),但是前端不需要解析(不用jJSON.parse(data))直接可以获取执行callback(data);

​	不能直接用ajax请求，要利用script标签请求

​	把全局的“函数名”发送给服务器 ：window.getData()

​	

​	<strong>如果后端返回的数值是object object, 说明后端没有做json.stringfy()处理；



​	*CORS 跨域资源共享

​	通过设置res,header("Access-Control-Allow-origin","http://localhost:1901") 如果是*，允许所有服务器访问

​	另外，通过设置allowList =[几个端口]，判断res.headers.origin是否存在于被请求

2:别人的服务器

​	*服务器代理

​	通过服务器request(“目标网址”，{form:{key:'values'}}),(err,response,body)=>{

​	})

​	这是最原始的工具

​	*http-proxy-middleware

​	服务器代理中间件，这是第三方代理

​	1：先引入模块

​	const proxy = require('http-proxy-middleware');

​	2:代理配置

​	var options = {}

​	3:Router.get('/jiuxian',proxy(options));

​	4:前端请求的时候，要把路径补全，就是options 的target路径后面的写全

​	<em>Router.use()与Router.get():use 不管什么请求都进来，get只有get才进来</em>

Websocket

​	http:80端口/https:443端口

​		*无状态

​		*被动性响应

​		*跨域限制

​		*短连接（接收到请求的消息后，断开）

​	websocket:ws

​		*主动性

​		*信息安全性

​		*跨域

​		*长连接

​	###客户端：socket

​	###服务端：socket

​	(前后联动，可以实现多人聊天室功能)

<h4>Websocket 详解</h4>

<p style="color:red">这是聊天室的代码总结，应该复用性很高，源代码在chatRoom里面</p>

<ul style="color:green">服务器端01
    <li>创建普通express 服务器</li>
    <li>express获取app组件</li>
    <li>app植入内置中间件，利用中间件实现静态资源服务器</li>
    <li>app 监听服务器端口号</li></ul>

<span>上面的流程是普通的创建服务器</span>

<ul style="color:green">服务器端02
    <li>引入'ws'组件      
    </li>
    <li>通过http 模块连接web服务器和socket服务器,让其公用一个端口<br/>
    	let server = http.Server(app);
    </li>
    <li>
        创建websocket服务<br/>
        let socketServer = ws.Server;(引入服务器)<br/>
        let socket = new socketServer({sercer});(创建websocket服务器)
    </li>
</ul>

​        

<ul style="color:green">下面开始要进入服务器轮巡咯
    <li>监测socket 是否连接，传入callback,唯一参数就是client<br/>
    <span style="color:#234">每个客户端连接到socket服务器都会执行处理函数</span>
    </li>
    <li>连接到服务器的客户端，socket.client 都要进行消息监听，并对所有的socket.clients进行广播<span style='color:red'>返回给前端让前端渲染，前端通过判断username是否是当前客户端的username进行颜色/右浮动处理</span></li>
    <li>client也要进行'退出’操作的监听，向所有用户广播当前用户退出</li>
</ul>

```html



<p style="color:red">
    终于轮到前端了
</p>
  
  
```

<ul style='color:hotpink'>
    <li>点击注册</li>
<li>socket = new WebSocket('ws://localhost:1901')<br/>
    webSocket是windows内置对象，连接到后端设置的ws服务器</li>
    <li>socket的onopen 和onmessage都是一直在轮询的状态</li>
  <li>连接服务器成功后执行onopen事件，并在当前客户端显示“服务已连接信息”
      并且把自己的用户名信息发送给服务器</li></ul>

## 0505
* 阻止事件冒泡
    * e.cancelBubble = true(IE8以下) && e.stoppropagation()
    * 表单阻止提交， return false// 这是阻止默认事件哦
* Vue directives(v-on:click=)
    * v-on directive to listen to DOM event 
    * event modifiers
        * .stop
        * .prevent
        * .capture
        * .self
        * .once
        * .passive




​    
















<h3>Array(last edit <time>04/22</time>)</h3>

<h5>Array.prototype.reduce</h5>

<h6> The reduce() method executes a reducer function on each member of the array resulting in a single output value.(from 0-array.length-1, for reduceRight(), from array.length-1 to 0</h6>

<p>The reducer function takes four arguments.</p>

<p>回调的reducer函数可以传入四个参数</p>

​	1:Accumulator

​	2:Current Value

​	3:idx

​	4:arr

(作为一种数组遍历？后三个参数与map,forEach等类似，第一个参数acc作为内置累加器，其实和自己在外面定义一个res=[]来存储的效果一样)

<strong>Attention:Accumulator 也是返回值哦</strong>

<h5>The full list of methods on array instances that  change the values or the number of values in the array</h5>

1:push &&pop 

push:(返回值是array新的长度)

pop:The removed element from the array

2:shift && unshift

unshift: return value:the new length of the array

shift: returns the removed element

3:splice &&reverse

arr.splice(startidx,num,addElement)   startidx: the index to delete num elements       addElements: Elements to be added to the array

<strong>返回值是被delete的值</strong>

reverse: return value=> The reversed array

4:sort

返回值：排序后的数组

排序方法是按照unicode 的编码顺序，对于字符串数字？"12"排序有误

一般调用arr.sort((a,b)=>a-b)是升序，反之降序

总结：删就返回被删除，增加就返回新数组长度





