## promise声明

promise 肯定是一个类，我们用 class 来声明。

* 由于 `new Promise((resolve, reject) => {})`，所以传入一个参数（函数），叫做 executor，传入就执行。
* executor 中有两个参数，resolve (成功)，reject (失败)。
* 由于 resolve 和 reject 可执行，所以都是函数。

```js
class Promise {
// 构造器
  constructor(executor) {
    // 成功
    let resolve = () => {};
    // 失败
    let reject = () => {};
    // 立即执行
    executor(resolve, reject);
  }
}
```

## 解决基本状态

* Promise 有三个状态 (state) -- pending、fulfilled、rejected
* pending (等待态) 为初始态，可转化为 fulfilled (成功态) 和 rejected (失败态)
* 成功时，不可转化为其他状态，且必须有一个不可改变的值 (value)
* 失败时，不可转化为其他状态，且必须有一个不可改变的结果 (reason)
* `new Promise((resolve, reject) => { resolve(value) })` resolve 为成功，接收参数 Value，状态改变为 fulfilled，不可再次改变
* `new Promise((resolve, reject) => { reject(reason) })` reject 为失败，接收参数 reason，状态改为 rejected，不可再次改变
* 若是 executor 函数报错，直接执行 reject()

```js
class Promise {
  constructor(executor) {
    // 初始状态
    this.state = 'pending';
    // 成功的值
    this.value = undefined;
    // 失败的原因
    this.reason = undefined;

    let resolve = value => {
      // state改变 resolve调用就会失败
      if(this.state === 'pending') {
        // resolve调用之后 state转化为成功态
        this.state = 'fulfilled';
        // 存储成功的值
        this.value = value;
      }
    };

    let reject = reason => {
      // state改变 reject调用就会失败
      if(this.state === 'pending') {
        // reject调用之后 state转化为失败态
        this.state = 'rejected';
        // 存储失败的原因
        this.reason = reason;
      }
    };

    // 如果executor执行报错，直接执行reject
    try {
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }
}
```

## then方法

Promise 中有一个 then 方法，里面有两个参数: OnFulfilled, onRejected。成功有成功的值，失败有失败的原因。

* 当状态state 为 fulfilled，传入 this.value。当状态state 为 rejected，传入 this.reason。
* onFulfilled, onRejected 如果他们是函数，则必须分别在 fulfilled，rejected 后被调用，value 或 reason 依次作为他们的第一个参数。

```js
class Promise {
  constructor(executor) { ... }

  // then 有两个参数
  then(onFulfilled, onRejected) {
    if(this.state === 'fulfilled') {
      onFulfilled(this.value);
    };
    if(this.state === 'rejected') {
      onRejected(this.reason);
    }
  }
}
```

参考资料：

* 原作者博客地址：[BAT前端经典面试问题：史上最详细的手写Promise教程](https://juejin.im/post/5b2f02cd5188252b937548ab?utm_source=gold_browser_extension)
* [Promises/A+](https://promisesaplus.com/)