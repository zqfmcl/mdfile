---
title: Javascript
date: 2019-10-02 10:00:00
tags: 前端
---

## Javascript

/*函数是对象，函数名是指针*/

function sum(num1, num2){
    return num1 + num2;
}
alert(sum(10, 20));    // 20    

var anotherSum = sum;     // 使用不带圆括号的函数名是访问函数指针，而非调用函数   

alert(anotherSum(10, 10);    // 20

sum = null;
alert(anotherSum(10, 10));    // 20

//    ==========

/*函数声明与函数表达式*/
            // 解析器会率先读取函数声明，并使其在执行任何代码之前可用(可以访问);
        // 至于函数表达式，则必须等到解析器执行到它所在的代码行，才会被真正被解释执行。
        // 

```
    alert(sum(10, 10));
    // 函数声明
    function sum(num1, num2){
        return num1 + num2;
    }
    // 函数表达式
    sum = function(num1, num2){ // 执行会报错
        return num1 + num2;
    }
```

//    ==========

/*函数名本身就是变量，函数可以作为值来使用*/
        // 1.作为参数传递；2.作为函数结果返回
        function callSomeFunction(someFunction, someArgument){
            return someFunction(someArgument);
        }
        // 要访问函数的指针而不执行函数的话，必须去掉函数名后面的那对圆括号

//    ==========
/*函数内部属性  arguments 和 this*/
        // arguments 还有一个名叫  callee 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数

```
    // 阶乘函数(一般用到递归算法)
    function factorial(num) {
        if(num <= 1){
            return 1;
        }else{
            return num * factorial(num - 1); //问题：函数执行与函数名factorial紧紧耦合了
        }
    }
    // 使用 callee 属性 解决 耦合
    function factorial(num){
        if(num <= 1){
            return 1;
        }else{
            // 严格模式下访问 callee 会导致错误
            return num * arguments.callee(num -1);// 解除了函数体内的代码与函数名的耦合状态了
        }
    }
    // 
    var trueFactorial = factorial; //实际上是在另一个位置上保存了一个函数的指针。
    factorial = function(){
        return 0;
    }

    alert(trueFactorial(5)); //120
    alert(factorial(5)); // 0
```

//=== this
        // 在调用函数前，this的值并不确定，因此 this 可能会在代码执行过程中引用不同的对象。
        window.color = 'red';
        var o = {
            color: 'blue'
        }
        function sayColor(){
            alert(this.color);
        }
        // 函数的名字仅仅是一个包含指针的变量而已.
        o.sayColor = sayColor;
        o.sayColor();
        // 即使在不同的环境中执行，全局的 sayColor() 函数与 o.sayColor() 指向的仍然是同一个函数
        // 只是执行作用域不同

//    ==========

/*函数属性和方法*/
        // 每个函数都包含两个非继承而来的方法：apply() 和 call()
        // 用途：在特定的作用域中调用函数，实际等于设置函数体内this对象的值。
        // apply(运行函数的作用域, 参数数组)
        // call(运行函数的作用域, 参数列表)

```
    window.color = 'red';
    var o = {
        color: 'blue'
    };
    function sayColor(){
        alert(this.color);
    }
    sayColor();
    sayColor.call(this);
    sayColor.call(window);
    sayColor.call(o);
    // 使用call 或 apply 来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系

    // ==== bind() 创建一个函数的实例，其 this的值会被绑定到传给 bind() 函数的值
    window.color = 'red';
    var o = {
        color: 'blue'
    }
    function sayColor(){
        alert(this.color);
    }
    var objectSayColor = sayColor.bind(o);
    objectSayColor(); // blue
```