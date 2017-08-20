# Promise #

## ES6 promise

`Promise` 是异步编程的一种解决方案，从`Promise`对象可以获取异步操作的消息

#### Promise对象的 特点
1. 对象的状态不受外界影响，只有异步操作的结果可以决定当前状态。
    * `Pending`（进行中）
    * `Fulfilled`（已成功）
    * `Rejected`（已失败）
2. 一旦状态改变就不会再变。
    *  `Pending` -> `Fulfilled`
    * `Pending` -> `Rejected`

#### Promise对象的 缺点
1. 一旦新建立即执行，且无法中途取消。
2. 不设置回调函数时，`Promise`内部抛错不会反应到外部。
3. 无法根据`Pending`状态得知进展到哪个阶段（刚刚开始还是即将完成）

#### Promise对象的 用法
````
let promise = new Promise(
  (resolve, reject) => {
    if(/*success*/){
      resolve(response);
    }else{
      reject(new Error(status));
    }
  })

promise.then(
  response => console.info("data");
  error => console.info("error");// 可以省略
)
````

参考：http://es6.ruanyifeng.com/#docs/promise

## angular1 promise
