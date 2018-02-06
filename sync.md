## 这是异步事件的文档学习

- 回调函数
```javascript
假定有两个函数f1/f2 后者等待前者的执行结果
f1();
f2();
```
```javascript
function f2(){
    console.log(222)
}
function f1(callback){
    setTimeout(function(){
        callback();
    },1000)
}
f1(f2);
console.log(5555);
```
> 采用这种方式，我们把同步操作变成了异步操作，f1不会堵塞程序运行，相当于先执行程序的主要逻辑，将耗时的操作推迟执行。

  回调函数的优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（Coupling），流程会很混乱，而且每个任务只能指定一个回调函数
- 事件监听
`思路`
> 另一种思路是采用事件驱动模式。任务的执行不取决于代码的顺序，而取决于某个事件是否发生。

  还是以f1和f2为例。首先，为f1绑定一个事件（这里采用的jQuery的写法）
  ```javascript
  　f1.on('done', f2);
  ```
  ```javascript
  function f2(){
          console.log(222)
      }

      var f1=function(){
          setTimeout(function(){
              console.log(111);
              $("#btn").trigger("done");
          },1000)
      };
      $("#btn").bind("done",f2);
      f1();
      console.log(5555)
  ```
  > 这种方法的优点是比较容易理解，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以"去耦合"（Decoupling），有利于实现模块化。缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。

- 发布订阅 `思路`
> 上一节的"事件"，完全可以理解成"信号"。

>  我们假定，存在一个"信号中心"，某个任务执行完成，就向信号中心"发布"（publish）一个信号，其他任务可以向信号中心"订阅"（subscribe）这个信号，从而知道什么时候自己可以开始执行。这就叫做"发布/订阅模式"（publish-subscribe pattern），又称"观察者模式"（observer pattern）。
> 这个模式有多种实现，下面采用的是Ben Alman的Tiny Pub/Sub，这是jQuery的一个插件。
  首先，f2向"信号中心"jQuery订阅"done"信号。


 ```javascript
 jQuery.subscribe("done", f2);

 　function f1(){

 　　　　setTimeout(function () {

 　　　　　　// f1的任务代码

 　　　　　　jQuery.publish("done");

 　　　　}, 1000);

 　　}
 ```
 > jQuery.publish("done")的意思是，f1执行完成后，向"信号中心"jQuery发布"done"信号，从而引发f2的执行。

 > 此外，f2完成执行后，也可以取消订阅（unsubscribe）。这种方法的性质与"事件监听"类似，但是明显优于后者。因为我们可以通过查看"消息中心"，了解存在多少信号、每个信号有多少订阅者，从而监控程序的运行。

```javascript

jQuery.unsubscribe("done", f2);
```
- promise 对象

> Promises对象是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口。

> 简单说，它的思想是，每一个异步任务返回一个Promise对象，该对象有一个then方法，允许指定回调函数。比如，f1的回调函数f2,可以写成：

```javascript
f1().then(f2);
```
> f1要进行如下改写（这里使用的是jQuery的实现)

```javascript
unction f1(){

　　　　var dfd = $.Deferred();

　　　　setTimeout(function () {

　　　　　　// f1的任务代码

　　　　　　dfd.resolve();

　　　　}, 500);

　　　　return dfd.promise;

　　}
```
> 这样写的优点在于，回调函数变成了链式写法，程序的流程可以看得很清楚，而且有一整套的配套方法，可以实现许多强大的功能。

 > 比如，指定多个回调函数.

  > 而且，它还有一个前面三种方法都没有的好处：如果一个任务已经完成，再添加回调函数，该回调函数会立即执行。所以，你不用担心是否错过了某个事件或信号。这种方法的缺点就是编写和理解，都相对比较难。

[参考大神的链接](http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html)