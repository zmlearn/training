# JavaScript 基础知识清单

JavaScript 是一门独立的脚本语言, 和 DOM 没有直接关系.

DOM 可以粗略理解为浏览器为 JavaScript 提供的一套 API, 让 JavaScript 可以通过调用相关 API 实现具体的功能.
比如增减/改变 HTML 元素.

JQuery 是 JavaScript 的一个库, 如果乐意, 你也可以写一个自己的 XQuery.

## 闭包

- 理解什么是闭包.

## 函数

- 理解函数值和函数调用的区别:

    ```js
    function fn() {
    
    }
    
    window.onload = fn;
    window.onload = fn();
    ```

- 理解 arguments:

    ```js
    function fn() {
        console.log('arguments 是数组吗?', arguments instanceof Array);
        console.log('参数个数:', arguments.length);
        console.log('参数:', arguments);
    }
    
    fn('abc', 123);
    ```

- 理解 call/apply:

    ```js
    function fn(a, b) {
        console.log(a, b);
    }
    
    fn.call(undefined, 'abc', 123);
    fn.apply(undefined, ['abc', 123]);
    ```

- 理解 return:

    ```js
    function foo() {
    
    }
    
    function bar() {
        return undefined;
    }
    
    console.log(foo() === bar());
    ```

# 构造函数/类

- 构造函数

    ```js
    function Foo() {
        console.log(this);
    }
    
    new Foo();
    Foo();
    ```

- 原型

    ```js
    function Foo(name) {
        this.name = name;
    }
    
    Foo.prototype.test = function () {
        console.log('hello, ' + this.name + '!');
    };
    
    var foo = new Foo('lalala');
    
    foo.test();
    ```

## 事件

- 常见的用于添加事件的方法:

    ```js
    window.addEventListener('load', function () {
        alert('window loaded');
    });
    
    $(window).on('load', function () {
        alert('window loaded');
    });
    ```

- 事件冒泡/取消/禁用浏览器默认行为:

    ```js
    $('button').click(function (event) {
        event.stopPropagation();
        event.preventDefault();
    });
    ```

## 同步/异步

- 常见的同步方法:

    ```js
    alert('alert 是同步的, 因为它会阻塞后面代码的执行.');
    confirm('当然 confirm 也是, 同样的还有 prompt.');
    
    var xhr = new XMLHttpRequest();
    
    // 当第三个参数是 false 时, 接下来的 xhr.send 是同步的.
    xhr.open('get', 'http://baidu.com', false);
    xhr.send();
    
    // 请求结束后才会继续执行这里.
    console.log(xhr.responseText);
    ```

- 常见的异步方法:

    ```js
    setTimeout(function () {
        console.log('BOOM!');
    }, 1000);
    
    setTimeout(function () {
        console.log('REPEATEDLY BOOM!');
    }, 1000);
    
    var xhr = new XMLHttpRequest();
    
    // 当第三个参数是 true 时, 接下来的 xhr.send 是同步的.
    xhr.open('get', 'http://baidu.com', true);
    xhr.send();
    
    // 这时需要通过监听 xhr 的 readystatechange 事件来获取结果.
    ```

- JavaScript 是单线程的. 所有异步执行的片段**一定**会在当前已经在执行的片段执行完成后才会执行:

    ```js
    setTimeout(function () {
        console.log('后');
    }, 0);
    
    console.log('先');
    ```
