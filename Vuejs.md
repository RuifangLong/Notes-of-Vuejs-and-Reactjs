
* 05 data && computed && methods
    * data 用于 数据的初始化，the initilization of data
    * computed 有缓存功能，用于修改date的值，**写在{{}}不需要写()，虽然它也是函数
    * methods 是动态修改的，只要有渲染，methods就得跟着监听变化
    * v-cloak 由于数据加载需要时间，用v-cloak配合display:none来避免闪现，原理是v-cloak会一直作用到实例化结束
    * vm.$mount('#app'), 实例定义的时候如果没有定义挂载点，可以通过这个挂载
* 06 生命周期函数 Life Cycle Function （HOOK)
    * beforeCreate(), data:undefined, $el:undefined ==>适合loading
    * created(), data: defined , $el: undefined ==>可以对data做修改
    * beforeMount(),            $el.innerHTML:{{username}} ==> 可以操纵节点
    * mounted()                 $el.innerHTML: {{Rae}}
    * beforeUpdate() 前提(在mounted()以后生效，修改了值)，此阶段更新data
    * updated() 此阶段把更新后的data更新render到挂载点上
    * beforeDestroy() 卸载组件，DOM不会再变化，监听事件全部取消，不受Vue控制
    * destroyed() 同上 ==> 清除定时器，延时器，ajax请求

  * <h4>局部样式的实现原理</h4>
    * scoped , webpack 会给当前组件所有html 元素添加data-v-hash
    * 其实只是个属性选择器啦
  * 0430 git
    * 团队开发
    * 分支 branch
        * master
        * dev (开发环境)
        * Rae
        * Lemon
        * Leslie
    * 上线流程
        * 开发环境
            * 自测
            * 单元测试
        * 测试阶段
            * 本地测试
                * 模拟数据
            * UAT (用户测试环境)
                * 真实数据
        * 上线阶段

* webpack 基于模块配置
    export default{

    }
    import todo from '***'// "***" 文件名，import 的是export 的对象 {}
* gulp:基于任务

* 兄弟数据传输  兄---》爸爸---》弟

    * 爸爸传过来的值儿子不接着？ 直接变成儿子的属性
* 虚拟DOM（VNode)
    * 结构类似于DOM节点的js对象
    * diff算法，判断节点状态是否改变，来决定是否更新VNode
    * key 是虚拟节点的唯一标识
* Vuex
* 过滤器（数据换种方式体现或者过滤）{{username}}--->{{username | upperCase}}
   * 全局过滤 Vue.filter("upperCase",definition)
   * 局部过滤 filters
   * 局部与全局命名可以相同，先用局部，找不到局部找全局
   * 正则 
        * /\d{2,5}\/ 默认贪婪拿到5
        * /\d{2,5}？\/  不贪婪拿到2
        
        * 非捕获分组    ?:    不会被捕获，结果不显示
        * ？= 零宽断言
            * 正向/负向
            * 先行/

## webpack 工作原理
    # 基于配置的打包工具
    * entry
    * output
    * loader:加载器，css loader/
       
     * 图片会被webpack 处理
        * require
        * import
        * 相对路径 （在html/css 中的相对路径）
    * 不被webpack处理的情况
        * 绝对路径
        * js中的相对路径
    
    * plugin

## 内置组件：transition && transition group

## h5 新特性
    * 新标签：header....
    * 表单新类型：input type->datapicker(data,time),color
    * Canvas,Video,Audio
    * web Storage
        * sessionStorage
        * localStorage
    * webSocket
    * formData
    * draggable ??真正的拖拽

## VueRouter
* component
* SPA  ---Single Page Application
    * 一个应用只有一个页面
    移动端具有绝对优势，服务器不用多次跳转
* 导航
    * 声明式导航<router-link/>
    * 编程式导航：利用js代码实现导航
* 路由
    * hash (开发阶段用的多)
    * history (上线的时候用的多)
    * 使用步骤
        1. 引用import 
        2. 安装/使用 Vue.use()
        3. 实例化(配置参数), new VueRouter(options)
        4. 注入Vue实例
    * 配置参数
        1. mode: hash, history
        2. routes:[{}]
            * name
            * path
            * component/components(此时要配合多个<router-view>)
            * redirect
            * children[{}]//嵌套路由
                * path 'pad' //不要加/(forwardslash)

    * 路由渲染
        * <router-view/>
            * name
    * 导航
        * 声明式导航 <router-link>
            * to (path|Object)
                to = {name : 'Home'} ->to ='/home'
            <router-link to="{name:'Home'}" replace>

        * 编程式导航
                this.$router // 路由实例，一般用于路由跳转
                this.$route //当前路由
* ajax 请求第三方工具
    * axios
    * fetch

* 传参
    @click.native = "goto(id)"
    methods: {
        goto(){
            this.$routes
        }
    }
* Vuex
    * 核心概念
        * store
            * state
            * getters    类似于computed,不去改变state，对state做一些处理
            * mutations 相当于methods ，修改state的方法
