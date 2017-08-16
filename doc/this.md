<i id="top"></i>

# this #

不同场景下的this指向
* <a href="#global">全局函数</a>
* <a href="#object">对象</a>
* <a href="#call">call(), apply()</a>
* <a href="#bind">bind()</a>
* <a href="#new">new</a>
* <a href="#es6">ES6箭头函数</a> 

## <span id="global">全局函数</span> <a href="#top">♥</a>

#### 非严格模式
```
function thisFn() {
  console.info('this',this);
};

thisFn();// window
```

#### 严格模式

```
'use strict'

function thisFn() {
  console.info('this',this);
};

thisFn();// undefined
```

## <span id="object">对象</span> <a href="#top">♥</a>

函数作为对象的属性。
```
let obj = {
    getThis: function() {
        return this;
    }
}
```
1 函数作为对象的属性调用，`this`指调用的对象
```
obj.getThis();// obj对象
```
2 函数不作为对象的属性调用, `this`指`window`
```
var o = obj.getThis;
o();// obj 对象
```
3 函数的返回值是 其他对象的函数
```
let obj2 = {
    getThis: function() {
        return obj.getThis();
    }
}

obj2.getThis();// obj 对象
```
4 键值对的值 是其它函数
```
let obj3 = {
    getThis: obj.getThis
}

obj3.getThis();// obj3 对象
```
## <span id="call">call(), apply()</span> <a href="#top">♥</a> 
call(), apply() 函数的作用：在特定作用域中调用函数。第一个参数是在其中运行函数的作用域
```
function fn() {
    return this;
};

fn();// window
fn.call(obj);// obj 对象
fn.apply(obj);// obj 对象
```
## <span id="bind">bind()</span> <a href="#top">♥</a> 
1 bind()方法绑定对象，上下文到函数中
```
function fn() {
    return this;
};

fn.bind(obj)();// obj 对象
fn.bind(window);// window
```

2 apply(),call()方法的替换对象无法覆盖
```
var o = fn.bind(window);

o()// window
o.call(obj);// window
```
## <span id="new">new</span> <a href="#top">♥</a> 
1 new 一个构造函数和普通函数用法的 this指向不同
```
function Function = (){
    return this;
};

Function();// window

let fun = new Function();
fun();// Function对象
```
2 通过bind()绑定的函数也会被new覆盖
```
let fun = Function.bind(obj);
fun();// obj对象
new fun();// Function对象
```
## <span id="es6">ES6箭头函数</span> <a href="#top">♥</a>
箭头函数中的this指向

>函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

1 箭头函数没有自己的this,而是引用外层函数的this
````
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });// id: 42
````

2 由于箭头函数没有自己的this，所以不能通过apply(),call(),bind()方法改变this指向
````
(function() {
  return [
    (() => this.x).bind({ x: 'inner' })()
  ];
}).call({ x: 'outer' });// ['outer']
````

````
function fun(){
    return ()=>{
        return ()=>this
    }
}
let f1 = fun.call(obj);//window
````
