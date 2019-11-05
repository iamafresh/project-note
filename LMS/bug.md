## React.memo + connect 导致页面空白 如下

export default connect(
mapStateToProps,
mapDispatchToProps,
)(React.memo(ChooseScenes));

解决： react-redux 一个 bug 在 5.1.0 修复 所以升级一下版本解决了
参考 https://stackoverflow.com/questions/52998469/how-to-use-react-memo-with-react-redux-connect

## 处理 ios input 在 readonly 还会显示光标

> input[readonly] {

    pointer-events: none;

}

参考 https://segmentfault.com/a/1190000011393682

## slider 组件如果用到 align-xx 系列属性包 bug(需要更多的确认和定位原因)

## 获取本地时间正午十二点小时 得到 0 时

#### 原因

> 本地客户端为十二小时制时候 就会导致这种情况

#### 解决

> toLacaleTimeString 方法获得本地时间字符串判断上下午

## slider 组件快速滑动一小段距离还会回弹

#### 原因： afterOnchange 之后还会触发一次 onchange 和 afterOnchange

#### 解决： afterOnchange 之后 300ms 不让触发 onchange

## 模态框蒙层点击穿透

### 原因

> onclick 时间 300 毫秒延迟

### 解决： 用 touch 代替 onclick
