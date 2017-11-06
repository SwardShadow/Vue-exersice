# 这是一个个人学习的练习项目

## 这里面有各种不足请各位大牛指正

### 有注释的代码都是好代码

## 制作首页App组件

1. 完成Header区域，使用的是Mint-UI中的header组件
1. 制作底部的Tabbar区域，使用的是MUI的Tabbar.html

+ 在制作购物车小图标的是后续，操作会相对多一些
+ 先把扩展图标的css样式拷贝到目录中
+ 拷贝拓展字体库ttf文件到项目中
+ 为购物车添加小图标，添加如下样式`mui-icon mui-icon-extra mui-icon-extra-cart`

1. 要在中间区域防止一个`router-view`来展示路由匹配到的组件

## 改造tabbar为router-link

## 设置路由高亮

## 点击tabbar中的理由链接，展示对应的路由组件

## 制作首页轮播图布局

## 加载首页轮播图数据

1. 获取数据，使用`vue-resource`。
1. 使用`vue-resource`的`this.$http.get`获取数据
1. 获取到的数据要保存到data身上
1. 使用`v-for`循环渲染每个item项

## 改造九宫格区域的样式

## 改造新闻资讯的路由链接

## 新闻资讯页面的制作

1. 绘制界面，使用MUI中的`media-list.html`
1. 使用`vue-resource`获取数据
1. 渲染真实数据

### 实现新闻资讯列表

点击跳转到新闻详情

1. 把列表中的每一项改造为`router-link`，同时在跳转的时候应该提供唯一的Id标识符
1. 创建新闻详情的组件页面 `NewsInfo.vue`
1. 在路由模块将新闻详情的路由地址和组件页面对应起来

## 实现新闻详情的页面布局和数据渲染

## 单独封装一个comment.vue评论子罪案

1. 线创建一个comment.vue组件模版
1. 在需要使用comment组件的页面中，先手动导入comment组件
1. 在父组件中，使用`components`属性，将刚才导入comment组件注册为自己的子组件
1. 将注册子组件时候的注册名称，可以以标签形式在页面中引用即可。

## 获取所有的评论数据显示到页面中

+ getComments

## 实现点击加载更多评论的功能

1. 为加载更多按钮绑定点击事件，在事件中请求下一页数据
1. 点击加载更多，让`pageIndex++`,然后重新调用this.getComments()方法重新获取最新一页的数据
1. 为了防止新数据覆盖老数据的情况，我们在点击加载更多的时候，每当获取到新数据，应该让老数据调用数组的concat方法拼接上新数组

## 发表评论

1. 把文本框做双向数据绑定
1. 为发表按钮绑定一个事件
1. 校验评论内容是否为空，如果为空，则`Toast`提示用户，评论内容不能为空。
1. 通过`vue-resource`发送一个请求，把评论内容提交给服务器。
1. 当发表评论OK后，重新刷新列表，以查看最新的评论

+ 如果调用`getComments`方法重新刷新评论列表的话，可能只能得到对后一页的评论，前几页的评论获取不到。
+ 换一种思路：当评论成成后，在客户端手动拼接出一个最新的评论对象，然后调用数组的`unshift`方法，把最新的评论，追加到`data`中`comments`的开头；这样就能完美实现刷新评论列表的需求。

## 改造图片分析 按钮为路由的链接并显示对应的组件页面

## 绘制图片列表，组件页面结构并美化样式

1. 制作顶部的滑动条；
1. 制作底部的图片列表

### 制作顶部滑动条的"坑"

1. 需要借助于MUI的`tab-top-webview-main.html`
1. 需要把`slider`区域的`mui-fullscreen`类去掉
1. 滑动条无法正常触发滑动，通过检查官方文档，发现在是JS组件，需要被初始化一下

+ 导入`mui.js`
+ 调用官方提供的方式去初始化

```js
mui(".mui-scroll-wrapper").scroll({
// flick减速系数，系数越大，滚动速度越慢。滚动距离越小。默认值0.0006
deceleration:0.0005;
});
```

1. 我们在初始化滑动条的时候，导入的`mui.js`，但是控制台会报错，`Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode`
+ 经过我们合理的推测，觉得可能是`mui.js`中用到了"callee","caller","arguments"东西，但是webpack在打包好的`bundle.js`中，默认是启用严格模式的，所以这两者冲突了。
+ 解决方案：第一种方法是把`mui.js`中的非严格模式的代码改掉，但是不现实。第二种方法是把`webpack`打包时候的严格模式禁用掉。
+ 最终，我们选择了方法二移除严格模式；使用这个插件 babel-plugin-transform-remove-strict-mode

1. 刚进入图片分型页面的时候，滑动条无法正常工作，经过我们认真的分析，发现如果要初始化滑动条，必须要等DOM元素加载完毕，所以我们把初始化滑动条的代码搬到了`mounted`生命周期函数中;
1. 当滑动条调试OK后，发现tabbar无法正常工作了，这时候我们需要把tabbat按钮的样式中`mui-tab-item`改一下名字；
1. 获取所有分类，并渲染分类列表；

### 制作图片列表区域

1. 图片列表需要使用懒加载技术，我们可以使用`Mint-UI`提供的现成的组件`lazy-load`
1. 根据`lazy-load`的使用文档，尝试使用
1. 渲染图片列表数据

### 实现了图片列表的懒加载改造和样式美化

## 实现了点击图片跳转到图片详情页面

1. 在改造li成`router-link`的时候，需要使用tag属性执行要渲染为哪种元素

## 实现图片详情中的缩略图的功能

1. 使用插件`vue-preview`这个缩略图插件
1. 获取到所有的图片列表，然后使用`v-for`指令渲染数据
1. 注意：img标签上的class不能去掉
1. 注意：每个图片数据对象中，必须有w和h属性。

## 绘制商品列表页面基本结构并美化

## 尝试在手机上去进行项目的预览和测试

1. 要保证自己的手机可以正常运行；
1. 要保证手机和开发项目的电脑处于同一个`wifi`环境中，也就是说手机可以访问到电脑的IP;
1. 打开自己的项目中`package.json`文件，在`dev`脚本中，添加一个`--host`指令，把当前电脑的`wifi Ip`地址设置为`--host`的指令之；
1. 如何查看自己电脑锁处的`wifi`环境呢，在cmd终端中运行`ip config`，查看无线网的ip地址