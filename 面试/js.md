### new实现
```js
function myNew(fn, ...rest) {
    const instanceObj = Object.create(null)  // 创建一个真正的空对象
    Object.setPrototypeOf(instanceObj, fn.prototype) // 设置空对象的原型
    fn.apply(obj, rest)  // 给实例对象添加属性

    return instanceObj //返回实例对象
}
```

### bind
```js
if (!Function.prototype.bind) {
    Function.prototype.bind = function(context, ...bindRest) {
        // bindRest 绑定时传参
      const self = this;
      if (typeof self !== 'function') {
          throw new TypeError('context must be functionj')
      }

      return function(...callRest) {
          // callRest 调用时传参
        const rest = bindRest.concat(callRest)
          return self.apply(context, rest)
      }
    }
}
```

### 深拷贝
```js
```

### curry

### redux
### redux中间件原理
> Redux 的中间件提供的是位于 action 被发起之后，到达 reducer 之前的扩展点 redux 中间件通过改写 store.dispatch 方法实现了action -> reducer的拦截