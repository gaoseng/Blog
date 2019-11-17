# 原型
## 什么是原型
    每个javascript对象(除了null)创建的时候就会产生与之关联的另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型中'继承'属性与方法;
## 词法作用域与动态作用域
    js采用的是词法作用域，作用域在函数定义时就决定了。
    而词法作用域相对的是动态作用域，函数的作用域是在函数被调用时决定的。

    ```bash
    var scope = "global scope";
    function checkscope(){
        var scope = "local scope";
        function f(){
            return scope;
        }
        return f;
    }
    checkscope()();
    ```

    ```bash
    var scope = "global scope";
    function checkscope(){
        var scope = "local scope";
        function f(){
            return scope;
        }
        return f;
    }
    checkscope()();
    ```
    


