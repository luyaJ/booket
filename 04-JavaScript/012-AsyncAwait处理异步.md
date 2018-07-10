## async

`async` 它作为一个关键字放在函数前面，用于表示函数是一个 **异步函数**。异步函数也就意味着该函数的执行不会阻塞后面代码的执行。

```js
async function timeout() {
  return 'hello luyaj'
}
timeout();
console.log('虽然在后面，但是我先执行了');
```

控制台输出：
```bash
虽然在后面，但是我先执行了
```

上面的代码，我们再看看，`timeout()` 执行返回了什么，把上面的 timeout() 语句改为 console.log(timeout())：

```js
async function timeout() {
    return 'hello luyaj'
}
console.log(timeout());
console.log('虽然在后面，但是我先执行');

// 控制台输出：
// Promise {<resolved>: "hello luyaj"}
// 虽然在后面，但是我先执行
```

原来 `async` 函数返回的是一个 `promise` 对象，如果要获得 promise 的返回值，我们应该用 then 方法：

```js
async function timeout() {
  return 'hello luyaj'
}
timeout().then(result => {
  console.log(result);
})
console.log('虽然在后面，但是我先执行了');

// 控制台输出：
// 虽然在后面，但是我先执行
// hello luyaj
```

我们获得了“hello luyaj”，同时 timeout 的执行也没有阻塞后面代码的执行。

在上上面的执行结果中，我们看到了在 Promise 中有一个 resolved，这是 async 函数内部的实现原理。如果 async 函数中有返回一个值，当调用该函数时，内部会调用 `Promise.resolve()` 方法把它转化为一个 Promise 对象作为返回，但如果 timeout 函数内部抛出错误呢？那么就会调用 `Promise.reject()` 返回一个 Promise 对象，这时修改一下代码：

```js
async function timeout(flag) {
  if(flag) {
    return 'hello luyaj'
  } else {
    throw 'oh no, it has mistakes'
  }
}
console.log(timeout(true));  // 调用Promise.resolve() 返回promise对象
console.log(timeout(false));  // 调用Promise.reject() 返回promise对象

// 控制台输出：
// Promise {<resolved>: "hello luyaj"}
// Promise {<rejected>: "oh no, it has mistakes"}
```

## await

`await` 的意思是等待的意思，它的后面可以放任何表达式，不过我们更多的放一个返回 promise 对象的表达式。await 关键字只能放到 async 函数里面。

现在写一个函数，让它返回 promise 对象，该函数的作用是2s 之后让数值乘以2：

```js
function after2seconds(num) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num * 2)
    }, 2000);
  })
}

<!-- 写一个async函数，从而可以使用await关键字 -->
async function testResult() {
  let res = await after2seconds(30);
  console.log(res);
}

testResult();
```

在控制台看结果，先会出现 `Promise {<pending>}`，两秒之后打印出 `60`。

代码运行过程：调用 testResult 函数，它在里面遇到了 await，代码就先暂停在这里，不再向下执行了。它将会等到后面的 after2seconds(30) 执行完毕，after2seconds(30) 返回的 promise 开始执行，2秒之后，promise resolve 了，并返回了值为 60，这是 await 才拿到返回值 60，然后赋值给 result，暂停结束，代码才开始继续执行，执行 console 语句。

```js
function after2seconds(num) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num * 2);
    }, 2000);
  });
}

async function testResult() {
  let first = await after2seconds(30);
  let second = await after2seconds(50);
  let third = await after2seconds(30);
  console.log(first + second + third);
}

testResult();

// 6秒后，输出值为220
```

文章转载自：[用async/await来处理异步](https://www.cnblogs.com/SamWeb/p/8417940.html)