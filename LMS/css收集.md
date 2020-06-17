### 网页适配 iPhoneX
```js
@supports (bottom: constant(safe-area-inset-bottom)) or (bottom: env(safe-area-inset-bottom)) {
div {
margin-bottom: constant(safe-area-inset-bottom);
margin-bottom: env(safe-area-inset-bottom);
}
```
[参考](https://blog.csdn.net/qq_42354773/article/details/81018615)

### 移动端适配方案

#### 目前我们采用的
> 利用rem的特性  动态更改根元素的font-size大小再结合媒体查询 + flex布局
