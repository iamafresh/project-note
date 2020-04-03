1 各种超出处理（页面超出（滚动， 分页), 单行 多行文本超出（...)
2 多个相关联字段共用一个 action， 容易导致字段拼错问题， 如何校验？？？

React.memo 处理函数式组件的重新渲染

## 第三方库

### react-dnd

> 提供一个拖拽上下文和反馈拖拽状态的第三方库

### 第三方库问题

### antd-mobile

### 技巧

> 如果某一个组件提供的 api 不能满足要求，可以查看这个组件依赖的 rc-xx 系列组件，这一些列组件的 api 更底层，可以做更多的定制

### 样式

#### 
 > 页面布局组件：处理页面title固定，页面滚动等问题
 > 处理刘海屏  css surport属性

> 背景模糊化
> filter: blur(5px);

> 默认向右对齐
> justify-content: flex-end;

> 蒙层实现
> filter: gray;

    opacity: .8;

filter: alpha(opacity=50);

> 不定个数垂直居中自左向右对齐(grid)
> display: grid;

    grid-gap: 20px;
    grid-template-columns: repeat(auto-fit, minmax(6rem, 1fr));

这个如果只有一行时候还是会居中，但是我们想要的是整体居中，自选自左向右对齐，可以通过 js 大致判断其个数填充数据来实现

### 页面内滚动实现

> 特别是页面头部或者底部有需要固定在页面时，此时页面可以采用 flex 布局， 然后滚动部分容器组件用如下样式可解决大部分问题
> flex: 1;
> overflow-y: scroll;

## 遇到的问题

===============================================================================

#### 滚动穿透

> 目前使用的解决方法：通过调节判断强制设置背景页为不能滚动
> 一个标准 input 输入框，输入文字自左向右显示，光标显示正常，但是设置 text-align:right 后，文字向右对齐后，光标（caret）居然显示在最后一个字符上面了

> 渲染覆盖了(展示组件只加载一次，但是每次展示组件都重新渲染了 props 导致每次展示都是一样)
> 为了不重新渲染父组件，控制显隐的 state 放在子组件，但是交互完成之后需要在父组件重置显隐 state(如何在父组件不引起自身重新渲染的前提下改变子组件的值 )
> 为什么父组件调用子组件的失败

#### 后行判断正则兼容问题（只有 chrome 实现)

[参考](https://segmentfault.com/a/1190000018194862)

### 样式问题

> 同一个 LightItem 需要单控，组控里面的单控，组双击出来模态框里面单控等多个响应式样式
> 还需要考虑 ipad 和手机的适配
> svg Icon 组件如何响应式
> flex 布局的文本溢出问题（设置 width：0 或其他 min-width, max-width)

### 路由问题

> 路由的正确使用（push replace pop redirect 使用场景，与浏览器和移动端返回键预期效果一致)
> 通过路由的匹配和 action 作为判断数据

### 工具问题

react-devtool 的组件为什么不响应页面操作了（而且只是某一个）
vconsole 打印日志插件为啥用着用着就不能打印请求日志了

### 待解决问题

1 装饰器影响获取完整的组件实例？

> SingleRoom 中获取 GroupController 实例， GroupController 有这个@injectIntl 装饰器时候不能拿到完整的实例

## 性能优化

=======================================================================================

> React.memo + useCallback
> 1 schedule 模块 UI 目录 CustomDatePicker 组件

## 组件设计

#### LongPress

#### Popup

#### Tab

## 技巧和经验

> 数组操作预先做 falsy 值过滤

## 薄弱点

> replace 和正则

## 新知识点

### sentry bug 监听原理

> 通过劫持 window.error

### 其他问题

zigbee 成组问题（多个接口成功失败如何处理
切换账户 sceneList 没有拉取网关同步数据

### git 记录

### 分支操作

- 本地先开好分支然后推送到远程

> git push origin feature-branch:feature-branch

- 拉去远程某个分支到本地并切换过去

> git fetch origin [remote-branch-name]
> git checkout -b [local-branch-name] origin/[remote-branch-name]

### git diff

- git diff 查看尚未暂存的文件变更部分
- git diff --staged 查看已暂存的变更

### git log (常用)

- git log --stat 显示每次更新的文件修改统计信息
- git log --graph 显示 ASCII 图形表示的分支合并历史
- git log --pretty=short 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式
- git log git log --pretty=format:"%h - %an, %ar : %s"
- git log -- [path] 查看制定文件或者目录的提交记录
- git log --author=[person] 查看某个开发者提交记录

### 撤销操作

#### 取消暂存文件

- git reset HEAD <file>

#### 撤销对文件修改

- git checkout --<file>

### git config

- git conifg -l
- git config --global alias.co checkout 别名
- git config --global user.name [name] 用户配置

### 具体逻辑（createRoom)

==================================================================================
1 创建 room 判断当前房间数据是否已达到限制上限
2 清除创建房间表单可能的缓存数据
3 在页面通过 roomId 判断是创建还是编辑
4 name 字段的输入限制（输入长度和可输入的字符）
5 placeholder 和未选择的默认值
6 选项跨页面，主页面会不定卸载加载，意味着数据要保存在全局（redux,或 localStarate)
7 字段不仅要考虑输入，还是考虑编辑模式每项显示正确完整一致的数据

> 提交时候
> 1 校验
> 1 判断必填项
> 2 判断 name 是否为空或者重名
> 2 准备提交
> 1 设置定时器（因为是监听方式）做一些重置数据操作和清除定时器操作
> 2 请求开始 loading
> 3 发送数据给中间层
> 3 多层协议的中间层发送请求并接受请求返回给页面
> 4 处理响应
> 1 成功处理方式（更新 redux 数据，成功提示，清除数据、定时器，跳转返回上一个页面
> 2 失败处理 （失败提示，清除定时器）
> 3 超时提示 （清除定时器，清除计算数据
> 其他
> 如何保证返回上一个页面（手机返回键，而不是写死路由地址）
> 很简单维护历史记录栈，创建 push 进入子选项页面 push ， 子选项返回主页面用 goBack(), 这就是关键点
> 如何保证多次快速点击子选项，goBack()只执行一次
> 自定义个一个 once 函数

## TODO

1 国际化语言 key 值能否简洁些
2 为什么没有 prettier + airbnb 插件 看看这个 Prettier-Standard
3 总结 antd-mobile 各组件可能遇到的坑

## 体验优化

### 页面焦点管理

> 一个常见的问题：我刚刚在 ipad 上面创建一个 group， 并且编辑了组名， 这时候焦点在 input 上面， 我点击其他空白区域发送请求， 但是这时候我希望键盘也会自动收起

解决方案
1 获取页面焦点元素 const el = document.activeElement;
2 让焦点元素失去焦点 el.blur();

参考 https://blog.csdn.net/yc123h/article/details/51337411

// 2019
https://github.com/iamafresh/2019-demo.git

## latest

- @supports

## 物联网相关

- [MQTT 入门](https://www.runoob.com/w3cnote/mqtt-intro.html)
- [MQTT 中文网](http://mqtt.p2hp.com/mqtt311)

## 跟踪

1 一个问题：创建一个默认亮度和默认色温的 scene 执行 scene 回传回来的数据是有误差的

## 再次强调原则

- 逻辑与 UI 分离
- State 最小化

## 请求

### 异步串行实现

- for of + await
- reduce + promise
- async(第三方库)

## sensor group 设计

UI
按照功能模块划分局部组件（这样好处是局部组件可以自己管理内部字段的依赖关系）局部组件内部各字段使用全局基础组件 参考（MoreEdit 组件）

逻辑处理
按照上面的局部组件作为局部容器组件处理业务，每个模块无非就是编辑某些字段
redux 设计
沿用以前的思路：只需要一个 action action 内容包括字段和字段值
good：简化 redux 代码 简化 action 定义 文件导出 action 等
bad: 不能保证每次 action 的字段名是有效的

解决方式： 字段名 常量化，reducer 中检测字段名，方可保证字段名有效

todo
1 整理相关全局基础 UI 组件
2 是否中间协议层的？这部分估时是否没有？
3 是否后面还会添加 zigbee 协议
4 如何做到逻辑与 UI 分离，可维护可扩展？

feat/LMS-8903

### 一些自定义方法

```js
/**
 * 请求重试方法
 * @param {Function} fn 请求方法
 * @param {Object} data 请求参数对象
 * @param {Number} count 重试次数
 * @return {Promise}
 */
export async function reTry(fn, data, count) {
  if (count === 0) {
    const errorRes = {
      code: 400,
      data: { message: '重试多次失败' },
    };
    return errorRes;
  }

  const res = await fn.call(window, data);

  if (res && res.code === 200) {
    return res;
  }

  count -= 1;
  return await reTry(fn, data, count);
}
```

```js
// call自定义实现
/* 想想有这样一个对象 const obj = {name: 'song'} 调用原生call方法 就相当于在这个对象上面添加一个同名方法调用 */
Function.prototype.myCall = function myCall(...rest) {
    const context = rest[0]
    const fn = this;
    context.func = fn;
    
    return context.func(...rest.slice(1))
}
```

