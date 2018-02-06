## jQuery的deferred对象详解
> 简单说，deferred对象就是jQuery的回调函数解决方案 它解决了如何处理耗时操作的问题，对那些操作提供了更好的控制，以及统一的编程接口。它的主要功能，可以归结为四点。下面我们通过示例代码，一步步来学习.

> deferred对象的最大优点，就是它把这一套回调函数接口，从ajax操作扩展到了所有操作。也就是说，任何一个操作----不管是ajax操作还是本地操作，也不管是异步操作还是同步操作----都可以使用deferred对象的各种方法，指定回调函数。

```javascript
$.when($.ajax("test.json"),$.ajax("test2.json"))

        .done(function(data,data2){

            console.log(data,data2);

        } )

        .fail(function(){ console.log("出错啦！"); } )

        .done(function(){ console.log("第二个回调函数！");} );

```
[参考文档地址](http://www.ruanyifeng.com/blog/2011/08/a_detailed_explanation_of_jquery_deferred_object.html)

