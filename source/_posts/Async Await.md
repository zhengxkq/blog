---
title:Async/Await知识总结
---

### 基本规则

1. async 表示这是一个async函数，await只能用在这个函数里面。
2. await 表示在这里等待promise返回结果了，再继续执行。
3. await 后面跟着的应该是一个promise对象（当然，其他返回值也没关系，只是会立即执行，不过那样就没有意义了…）

### 栗子

这里我们要实现一个暂停功能，输入N毫秒，则停顿N毫秒后才继续往下执行。


```
var sleep = function (time) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            resolve();
        }, time);
    })
};

var start = async function () {
    // 在这里使用起来就像同步代码那样直观
    console.log('start');
    await sleep(3000);
    console.log('end');
};

start();
```
控制台先输出start，稍等3秒后，输出了end。

### 获得返回值

await等待的虽然是promise对象，但不必写.then(..)，直接可以得到返回值。


```
var sleep = function (time) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            // 返回 ‘ok’
            resolve('ok');
        }, time);
    })
};

var start = async function () {
    let result = await sleep(3000);
    console.log(result); // 收到 ‘ok’
};
```

### 捕捉错误

既然.then(..)不用写了，那么.catch(..)也不用写，可以直接用标准的try catch语法捕捉错误。


```
var sleep = function (time) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            // 模拟出错了，返回 ‘error’
            reject('error');
        }, time);
    })
};

var start = async function () {
    try {
        console.log('start');
        await sleep(3000); // 这里得到了一个返回错误
        
        // 所以以下代码不会被执行了
        console.log('end');
    } catch (err) {
        console.log(err); // 这里捕捉到错误 `error`
    }
};
```

### 循环多个await


```
..省略以上代码

var start = async function () {
    for (var i = 1; i <= 10; i++) {
        console.log(`当前是第${i}次等待..`);
        await sleep(1000);
    }
};
```

值得注意的是，await必须在async函数的上下文中的。


```
..省略以上代码

let 一到十 = [1,2,3,4,5,6,7,8,9,10];

// 错误示范
一到十.forEach(function (v) {
    console.log(`当前是第${v}次等待..`);
    await sleep(1000); // 错误!! await只能在async函数中运行
});

// 正确示范
for(var v of 一到十) {
    console.log(`当前是第${v}次等待..`);
    await sleep(1000); // 正确, for循环的上下文还在async函数中
}
```






