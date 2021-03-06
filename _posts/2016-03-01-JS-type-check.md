---
layout: post
title:  "Javascript 类型判断方法!"
date:   2016-03-01 16:58:04
categories: jekyll update
tags:
- javascript
---
# 判断js变量类型的三个方法

#### 1. 使用Object.prototype.toString.call(val)
{% highlight ruby %}
    console.log(Object.prototype.toString.call(true)); //[object Boolean]
    console.log(Object.prototype.toString.call(3)); //[object Number]
    console.log(Object.prototype.toString.call({})); //[object Object]
    console.log(Object.prototype.toString.call([])); //[object Array]
    
    console.log(Object.prototype.toString.call(undefined)); //[object Undefined]
    console.log(Object.prototype.toString.call(null)); //[object Null]
    
    console.log(Object.prototype.toString.call(Array)); //[object Function]
    console.log(Object.prototype.toString.call(Function)); //[object Function]
    console.log(Object.prototype.toString.call(Object)); //[object Function]
{% endhighlight %}


#### 2. 使用val.constructor的方法
{% highlight ruby %}

    var num = 3;
    var undef = undefined;
    var nu = null;

    console.log(true.constructor); //[Function: Boolean]
    console.log(num.constructor); //[Function: Number]
    console.log({}.constructor); //[Function: Object]
    console.log([].constructor); //[Function: Array]

    console.log(undef.constructor); // error
    console.log(nu.constructor);    // error

    console.log(Array.constructor); //[Function: Function]
    console.log(Function.constructor); //[Function: Function]
    console.log(Object.constructor); //[Function: Function]
{% endhighlight %}
至于为什么不用typeof呢?这是因为对于数组, typeof的结果会很奇怪:


#### 3. 使用typeof
{% highlight ruby %}
    console.log(typeof true); // boolean
    console.log(typeof 3); // number
    console.log(typeof {}); // object
    console.log(typeof []); // object

    console.log(typeof undefined); // undefined
    console.log(typeof null); // object

    console.log(typeof Array); // function
    console.log(typeof Function); // function
    console.log(typeof Object); // function
{% endhighlight %}

  总结:

  感觉目前为止最好的方法是第一种,用Object.prototype.toString.call(val)去获取,然后最后得到 [object 类型名] 这种形式的字符串,,虽然比较难记住,但是它的局限性是最小的.

  而用constructor这种方法,得到的是[Function: 类型]的形式,不过对于构造子形式的局限是对于undefined和null这两个特殊
的数据结构是不存在构造子的,而且对于函数的声明,构造子会返回声明时的构造函数,而不是类型!
  
  至于typeof这个方法算是比较简单粗暴,可以直接返回类型名,不过需要注意的是当用typeof判断数组的时候,会返回object而不是array,而且typeof null 返回的结果也是object.
