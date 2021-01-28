
**目录**

---
- [JavaScript](#javascript)
  - [Function类型](#function类型)
  - [传递参数](#传递参数)
  - [检测类型](#检测类型)
    - [typeof obj === 'object'判断obj是对象的弊端？如何改进？](#typeof-obj--object判断obj是对象的弊端如何改进)
  - [垃圾清除](#垃圾清除)
  - [数据属性和访问器属性](#数据属性和访问器属性)
  - [对象和构造函数](#对象和构造函数)
  - [继承](#继承)
  - [闭包](#闭包)
  - [FormData 文件上传](#formdata-文件上传)
  - [切割字符串](#切割字符串)
  - [深拷贝与浅拷贝](#深拷贝与浅拷贝)
  - [for……in和for……of](#forin和forof)
- [Css](#css)
  - [BFC](#bfc)
  - [圣杯布局与双飞翼布局](#圣杯布局与双飞翼布局)
    - [圣杯布局](#圣杯布局)
    - [双飞翼布局](#双飞翼布局)
- [Vue](#vue)
- [Http](#http)
  - [三次握手和四次挥手](#三次握手和四次挥手)
- [Browser](#browser)
  - [浏览器渲染](#浏览器渲染)
    - [工作流程](#工作流程)
    - [回流和重绘](#回流和重绘)
    - [性能优化策略](#性能优化策略)
- [Notes](#notes)
  - [滑动穿透事件](#滑动穿透事件)
---


# JavaScript
## Function类型
ECMAScript中的函数是对象，因此函数也有属性和方法。每个函数都包含两个属性：length和prototype。其中，length属性表示函数希望接收的命名参数的个数

每个函数都包含两个非继承而来的方法：apply()和call()。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内this对象的值。

apply()方法接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是Array的实例，也可以是arguments对象。

call()需要将参数列举出来

## 传递参数
所有函数的参数都是按值传递的
```javascript
function setName(obj){
    obj.name = 'nike1'
    obj = new Object()
    obj.name = 'nike2'
}
var person = new Object()
setName(person)
console.log(person.name)//nike1
```
## 检测类型
typeof操作符是确定一个变量是字符串、数值、布尔值，还是undefined的最佳工具，变量为对象或者null,都会返回object。

根据规定，所有引用类型的值都是Object的实例。因此，在检测一个引用类型值和Object构造函数时，instanceof操作符始终会返回true。当然，如果使用instanceof操作符检测基本类型的值，则该操作符始终会返回false，因为基本类型不是对象。

### typeof obj === 'object'判断obj是对象的弊端？如何改进？
```javascript
var  obj = {};
var  arr = [];
var funcInstance = new (function (){});  
var isNull = null;
 
console.log(typeof obj === 'object');  //true
console.log(typeof arr === 'object');  //true
console.log(typeof funcInstance === 'object');  //true
console.log(typeof isNull === 'object');    // true
 
// constructor
({}).constructor === Object;  //true
([]).constructor === Array;  //true
 
// instanceof
({}) instanceof Object;  //true
([]) instanceof Array;   //true
 
// toString: 将当前对象以字符串的形式返回
console.log(Object.prototype.toString.call(obj));  //[object Object]
console.log(Object.prototype.toString.call(arr));  //[object Array]
console.log(Object.prototype.toString.call(null));  //[object Null]
```
## 垃圾清除
- 标记清除
 
    垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记（当然，可以使用任何标记方式）。然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后，垃圾收集器完成内存清除工作，销毁那些带标记的值并回收它们所占用的内存空间。
- 引用计数

    当声明了一个变量并将一个**引用类型**值赋给该变量时，则这个值的引用次数就是1。如果同一个值又被赋给另一个变量，则该值的引用次数加1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数减1。当这个值的引用次数变成0时，则说明没有办法再访问这个值了，因而就可以将其占用的内存空间回收回来。这样，当垃圾收集器下次再运行时，它就会释放那些引用次数为零的值所占用的内存。

    问题：循环引用，循环引用指的是对象A中包含一个指向对象B的指针，而对象B中也包含一个指向对象A的引用。
    ```javascript
    function problem(){
        var a = new Object()
        var b = new Object()
        a.name1 = b
        b.name2 = a
        //解决 
        //a.name1 = null b.name2 = null
    }
    ```

    IE9把BOM和DOM对象都转换成了真正的JavaScript对象。这样，就避免了两种垃圾收集算法并存导致的问题，也消除了常见的内存泄漏现象。

    解除变量的引用不仅有助于消除循环引用现象，而且对垃圾收集也有好处。为了确保有效地回收内存，应该及时解除不再使用的全局对象、全局对象属性以及循环引用变量的引用。
## 数据属性和访问器属性
- [[Configurable]]：表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为true。
- [[Enumerable]]：表示能否通过for-in循环返回属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为true。
-  [[Writable]]：表示能否修改属性的值。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为true。
-  [[Value]]：包含这个属性的数据值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。这个特性的默认值为undefined。

Object.defineProperty()方法。这个方法接收三个参数：属性所在的对象、属性的名字和一个描述符对象。其中，描述符（descriptor）对象的属性必须是：configurable、enumerable、writable和value。设置其中的一或多个值，可以修改对应的特性值
```javascript
var person = {}
Object.defineProperty(person,’name’,{
    Writable:false,
    Value:'nike'
})
console.log(person.name)//nike
person.name = 'kkk'
console.log(person.name)//nike
```
configurable设置为false, 把属性定义为不可配置的，就不能再把它变回可配置, 再调用Object.defineProperty()方法修改除writable之外的特性，都会导致错误

调用Object.defineProperty()方法时，如果不指定，configurable、enumerable和writable特性的默认值都是false

## 对象和构造函数
- 工厂模式（可以创建多个相似对象，但却没有解决对象识别的问题即对象的类型）
```javascript
function createPerson(name,age){
    var o = new Object()
    o.name = name
    o.age = age
    o.sayName = function(){
        console.log(this.name)
    }
    return o
}
var person =  createPerson('jack','12')
```
- 构造函数
  - 优点：可以将实例标识为一种特性的类型
  - 缺点：每个方法都要在每个实例上重新创建一遍
- 构造函数创建实例过程
  - 创建一个新对象
  - 将构造函数的作用域赋给新对象（因此this指向此对象）
  - 执行构造函数中的代码（为新对象添加属性）
  - 返回新对象
```javascript
function Person(name,age){
    this.name = name
    this.age = age
    this.sayName = function(){
        console.log(this.name)
    }
}
var person =  new Person('jack','12')

//person instanceof Object//true
//person instanceof Person//true
```

- 原型模式
```javascript
function Person(){}
Person.prototype.name = 'jack'
Person.prototype.age = '12'
Person.prototype.sayName = function(){
    console.log(this.name)
}
var person =  new Person()
console.log(person.sayName())//jack
```
只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个prototype属性，这个属性指向函数的原型对象。在默认情况下，所有原型对象都会自动获得一个constructor（构造函数）属性，这个属性是一个指向prototype属性所在函数的指针

创建了自定义的构造函数之后，其原型对象默认只会取得constructor属性；至于其他方法，则都是从Object继承而来的。当调用构造函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象。

所有实现中都无法访问到[[Prototype]]（Firefox、Safari和Chrome在每个对象上都支持一个属性__proto__），但可以通过isPrototypeOf()方法来确定对象之间是否存在这种关系。从本质上讲，如果[[Prototype]]指向调用isPrototypeOf()方法的对象（Person.prototype），那么这个方法就返回true

存在问题：所有实例在默认情况下都将取得相同的属性值，某一实例修改引用类型属性值会影响其他实例
```javascript
person.__proto__ == Person.prototype
person.prototype.isPrototypeOf(person1) //true

Object.getPrototypeOf()//返回[[Prototype]]的值
Object.getPrototypeOf(person1).name //'jack'访问到name值

//使用hasOwnProperty()方法可以检测一个属性是存在于实例中，还是存在于原型中

Object.getOwnPropertyDescriptor()//用于实例属性取得原型属性的描述符
```
- 原型与in操作符

在单独使用时，in操作符会在通过对象能够访问给定属性时返回true

在使用for-in循环时，返回的是所有能够通过对象访问的、可枚举的（enumerated）属性，其中既包括存在于实例中的属性，也包括存在于原型中的属性

Object.keys()方法。这个方法接收一个对象作为参数，返回一个包含所有可枚举属性的字符串数组

得到所有实例属性，无论它是否可枚举，都可以使用Object.getOwnPropertyNames()方法
```javascript
var person1 = new Person()
person1.name = 'jack'
person1.age = '12'
console.log(Object.keys(person1))//name,age
```
- 创建自定义类型
  - 组合构造函数和原型模式
    ```javascript
    //1.每个实例都会有自己的一份实例属性的副本
    //2.共享方法的引用
    //3.最大限度地节省了内存
    //4.支持向构造函数传递参数
    function Person(name,age){
        this.name = name
        this.age = age
    }
    Person.prototype.sayName = function(){
        console.log(this.name)
    }
    var person =  new Person('jack','12')
    person.sayName()//jack
    ```
  - 动态原型模式
    ```javascript
    //可以通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型
    function Person(name,age){
        this.name = name
        this.age = age
        if(typeof this.sayName != 'funciton'){
            Person.prototype.sayName = function(){
                console.log(this.name)
            }
        }
    }
    Person.prototype = function(){
        console.log(this.name)
    }
    var person =  new Person('jack','12')
    person.sayName()//jack
    ```
  - 寄生构造函数模式
    ```javascript
    //不能依赖instanceof操作符来确定对象类型
    function Person(name,age){
        var o = new Object()
        o.name = name
        o.age = age
        o.sayName = function(){
            console.log(this.name)//jack
        }
    }
    var person =  new Person('jack','12')
    person.sayName()//jack
    ```
  - 稳妥构造函数模式
    ```javascript
    //安全
    //不能依赖instanceof操作符来确定对象类型
    function Person(name,age){
        var o = new Object()
        o.sayName = function(){
            console.log(name)//jack
        }
    }
    var person = Person('jack','12')
    person.sayName()
    ```
## 继承
- 原型链
    ```javascript
    function Person(){
        this.person = 'person'
    }
    Person.prototype.getPersonName = function(){
        console.log(this.person)
    }
    function Friend(){
        this.friend = 'friend'
    }
    var friend = new Friend()

    Friend.prototype = person//重写原型对象

    Friend.prototype.getFriendName = function(){
        console.log(this.friend)
    }
    var one = new Friend()
    one.getPersonName()//person

    //one.constructor指向Person，Friend.prototype被重写

    //所有函数的默认原型都是Object的实例，默认原型都会包含一个内部指针，指向Object.prototype。这也正是所有自定义类型都会继承toString()、valueOf()等默认方法的根本原因
    ```
    - 确定原型和实例之间的关系
        - instanceof测试实例与原型链中出现过的构造函数
         
            one instanceof (Object||Person||Friend) //true
        - isPrototypeOf()原型链中出现过的原型，都可以说是该原型链所派生的实例的原型

            (Object||Person||Friend).prototype.isPrototypeOf(one)//true
    - 原型链的问题
      - 引用类型值的共享
      - 在创建子类型的实例时，不能向父类型的构造函数中传递参数
      - 破坏子类型的原型链，constructor指向
- 借用构造函数（在子类型构造函数的内部调用父类型构造函数）
 
  解决原型中包含引用类型值所带来问题的过程
    ```javascript
    function Person(name){
        this.name = name
    }
    function Friend(){
        Person.call(this,'jack')
        this.age = '12'
    }
    var one = new Friend()
    console.log(one.name)//jack
    console.log(one.age)//12
    ```

    - 问题
        - 方法都在构造函数中定义，复用性差
        - 父类型的原型中定义的方法，对子类型而言也是不可见
- 组合继承（伪经典继承）
  
  使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承,避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为JavaScript中最常用的继承模式。而且，instanceof和isPrototypeOf()也能够用于识别基于组合继承创建的对象。

  无论什么情况下，都会调用两次父类型构造函数：一次是在创建子类型原型的时候，另一次是在子类型构造函数内部。
    ```javascript
    function Person(name){
        this.name = name
        this.colors = ['red','green','yellow']
    }
    Person.prototype.sayName = function(){
        console.log(this.name)
    }

    function Friend(name,age){
        Person.call(this,name)
        this.age = age
    }
    Friend.prototype = new Person()
    Friend.prototype.constructor = Friend
    Friend.prototype.sayAge = function(){
        console.log(this.age)
    }

    var one1 = new Friend('jack','12')
    one1.colors.push('black')
    console.log(one1.colors)//['red','green','yellow','black']
    one1.sayName()//jack
    one1.sayAge()//12

    var one2 = new Friend('ggg','10')
    console.log(one2.colors)//['red','green','yellow']
    one2.sayName()//ggg
    one2.sayAge()//10
    ```
- 原型式继承
  
  必须有一个对象可以作为另一个对象的基础

  适用于想让一个对象与另一个对象保持类似，不必创建构造函数

  Object.create()方法的第二个参数与Object.defineProperties()方法的第二个参数格式相同：每个属性都是通过自己的描述符定义的。以这种方式指定的任何属性都会覆盖原型对象上的同名属性。

  引用类型会共享值
  ```javascript
    //object()对传入其中的对象执行了一次浅复制
    function Object(o){
        function F(){}
        F.prototype = o
        return o
    }//Object.create

    var person = {
        name:'jack',
        friends:['a','b','c']
    }
    var personOne = Object.create(person)
    // 等价 var personOne = Object(person)
    personOne.name = 'mark'
    personOne.friends.push('d')

    var personTwo = Object.create(person,{
        name:{
            value:'hahaha'
        }
    })
    var personTwo = Object.create(person)
    personTwo.name = 'john'
    personTwo.friends.push('e')
    console.log(person.friends)//['a','b','c','d','e']
  ```
- 寄生式继承

  主要考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式

  使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率；这一点与构造函数模式类似。
  
  ```javascript
    //object()对传入其中的对象执行了一次浅复制
    function object(o){
        function F(){}
        F.prototype = o
        return o
    }

    function createPerson(o){
        var clone = object(o)
        clone.sayHi = function(){
            console.log('hi')
        }
        return clone
    }

    var person = {
        name:'jack',
        friends:['a','b','c']
    }
    var another = createPerson(person)
    another.sayHi()//hi
  ```
- 寄生组合式继承
  
  通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。
  
  基本思路是：不必为了指定子类型的原型而调用父类型的构造函数，我们所需要的无非就是父类型原型的一个副本而已。本质上，就是使用寄生式继承来继承父类型的原型，然后再将结果指定给子类型的原型

  避免了在Person.prototype上面创建不必要的、多余的属性,原型链保持不变。
  ```javascript
    //Object()对传入其中的对象执行了一次浅复制
    function Object(o){
        function F(){}
        F.prototype = o
        return o
    }
    function inheritPrototype(Person,Friend){
        var newObj = Object(Person.prototype) //复制父类Person的原型对象
        newObj.constructor = Friend //constructor指向子类构造函数
        Friend.prototype = newObj //再把这个对象给子类的原型对象
    }

    function Person(name){
        this.name = name
        this.colors = ['red','green','yellow']
    }
    Person.prototype.sayName = function(){
        console.log(this.name)
    }

    function Friend(name,age){
        Person.call(this,name)
        this.age = age
    }
    inheritPrototype(Person,Friend)
    Friend.prototype.sayAge = function(){
        console.log(this.age)
    }
  ```
## 闭包

闭包是指有权访问另一个函数作用域中的变量的函数

当某个函数被调用时，会创建一个执行环境和作用域链。然后使用arguments和其它命名参数的值来初始化函数的活动对象。但在作用域链中，外部函数的活动对象始终处于第二位，外部函数的外部函数的活动对象处于第三位，……直至作为作用域链终点的全局执行环境。

```javascript
    function parent(name){
        return function(obj1,obj2){
            var value1 = obj1[name]
            var value2 = obj2[name]
            if(value1 < value2){
                return 1
            }else{
                return 2
            }
        }
    }

    function compare(obj1,obj2){
        var value1 = obj1[name]
        var value2 = obj2[name]
        if(value1 < value2){
            return 1
        }else{
            return 2
        }
    }
```
当创建compare函数时，会创建预先包含全局变量对象的作用域链，作用域链被保存在[[Scope]]属性中。

当执行函数时，会为函数创建一个执行环境，然后复制函数[[Scope]]属性中的对象构建执行环境的作用域链。

此后，又有一个活动对象（在此作为变量对象使用）被创建并被推入执行环境作用域链的前端。

对于这个例子中compare()函数的执行环境而言，其作用域链中包含两个变量对象：本地活动对象和全局变量对象。显然，作用域链本质上是一个指向变量对象的指针列表，它只引用但不实际包含变量对象。

无论什么时候在函数中访问一个变量时，就会从作用域链中搜索具有相应名字的变量。一般来讲，当函数执行完毕后，局部活动对象就会被销毁，内存中仅保存全局作用域（全局执行环境的变量对象）。但是，闭包的情况又有所不同。

parent()内创建的匿名函数会将parent()的活动对象添加到匿名函数的作用域链中，在匿名函数被返回后，作用域链初始化为parent()的活动对象和全局变量对象。parent()执行完毕后,其活动对象也不会被销毁，因为匿名函数的作用域链仍然在引用这个活动对象。换句话说，当parent()函数返回后，其执行环境的作用域链会被销毁，但它的活动对象仍然会留在内存中；直到匿名函数被销毁后，parent()的活动对象才会被销毁。

闭包会导致内存泄漏，需要手动释放

模仿块级作用域（函数立即执行表达式）可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。只要函数执行完毕，就可以立即销毁其作用域链了。//(function(){ })()

应用场景
- 访问函数内部参数
- 变量永久保存
- 函数在执行前要为执行的函数提供具体参数
```javascript
var compareName = parent('name')
/*此时compareName = function(obj1,obj2){
                        var value1 = obj1[name]
                        var value2 = obj2[name]
                        if(value1 < value2){
                            return 1
                        }else{
                            return 2
                        }
                    }
*/
var result = compareName({name:1},{name:2})
compareName = null//释放内存
```
## FormData 文件上传
```javascript
document.getElementById("upJS").onclick = function() {
    /* FormData是表单数据类 */
    Var fd = new FormData();
    var ajax = new XMLHttpRequest();
    fd.append("upload", 1);
    /* 把文件添加到表单里 */
    fd.append("upfile", document.getElementById("upfile").files[0]);
    ajax.open("post", "test.php", true);  //true异步提交

    ajax.onload = function () {
        console.log(ajax.responseText);
    };
    ajax.send(fd);
    /*如果是post请求，那么在调用send方法之前，要设置请求头。
    xhr.setRequestHeader("Content-type","Application/x-www-form-urlencoded");*/
}

$('#upJQuery').on('click', function() {
    varfd = new FormData();
    fd.append("upload", 1);
    fd.append("upfile", $("#upfile").get(0).files[0]);
        $.ajax({
        url: "test.php",
        type: "POST",
        processData: false,//不处理发送的数据，因为data值是FormData对象，不需要对数据做处理,默认为true,会将发送的数据序列化以适应默认的内容类型application/x-www-form-urlencoded
        contentType: false,//不设置Content-type请求头  
        data: fd,
        success: function(d) {
            console.log(d);
        }
    });
});
```
## 切割字符串
- slice从已有的数组中返回选定的元素
  ```javascript
  'abcde'.slice(1,3);//bc			
  'abcde'.slice(1,-1);//bcd
  ```
- split把一个字符串分割成字符串数组
  ```javascript
  //参数2为返回数组长度
  "abcdef".split("c"); //['ab','def']		
  "abcdef".split("c",1); //['ab']
  ```
- substr在字符串中抽取从start下标开始的指定数目的字符
  ```javascript
  //参数2为长度
  'abcde'.substr(1,2); //bc  
  ```
- substring提取字符串中介于两个指定下标之间的字符
  ```javascript
  //参数均为非负整数
  'abcde'.substring(1,3) //bc
  ```
## 深拷贝与浅拷贝
- Object.assign()//嵌套对象浅拷贝，非嵌套为深拷贝
- JSON.stringify()//破坏原型链，且无法拷贝属性值为function和RegExp
- concat()、slice()//只能是一维数组，内部为引用类型则还是浅拷贝
- 递归拷贝
  ```javascript
  var json1 = {"name":"shauna","age":18,"arr1":[1,2,3,4,5],"string":'got7',"arr2":[1,2,3,4,5],"arr3":[{"name1":"shauna"},{"job":"web"}]};
  var json2 = {};
  function copy(obj1,obj2){
    var obj2 = obj2 || {};
    for(var name in obj1){
        if(typeof obj1[name] === "object"){ 
            obj2[name] = (obj1[name].constructor === Array) ? [] : {}; 
            copy(obj1[name],obj2[name]); 
        }else{
            obj2[name] = obj1[name];  
        }
    }
    return obj2;
  }
  json2 = copy(json1,json2)
  ```
## for……in和for……of
- for……in
    - 循环输出key
    - 可以遍历自定义属性
    - 遍历可枚举属性，包括原型
- for……of
    - 循环输出value
    - 可通过Object.key()遍历普通对象
    ```javascript
    var student={
        name:'wujunchuan',
        age:22,
        locate:{
            country:'china',
            city:'xiamen',
            school:'XMUT'
        }
    }
    for(var key of Object.keys(student)){
        //使用Object.keys()方法获取对象key的数组
        console.log(key+": "+student[key]);
    }// name: wujunchuan    age: 22    locate: [object Object]
    ```
# Css
## BFC
BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

BFC的布局规则：
- 内部的Box会在垂直方向，一个接一个地放置。
- Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。
- 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
- BFC的区域不会与float box重叠。
- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
- 计算BFC的高度时，浮动元素也参与计算。

形成BFC的条件：
- float除none以外
- 绝对定位元素（absolute，fixed）
- display为以下之一inline-block，table-cell，table-captions，flex，inline-flex
- overflow：除visible以外（auto，hidden，scroll）
  
场景应用：
- 自适应两栏布局（规则1,4）
- 清除内部浮动（规则6）
- 防止垂直margin重叠（规则2）
## 圣杯布局与双飞翼布局
圣杯布局和双飞翼布局解决的问题是相同的，就是两边顶宽，中间自适应的三栏布局，中间栏要在放在文档流前面以优先渲染。
### 圣杯布局
优点：不需要添加dom节点

缺点：圣杯布局的缺点：正常情况下是没有问题的，但是特殊情况下就会暴露此方案的弊端，如果将浏览器无线放大时，「圣杯」将会「破碎」掉。如图：当middle部分的宽小于left部分时就会发生布局混乱。（middle<left即会变形）
```html
<html>
	<head>
        <style>
            #container {
                height: 100%;
                padding-left: 200px; 
                padding-right: 150px;
                background-color: gray;
            }
            #container .column {
                float: left;
                height: 100%;
            }
            #center {
                background-color: red;
                width: 100%;
            }
            #left {
                background-color: yellow;
                width: 200px; 
                margin-left: -100%;
                position: relative;
                left: -200px;
            }
            #right {
                background-color: green;
                width: 150px; 
                margin-left: -150px;
                position: relative;
                right: -150px;
            }
    </style>
	</head>
	<body class="">
        <div id="container">
            <div id="center" class="column">中间</div>
            <div id="left" class="column">左侧</div>
            <div id="right" class="column">右侧</div>
        </div>
	</body>

</html>
```
### 双飞翼布局
优点：不会像圣杯布局那样变形

缺点：多加了一层dom节点
```html
<!DOCTYPE>
<html>
	<head>
		<title></title>
        <style>
            body {
                min-width: 500px;
            }
            .column {
                float: left;
                height: 100%;
            }
            #container {
                width: 100%;
                background-color: gray;
                height: 100%;
            }
            #center {
                background-color: red;
                margin-left: 200px;
                margin-right: 150px;
                height: 100%;
            }
            #left {
                background-color: yellow;
                width: 200px; 
                margin-left: -100%;
            }
            #right {
                background-color: green;
                width: 150px; 
                margin-left: -150px;
            }
    </style>
	</head>
	<body>
        <div id="container"  class="column">
            <div id="center">中间</div>
        </div>
        <div id="left" class="column">左侧</div>
        <div id="right" class="column">右侧</div>
	</body>
</html>
```
# Vue
# Http
## 三次握手和四次挥手
- 客户端发送syn请求。并包含自己的初始序号a
- 服务端收到syn后会回复一个的syn，同时包含对上个a回复的ack，回应的序号是希望收到下一个包的序号a+1，还有自己的初始序号b
- 客户端收到回应的syn后，回复一个ack回应，其中包含了下一个希望收到的序号b+1

- 客户端提出关闭请求发送一个fin，序号为a
- 服务器收到fin，并返回一个ack，序号为a+1
- Tcp服务器还会发送一个文件结束符，然后服务器关闭连接，tcp端发送一个fin
- 客户端发送确认，并将序列号设置为收到的序号加1

当Server端收到Client端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时，当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到我Server端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送。故需要四步握手。

# Browser
## 浏览器渲染
### 工作流程
构建DOM->构建CSSOM->构建渲染树->布局->绘制

CSSOM会阻塞渲染，只有当CSSOM构建完毕后才会进入下一个阶段构建渲染树
### 回流和重绘
1. 重绘：对dom修改导致样式变化，未影响集合属性（位置、尺寸），浏览器不需要重新计算，直接绘制行的样式
2. 回流：改变了几何属性，将计算的结果重新绘制
   
   触发回流的条件：
   - 添加或者删除可见的DOM元素
   - 元素尺寸改变（边距、填充、边框、宽高）
   - 内容变化（eg：input输入文字）
   - 浏览器窗口尺寸改变（resize事件）
   - 计算offsetWidth和offsetHeight属性
   - 设置style属性的值
  
   如何减少回流和重绘：
   - 使用transform替代top
   - 使用visibility替换display：none
   - 不把节点的属性值放在循环里当成循环里面的变量
   For(){console.log(document……。offsettop)} offsettop获取正确的值导致回流
   - 不使用table布局，小改动会导致整个table布局
   - 动画实现速度的选择，速度越快回流越多，可以使用requestAnimationFrame
   - Css选择符从右往左匹配查找，避免节点层级过多
   - 将频繁重绘回流的节点设置为图层，图层可以阻止该节点渲染行为影响别的节点（如video标签，浏览器会自动将该节点变为图层）

### 性能优化策略
- css优化

    link标签的rel属性中属性值设置为preload能够让HTML页面中可以指明哪些资源是在页面加载完成后即刻需要的，足以有的配置加载顺序，提高渲染性能。

- js优化
  
    script标签加上defer属性和async属性用于在不阻塞页面文档解析的前提下，控制脚本的下载和执行
    ![](https://github.com/LiuYJia/DailyNotes/blob/main/images/defer_async.png "defer_async")

# Notes
## 滑动穿透事件
禁用body的滚动条，由于滚动条的位置会丢失，所以需要在展示弹窗之前保存滚动条的位置，隐藏弹窗时恢复滚动条的位置。
```javascript
.modal-open {
    position:fixed;
    height: 100%;
}   
var ModalHelper = (function(bodyCls) {
    var scrollTop;
    return {
        afterOpen: function() {
            scrollTop = document.scrollingElement.scrollTop;
            document.body.classList.add(bodyCls);
            document.body.style.top = -scrollTop + 'px';
        },
        beforeClose: function() {
            document.body.classList.remove(bodyCls);
            document.scrollingElement.scrollTop = scrollTop;
        }
    };
})('modal-open');
```
