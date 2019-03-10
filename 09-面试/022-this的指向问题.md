> this的指向在函数定义的时候是确定不了的，只有函数执行时才能确定this到底指向谁，实际上this最终指向的是那个调用它的对象。

**例1**：指向window

```js
function a() {
  var age = 24;
  console.log(this.age);  //undefined
  console.log(this);  //Window
}
a();
```

```js
function a() {
  var age = 24;
  console.log(this.age);  //undefined
  console.log(this);  //Window
}
window.a();
```

按照我们说的this最终指向的是调用它的对象，这里的函数a实际就是被Window对象点出来的，上面第二段代码可以证明。

**例2**：指向调用它的对象

```js
var obj = {
  age: 24,
  fn: function() {
    console.log(this.age);  //24
  }
}
obj.fn();
```

这里的this指向的是对象obj。看起来很简单吧，那么我们继续吧！

**例3**：指向最近的调用它的对象

```js
var obj = {
  age: 24,
  fn: function() {
    console.log(this.age);  //24
  }
}
window.obj.fn();
```

按照“this指向在函数定义时是确定不了的，只有函数执行时，谁调用了它就指向谁”这段话，为什么指向的不是window呢？

其实关于this的指向问题我们需要分几种情况：
* 如果一个函数中有 `this`，他没有被上一级的对象所调用，那么 `this` 指向 `window`（js严格版中，`this` 指向的是 `undefined`）
* 如果一个函数中有 `this`，这个函数有被上一级的对象所调用，那么 `this` 指向的就是上一级的对象
* 如果一个函数中有 `this`，这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，`this` 指向的也只是它上一级的对象。

同例3：
```js
var obj = {
  age: 24,
  b: {
    fn: function() {
      console.log(this.age);  //undefined 
    }
  }
}
obj.b.fn();
```

**例4**：谁调用他就指向谁

```js
var obj = {
  age: 24,
  b: {
    age: 12,
    fn: function() {
      console.log(this.a);  //undefined
      console.log(this);  //Window
    }
  }
}
var j = obj.b.fn;
j();
```

咦，为什么这里的this指向的是window呢？

this永远指向的是最后调用它的对象，也就是看它执行的时候是谁调用的。例4中虽然函数fn是被对象b所引用，但是在将fn赋值给变量j的时候并没有执行，所以最后指向的是window。和例3不同，例3是直接执行了fn。

**例5**：new改变this指向

```js
function Fn() {
  this.age = 24;
}
var a = new Fn();
console.log(a.age);  //24
```

这里我们可以看出，`new` 关键字改变了this的指向，将this指向对象a。

为什么说a是对象，因为用了new关键字就是创建了一个对象实例，new关键字相当于复制了一份。

这里变量a创建了一个Fn的实例（相当于复制了一份Fn到对象a里面），此时仅仅只是创建，并没有执行，而调用这个函数Fn的是对象a，那么this指向的自然是对象a了。

**例6**：当this遇到return

```js
function fn() {
  this.age = 24;
  return {};
}
var a = new fn;
console.log(a.age);  //undefined
```

```js
function fn() {
  this.age = 24;
  return function() {};
} 
var a = new fn;
console.log(a.age);  //undefined
```

```js
function fn() {
  this.age = 24;
  return 1;
}
var a = new fn;
console.log(a.age);  //24
```

```js
function fn() {
  this.age = 24;
  return undefined;
}
var a = new fn;
console.log(a.age);  //24
```

从上面可以看出，如果返回值是一个对象，那么this指向那个返回的对象；如果返回值不是一个对象那么this还是指向函数的实例。

但是，虽然null是对象，但在这里this还是指向那个函数的实例，因为null比较特殊。

```js
function fn() {
  this.age = 24;
  return null;
}
var a = new fn;
console.log(a.age);  //24
```

### call,applay,bind

`call`, `applay`, `bind` 一般用来指定 `this` 的环境。

我们来看两个例子：

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);
  }
}
a.fn();  //24
```

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);
  }
}
var b = a.fn;
b();  //undefined
```

我们通过这种方法可以改变this的指向，但是最好的方法还是用 `call`/`apply`/`bind`。

#### 1.call()

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);  //24
  }
}
var b = a.fn;
b.call(a);
```

通过call方法，给第一个参数添加要把b添加到a的环境中，那么this就会指向a对象。

call方法除了第一个参数以外还可以添加多个参数：

```js
var a = {
  age: 24,
  fn: function(e, ee) {
    console.log(this.age);  //24
    console.log(e+ee);  //3
  }
}
var b = a.fn;
b.call(a, 1, 2);
```

#### 2.apply()

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);  //24
  }
}
var b = a.fn;
b.apply(a);
```

apply也可以多个参数，但是第二个参数必须是一个数组：

```js
var a = {
  age: 24,
  fn: function(e, ee) {
    console.log(this.age);  //24
    console.log(e+ee);  //11
  }
}
var b = a.fn;
b.apply(a, [10, 1]);

// var arr = [10, 1];
// b.apply(a, arr);
```

**如果call和apply的第一个参数写的是null，那么this指向的是window对象**

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this);  //Window {external: Object, chrome: Object, document: document, a: Object, speechSynthesis: SpeechSynthesis…}
  }
}
var b = a.fn;
b.apply(null);
```

#### 3.bind()

bind方法同样可以改变this的指向。

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);
  }
}
var b = a.fn;
b.bind(a);
```

我们发现代码没有被打印，是因为bind方法返回的是一个修改过后的函数。

```js
var a = {
  age: 24,
  fn: function() {
    console.log(this.age);
  }
}
var b = a.fn;
var c = b.bind(a);
console.log(c);  //function() { [native code] }
c();  //24
```

同样bind也可以有多个参数，并且参数可以执行的时候再次添加，但是要注意的是，参数是按照形参的顺序进行的。

```js
var a = {
  age: 24,
  fn: function(e, d, f){
      console.log(this.age);  //24
      console.log(e, d, f);  //10 1 2
  }
}
var b = a.fn;
var c = b.bind(a,10);
c(1,2);
```

**call 和 apply 都是改变上下文中的 this 并立即执行这个函数，而 bind 方法可以让对应的函数想什么时候调用就什么时候调用，并且可以将参数在执行的时候添加。**

#### 箭头函数中的this指向

箭头函数体内的 this 对象就是定义时所在的对象，而不是使用时所在的对象。

还有一点值得注意的，this 对象的指向是可变的，但在箭头函数中它是固定的。

```js
function foo() {
  setTimeout(() => {
    console.log("id", this.id);
  }, 100);
}
foo.call({ id: 42 });  // id: 42
```

在 《ES6标准入门》中有这样一个例子：

```js
var handler = {
  id: "123456",
  init: function() {
    document.addEventListener("click", event => this.doSomething(event.type), false);
  },
  doSomething: function(type) {
    console.log("Handling " + type + "for" + this.id);
  }
};
```

上面的 init 方法中使用了箭头函数，导致 this 指向 handler 对象。

```js
function Timer() {
  this.seconds = 0;
  setInterval(() => this.seconds++, 1000)
}
var timer = new Timer();
setTimeout(() => console.log(timer.seconds), 3100);  // 3
```

Timer 函数内部的 setInterval 调用了 `this.seconds` 属性，通过箭头函数让 this 总是指向 Timer 的实例对象。

**this 指向的固定化，并不是因为箭头函数内部有绑定 this 的机制，实际原因是箭头函数根本没有自己的 this，导致内部的 this 就是外层代码块的 this。正因为它没有 this，所以也就不能用作构造函数。**

详细内容见 《es6标准入门》 P80.