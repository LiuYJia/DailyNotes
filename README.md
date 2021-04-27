
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
  - [js question](#js-question)
    - [输出是什么？](#输出是什么)
    - [输出是什么？](#输出是什么-1)
    - [10. 当我们这么做时，会发生什么？](#10-当我们这么做时会发生什么)
    - [12. 输出是什么？](#12-输出是什么)
    - [15. 输出是什么？](#15-输出是什么)
    - [17. 输出是什么？](#17-输出是什么)
    - [输出是什么？](#输出是什么-2)
    - [输出是什么？](#输出是什么-3)
    - [输出是什么？](#输出是什么-4)
    - [输出是什么？](#输出是什么-5)
    - [输出是什么？](#输出是什么-6)
    - [输出是什么?](#输出是什么-7)
    - [返回值是什么?](#返回值是什么)
  - [</details>](#details)
    - [输出是什么?](#输出是什么-8)
    - [`num`的值是什么?](#num的值是什么)
    - [输出是什么?](#输出是什么-9)
    - [输出是什么?](#输出是什么-10)
    - [输出什么?](#输出什么)
    - [如何能打印出`console.log`语句后注释掉的值？](#如何能打印出consolelog语句后注释掉的值)
    - [输出什么?](#输出什么-1)
    - [输出什么?](#输出什么-2)
    - [输出什么?](#输出什么-3)
    - [输出什么?](#输出什么-4)
    - [输出什么?](#输出什么-5)
    - [<a name=20190817></a>输出什么?](#输出什么-6)
    - [输出什么?](#输出什么-7)
    - [输出什么?](#输出什么-8)
    - [输出什么?](#输出什么-9)
    - [结果是什么?](#结果是什么)
    - [输出什么?](#输出什么-10)
          - [88. 输出什么?](#88-输出什么)
      - [答案: B](#答案-b)
    - [输出什么?](#输出什么-11)
    - [输出什么?](#输出什么-12)
    - [输出什么?](#输出什么-13)
    - [输出什么?](#输出什么-14)
    - [输出什么？](#输出什么-15)
    - [输出什么？](#输出什么-16)
    - [输出什么？](#输出什么-17)
    - [我们怎样才能在 `index.js` 中调用 `sum.js?` 中的 `sum`？](#我们怎样才能在-indexjs-中调用-sumjs-中的-sum)
    - [输出什么？](#输出什么-18)
    - [以下哪一项会对对象 `person` 有副作用？](#以下哪一项会对对象-person-有副作用)
    - [以下哪一项会对对象 `person` 有副作用？](#以下哪一项会对对象-person-有副作用-1)
    - [输出什么？](#输出什么-19)
    - [我们需要向对象 `person` 添加什么，以致执行 `[...person]` 时获得形如 `["Lydia Hallie", 21]` 的输出？](#我们需要向对象-person-添加什么以致执行-person-时获得形如-lydia-hallie-21-的输出)
    - [输出是什么？](#输出是什么-11)
    - [输出什么?](#输出什么-20)
    - [输出什么?](#输出什么-21)
    - [输出什么?](#输出什么-22)
    - [哪个作为`method`的值可以打印`{ name: "Lydia", age: 22 }`?](#哪个作为method的值可以打印-name-lydia-age-22-)
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
- [微信小程序](#微信小程序)
  - [基础信息](#基础信息)
  - [icon组件](#icon组件)
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
    var fd = new FormData();
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
## js question
### 输出是什么？
```javascript
function sayHi() {
  console.log(name)
  console.log(age)
  var name = 'Lydia'
  let age = 21
}

sayHi()
```

- A: `Lydia` 和 `undefined`
- B: `Lydia` 和 `ReferenceError`
- C: `ReferenceError` 和 `21`
- D: `undefined` 和 `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: D

在函数内部，我们首先通过 `var` 关键字声明了 `name` 变量。这意味着变量被提升了（内存空间在创建阶段就被设置好了），直到程序运行到定义变量位置之前默认值都是 `undefined`。因为当我们打印 `name` 变量时还没有执行到定义变量的位置，因此变量的值保持为 `undefined`。

通过 `let` 和 `const` 关键字声明的变量也会提升，但是和 `var` 不同，它们不会被<i>初始化</i>。在我们声明（初始化）之前是不能访问它们的。这个行为被称之为暂时性死区。当我们试图在声明之前访问它们时，JavaScript 将会抛出一个 `ReferenceError` 错误。

</p>
</details>

---
### 输出是什么？

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor
    return this.newColor
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor
  }
}

const freddie = new Chameleon({ newColor: 'purple' })
freddie.colorChange('orange')
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details><summary><b>答案</b></summary>
<p>

答案: D

`colorChange` 是一个静态方法。静态方法被设计为只能被创建它们的构造器使用（也就是 `Chameleon`），并且不能传递给实例。因为 `freddie` 是一个实例，静态方法不能被实例使用，因此抛出了 `TypeError` 错误。

</p>
</details>

---

### 10. 当我们这么做时，会发生什么？

```javascript
function bark() {
  console.log('Woof!')
}

bark.animal = 'dog'
```

- A: 正常运行!
- B: `SyntaxError`. 你不能通过这种方式给函数增加属性。
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: A

这在 JavaScript 中是可以的，因为函数是对象！（除了基本类型之外其他都是对象）

函数是一个特殊的对象。你写的这个代码其实不是一个实际的函数。函数是一个拥有属性的对象，并且属性也可被调用。

</p>
</details>

---
### 12. 输出是什么？

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName
  this.lastName = lastName
}

const lydia = new Person('Lydia', 'Hallie')
const sarah = Person('Sarah', 'Smith')

console.log(lydia)
console.log(sarah)
```

- A: `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`
- B: `Person {firstName: "Lydia", lastName: "Hallie"}` and `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Lydia", lastName: "Hallie"}` and `{}`
- D:`Person {firstName: "Lydia", lastName: "Hallie"}` and `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: A

对于 `sarah`，我们没有使用 `new` 关键字。当使用 `new` 时，`this` 引用我们创建的空对象。当未使用 `new` 时，`this` 引用的是**全局对象**（global object）。

我们说 `this.firstName` 等于 `"Sarah"`，并且 `this.lastName` 等于 `"Smith"`。实际上我们做的是，定义了 `global.firstName = 'Sarah'` 和 `global.lastName = 'Smith'`。而 `sarah` 本身是 `undefined`。

</p>
</details>

---
### 15. 输出是什么？

```javascript
function sum(a, b) {
  return a + b
}

sum(1, '2')
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

<details><summary><b>答案</b></summary>
<p>

答案: C

JavaScript 是一种**动态类型语言**：我们不指定某些变量的类型。值可以在你不知道的情况下自动转换成另一种类型，这种类型称为**隐式类型转换**（implicit type coercion）。**Coercion** 是指将一种类型转换为另一种类型。

在本例中，JavaScript 将数字 `1` 转换为字符串，以便函数有意义并返回一个值。在数字类型（`1`）和字符串类型（`'2'`）相加时，该数字被视为字符串。我们可以连接字符串，比如 `"Hello" + "World"`，这里发生的是 `"1" + "2"`，它返回 `"12"`。

</p>
</details>

---
### 17. 输出是什么？

```javascript
function getPersonInfo(one, two, three) {
  console.log(one)
  console.log(two)
  console.log(three)
}

const person = 'Lydia'
const age = 21

getPersonInfo`${person} is ${age} years old`
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details><summary><b>答案</b></summary>
<p>

答案: B

如果使用标记模板字面量，第一个参数的值总是包含字符串的数组。其余的参数获取的是传递的表达式的值！

</p>
</details>

---
### 输出是什么？

```javascript
const a = {}
const b = { key: 'b' }
const c = { key: 'c' }

a[b] = 123
a[c] = 456

console.log(a[b])
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: B

对象的键被自动转换为字符串。我们试图将一个对象 `b` 设置为对象 `a` 的键，且相应的值为 `123`。

然而，当字符串化一个对象时，它会变成 `"[object Object]"`。因此这里说的是，`a["[object Object]"] = 123`。然后，我们再一次做了同样的事情，`c` 是另外一个对象，这里也有隐式字符串化，于是，`a["[object Object]"] = 456`。

然后，我们打印 `a[b]`，也就是 `a["[object Object]"]`。之前刚设置为 `456`，因此返回的是 `456`。

</p>
</details>

---
### 输出是什么？

```javascript
const numbers = [1, 2, 3]
numbers[10] = 11
console.log(numbers)
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: C

当你为数组设置超过数组长度的值的时候， JavaScript 会创建名为 "empty slots" 的东西。它们的值实际上是 `undefined`。你会看到以下场景：

`[1, 2, 3, 7 x empty, 11]`

这取决于你的运行环境（每个浏览器，以及 node 环境，都有可能不同）

</p>
</details>

---
### 输出是什么？

```javascript
(() => {
  let x, y
  try {
    throw new Error()
  } catch (x) {
    (x = 1), (y = 2)
    console.log(x)
  }
  console.log(x)
  console.log(y)
})()
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: A

`catch` 代码块接收参数 `x`。当我们传递参数时，这与之前定义的变量 `x` 不同 。这个 `x` 是属于 `catch` 块级作用域的。

然后，我们将块级作用域中的变量赋值为 `1`，同时也设置了变量 `y` 的值。现在，我们打印块级作用域中的变量 `x`，值为 `1`。

`catch` 块之外的变量 `x` 的值仍为 `undefined`， `y` 的值为 `2`。当我们在 `catch` 块之外执行 `console.log(x)` 时，返回 `undefined`，`y` 返回 `2`。

</p>
</details>

---
### 输出是什么？

```javascript
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
//必需。初始值, 上次调用函数的返回值。
//必需。当前元素
//可选。当前元素的索引
//可选。当前元素所属的数组对象。
//可选。传递给函数的初始值
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur)
  },
  [1, 2]
)
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

<details><summary><b>答案</b></summary>
<p>

答案: C

`[1, 2]`是初始值。初始值将会作为首次调用时第一个参数 `acc` 的值。在第一次执行时， `acc` 的值是 `[1, 2]`， `cur` 的值是 `[0, 1]`。合并它们，结果为 `[1, 2, 0, 1]`。
第二次执行， `acc` 的值是 `[1, 2, 0, 1]`， `cur` 的值是 `[2, 3]`。合并它们，最终结果为 `[1, 2, 0, 1, 2, 3]`

</p>
</details>

---
### 输出是什么？

```javascript
[...'Lydia']
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

<details><summary><b>答案</b></summary>
<p>

答案: A

string 类型是可迭代的。扩展运算符将迭代的每个字符映射成一个元素。

</p>
</details>

---

### 输出是什么?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

<details><summary><b>答案</b></summary>
<p>

答案: C

一般的函数在执行之后是不能中途停下的。但是，生成器函数却可以中途“停下”，之后可以再从停下的地方继续。当生成器遇到`yield`关键字的时候，会生成`yield`后面的值。注意，生成器在这种情况下不 _返回_ (_return_ )值，而是 _生成_ (_yield_)值。

首先，我们用`10`作为参数`i`来初始化生成器函数。然后使用`next()`方法一步步执行生成器。第一次执行生成器的时候，`i`的值为`10`，遇到第一个`yield`关键字，它要生成`i`的值。此时，生成器“暂停”，生成了`10`。

然后，我们再执行`next()`方法。生成器会从刚才暂停的地方继续，这个时候`i`还是`10`。于是我们走到了第二个`yield`关键字处，这时候需要生成的值是`i*2`，`i`为`10`，那么此时生成的值便是`20`。所以这道题的最终结果是`10,20`。


</p>
</details>

---

### 返回值是什么?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, "one");
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, "two");
});

Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
Promise.race([firstPromise, secondPromise]).then(res => console.log(res));//['one','two']失败的时候则返回最先被reject失败状态的值
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

<details><summary><b>答案</b></summary>
<p>

答案: B

当我们向`Promise.race`方法中传入多个`Promise`时，会进行 _优先_ 解析。在这个例子中，我们用`setTimeout`给`firstPromise`和`secondPromise`分别设定了500ms和100ms的定时器。这意味着`secondPromise`会首先解析出字符串`two`。那么此时`res`参数即为`two`，是为输出结果。

</p>
</details>
---

### 输出是什么?

```javascript
let person = { name: "Lydia" };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>答案</b></summary>
<p>

答案: D


首先我们声明了一个拥有`name`属性的对象 `person`。

<img src="https://i.imgur.com/TML1MbS.png" width="200">

然后我们又声明了一个变量`members`. 将首个元素赋值为变量`person`。 当设置两个对象彼此相等时，它们会通过 _引用_ 进行交互。但是当你将引用从一个变量分配至另一个变量时，其实只是执行了一个 _复制_ 操作。（注意一点，他们的引用 _并不相同_!）

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

接下来我们让`person`等于`null`。

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

我们没有修改数组第一个元素的值，而只是修改了变量`person`的值,因为元素（复制而来）的引用与`person`不同。`members`的第一个元素仍然保持着对原始对象的引用。当我们输出`members`数组时，第一个元素会将引用的对象打印出来。

</p>
</details>

---

### `num`的值是什么?

```javascript
const num = parseInt("7*6", 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

<details><summary><b>答案</b></summary>
<p>

答案: C

只返回了字符串中第一个字母. 设定了 _进制_ 后 (也就是第二个参数，指定需要解析的数字是什么进制: 十进制、十六机制、八进制、二进制等等……),`parseInt` 检查字符串中的字符是否合法. 一旦遇到一个在指定进制中不合法的字符后，立即停止解析并且忽略后面所有的字符。

`*`就是不合法的数字字符。所以只解析到`"7"`，并将其解析为十进制的`7`. `num`的值即为`7`.

</p>
</details>

---

### 输出是什么?

```javascript
// counter.js
let counter = 10;
export default counter;
```

```javascript
// index.js
import myCounter from "./counter";

myCounter += 1;

console.log(myCounter);
```

- A: `10`
- B: `11`
- C: `Error`
- D: `NaN`

<details><summary><b>答案</b></summary>
<p>

答案: C

引入的模块是 _只读_ 的: 你不能修改引入的模块。只有导出他们的模块才能修改其值。

当我们给`myCounter`增加一个值的时候会抛出一个异常： `myCounter`是只读的，不能被修改。

</p>
</details>

---

### 输出是什么?

```javascript
let num = 10;

const increaseNumber = () => num++;
const increasePassedNumber = number => number++;

const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);

console.log(num1);
console.log(num2);
```

- A: `10`, `10`
- B: `10`, `11`
- C: `11`, `11`
- D: `11`, `12`

<details><summary><b>答案</b></summary>
<p>

答案: A

一元操作符 `++` _先返回_ 操作值, _再累加_ 操作值。`num1`的值是`10`, 因为`increaseNumber`函数首先返回`num`的值，也就是`10`，随后再进行 `num`的累加。

`num2`是`10`因为我们将 `num1`传入`increasePassedNumber`. `number`等于`10`（`num1`的值。同样道理，`++` _先返回_ 操作值, _再累加_ 操作值。） `number`是`10`，所以`num2`也是`10`.

</p>
</details>

---

### 输出什么?

```javascript
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```

- A: `running index.js`, `running sum.js`, `3`
- B: `running sum.js`, `running index.js`, `3`
- C: `running sum.js`, `3`, `running index.js`
- D: `running index.js`, `undefined`, `running sum.js`

<details><summary><b>答案</b></summary>
<p>

答案: B

`import`命令是编译阶段执行的，在代码运行之前。因此这意味着被导入的模块会先运行，而导入模块的文件会后执行。

这是CommonJS中`require（）`和`import`之间的区别。使用`require()`，您可以在运行代码时根据需要加载依赖项。 如果我们使用`require`而不是`import`，`running index.js`，`running sum.js`，`3`会被依次打印。

</p>
</details>

---

### 如何能打印出`console.log`语句后注释掉的值？

```javascript
function* startGame() {
  const 答案 = yield "Do you love JavaScript?";
  if (答案 !== "Yes") {
    return "Oh wow... Guess we're gone here";
  }
  return "JavaScript loves you back ❤️";
}

const game = startGame();
console.log(/* 1 */); // Do you love JavaScript?
console.log(/* 2 */); // JavaScript loves you back ❤️
//.next()  { value: 'xxx', done: false } 
```

- A: `game.next("Yes").value` and `game.next().value`
- B: `game.next.value("Yes")` and `game.next.value()`
- C: `game.next().value` and `game.next("Yes").value`
- D: `game.next.value()` and `game.next.value("Yes")`

<details><summary><b>答案</b></summary>
<p>

答案: C

`generator`函数在遇到`yield`关键字时会“暂停”其执行。 首先，我们需要让函数产生字符串`Do you love JavaScript?`，这可以通过调用`game.next().value`来完成。上述函数的第一行就有一个`yield`关键字，那么运行立即停止了，`yield`表达式本身没有返回值，或者说总是返回`undefined`, 这意味着此时变量 `答案` 为`undefined`

`next`方法可以带一个参数，该参数会被当作上一个 `yield` 表达式的返回值。当我们调用`game.next("Yes").value`时，先前的 `yield` 的返回值将被替换为传递给`next()`函数的参数`"Yes"`。此时变量 `答案` 被赋值为 `"Yes"`，`if`语句返回`false`，所以`JavaScript loves you back ❤️`被打印。

</p>
</details>

---

### 输出什么?

```javascript
async function getData() {
  return await Promise.resolve("I made it!");
}

const data = getData();
console.log(data);
```

- A: `"I made it!"`
- B: `Promise {<resolved>: "I made it!"}`
- C: `Promise {<pending>}`
- D: `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: C

异步函数始终返回一个promise。`await`仍然需要等待promise的解决：当我们调用`getData()`并将其赋值给`data`，此时`data`为`getData`方法返回的一个挂起的promise，该promise并没有解决。

如果我们想要访问已解决的值`"I made it!"`，可以在`data`上使用`.then()`方法：

`data.then(res => console.log(res))`

这样将打印 `"I made it!"`

</p>
</details>

---

### 输出什么?

```javascript
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young."
  } else {
    const message = "Yay! You're old enough!"
  }

  return message
}

console.log(checkAge(21))
```

- A: `"Sorry, you're too young."`
- B: `"Yay! You're old enough!"`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: C

`const`和`let`声明的变量是具有**块级作用域**的，块是大括号（`{}`）之间的任何东西, 即上述情况`if / else`语句的花括号。 由于块级作用域，我们无法在声明的块之外引用变量，因此抛出`ReferenceError`。

</p>
</details>

---

### 输出什么?

```javascript
function giveLydiaPizza() {
  return "Here is pizza!"
}

const giveLydiaChocolate = () => "Here's chocolate... now go hit the gym already."

console.log(giveLydiaPizza.prototype)
console.log(giveLydiaChocolate.prototype)
```

- A: `{ constructor: ...}` `{ constructor: ...}` 
- B: `{}` `{ constructor: ...}` 
- C: `{ constructor: ...}` `{}`
- D: `{ constructor: ...}` `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: D

常规函数，例如`giveLydiaPizza`函数，有一个`prototype`属性，它是一个带有`constructor`属性的对象（原型对象）。 然而，箭头函数，例如`giveLydiaChocolate`函数，没有这个`prototype`属性。 尝试使用`giveLydiaChocolate.prototype`访问`prototype`属性时会返回`undefined`。

</p>
</details>

---

### 输出什么?

```javascript
const person = {
  name: "Lydia",
  age: 21
}

for (const [x, y] of Object.entries(person)) {
  console.log(x, y)
}
```

- A: `name` `Lydia` and `age` `21`
- B: `["name", "Lydia"]` and `["age", 21]` 
- C: `["name", "age"]` and `undefined`
- D: `Error`

<details><summary><b>答案</b></summary>
<p>

答案: A
`Object.entries()`方法返回一个给定对象自身可枚举属性的键值对数组，上述情况返回一个二维数组，数组每个元素是一个包含键和值的数组：

`[['name'，'Lydia']，['age'，21]]`

使用`for-of`循环，我们可以迭代数组中的每个元素，上述情况是子数组。 我们可以使用`const [x，y]`在`for-of`循环中解构子数组。 `x`等于子数组中的第一个元素，`y`等于子数组中的第二个元素。

第一个子阵列是`[“name”，“Lydia”]`，其中`x`等于`name`，而`y`等于`Lydia`。
第二个子阵列是`[“age”，21]`，其中`x`等于`age`，而`y`等于`21`。

</p>
</details>

---

###  输出什么?

```javascript
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

- A: `["banana", "apple", "pear", "orange"]`
- B: `[["banana", "apple"], "pear", "orange"]` 
- C: `["banana", "apple", ["pear"], "orange"]`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: D

`... args`是剩余参数，剩余参数的值是一个包含所有剩余参数的数组，**并且只能作为最后一个参数**。上述示例中，剩余参数是第二个参数，这是不可能的，并会抛出语法错误。

```javascript
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

上述例子是有效的，将会返回数组：`[ 'banana', 'apple', 'orange', 'pear' ]`
</p>
</details>

---

### <a name=20190817></a>输出什么?

```javascript
function nums(a, b) {
  if
  (a > b)
  console.log('a is bigger')
  else 
  console.log('b is bigger')
  return 
  a + b
}

console.log(nums(4, 2))
console.log(nums(1, 2))
```

- A: `a is bigger`, `6` and `b is bigger`, `3`
- B: `a is bigger`, `undefined` and `b is bigger`, `undefined`
- C: `undefined` and `undefined`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: B


在JavaScript中，我们不必显式地编写分号(`;`)，但是JavaScript引擎仍然在语句之后自动添加分号。这称为**自动分号插入**。例如，一个语句可以是变量，或者像`throw`、`return`、`break`这样的关键字。

在这里，我们在新的一行上写了一个`return`语句和另一个值`a + b `。然而，由于它是一个新行，引擎并不知道它实际上是我们想要返回的值。相反，它会在`return`后面自动添加分号。你可以这样看:

```javascript
  return;
  a + b
```

这意味着永远不会到达`a + b`，因为函数在`return`关键字之后停止运行。如果没有返回值，就像这里，函数返回`undefined`。注意，在`if/else`语句之后没有自动插入!

</p>
</details>

---

### 输出什么?

```javascript
class Person {
  constructor() {
    this.name = "Lydia"
  }
}

Person = class AnotherPerson {
  constructor() {
    this.name = "Sarah"
  }
}

const member = new Person()
console.log(member.name)
```

- A: `"Lydia"`
- B: `"Sarah"`
- C: `Error: cannot redeclare Person`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: B


我们可以将类设置为等于其他类/函数构造函数。 在这种情况下，我们将`Person`设置为`AnotherPerson`。 这个构造函数的名字是`Sarah`，所以新的`Person`实例`member`上的name属性是`Sarah`。


</p>
</details>

---

### 输出什么?

```javascript
const getList = ([x, ...y]) => [x, y]
const getUser = user => { name: user.name, age: user.age }

const list = [1, 2, 3, 4]
const user = { name: "Lydia", age: 21 }

console.log(getList(list))
console.log(getUser(user))
```

- A: `[1, [2, 3, 4]]` and `undefined`
- B: `[1, [2, 3, 4]]` and `{ name: "Lydia", age: 21 }`
- C: `[1, 2, 3, 4]` and `{ name: "Lydia", age: 21 }`
- D: `Error` and `{ name: "Lydia", age: 21 }`

<details><summary><b>答案</b></summary>
<p>

答案: A

`getList`函数接收一个数组作为其参数。 在`getList`函数的括号之间，我们立即解构这个数组。 您可以将其视为：

 `[x, ...y] = [1, 2, 3, 4]`


使用剩余的参数`... y`，我们将所有剩余参数放在一个数组中。 在这种情况下，其余的参数是`2`，`3`和`4`。 `y`的值是一个数组，包含所有其余参数。 在这种情况下，`x`的值等于`1`，所以当我们打印`[x，y]`时，会打印`[1，[2,3,4]]`。

 `getUser`函数接收一个对象。对于箭头函数，如果只返回一个值，我们不必编写花括号。但是，如果您想从一个箭头函数返回一个对象，您必须在圆括号之间编写它，否则不会返回任何值!下面的函数将返回一个对象:

```const getUser = user => ({ name: user.name, age: user.age })```

由于在这种情况下不返回任何值，因此该函数返回`undefined`。

</p>
</details>

---

### 输出什么?

```javascript
// 🎉✨ This is my 100th question! ✨🎉

const output = `${[] && 'Im'}possible!
You should${'' && `n't`} see a therapist after so much JavaScript lol`
```

- A: `possible! You should see a therapist after so much JavaScript lol`
- B: `Impossible! You should see a therapist after so much JavaScript lol`
- C: `possible! You shouldn't see a therapist after so much JavaScript lol`
- D: `Impossible! You shouldn't see a therapist after so much JavaScript lol`

<details><summary><b>答案</b></summary>
<p>

答案: B


`[]`是一个真值。 使用`&&`运算符，如果左侧值是真值，则返回右侧值。 在这种情况下，左侧值`[]`是一个真值，所以返回`Im`。

`""`是一个假值。 如果左侧值是假的，则不返回任何内容。 `n't`不会被退回。

</p>
</details>

---

### 结果是什么?

```javascript
Promise.resolve(5)
```

- A: `5`
- B: `Promise {<pending>: 5}`
- C: `Promise {<fulfilled>: 5}`
- D: `Error`

<details><summary><b>答案</b></summary>
<p>

答案: C

我们可以将我们想要的任何类型的值传递`Promise.resolve`，无论是否`promise`。 该方法本身返回带有已解析值的`Promise` (`<fulfilled>`)。 如果您传递常规函数，它将是具有常规值的已解决`promise`。 如果你通过了promise，它将是一个已经resolved的且带有传的值的promise。

上述情况，我们传了数字5，因此返回一个resolved状态的promise，resolve值为`5`

</p>
</details>

---

### 输出什么?

```javascript
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log("Not the same!")
  } else {
    console.log("They are the same!")
  }
}

const person = { name: "Lydia" }

compareMembers(person)
```

- A: `Not the same!`
- B: `They are the same!`
- C: `ReferenceError`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: B

对象通过引用传递。 当我们检查对象的严格相等性（===）时，我们正在比较它们的引用。

我们将“person2”的默认值设置为“person”对象，并将“person”对象作为“person1”的值传递。

这意味着两个值都引用内存中的同一位置，因此它们是相等的。

运行“ else”语句中的代码块，并记录`They are the same!` 。

</p>
</details>

---

###### 88. 输出什么?

```javascript
function sum(num1, num2 = num1) {
  console.log(num1 + num2)
}

sum(10)
```

- A: `NaN`
- B: `20`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>答案</b></summary>
<p>

#### 答案: B

您可以将默认参数的值设置为函数的另一个参数，只要另一个参数定义在其之前即可。 我们将值`10`传递给`sum`函数。 如果`sum`函数只接收1个参数，则意味着没有传递`num2`的值，这种情况下，`num1`的值等于传递的值`10`。 `num2`的默认值是`num1`的值，即`10`。 ```num1 + num2```返回`20`。

如果您尝试将默认参数的值设置为后面定义的参数，则可能导致参数的值尚未初始化，从而引发错误。比如：
```js
function test(m = n, n = 2) {
	console.log(m, n)
}
test() // Uncaught ReferenceError: Cannot access 'n' before initialization
test(3) // 3 2
test(3, 4) // 3 4
```

</p>
</details>

---

### 输出什么?

```javascript
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log("Not the same!")
  } else {
    console.log("They are the same!")
  }
}

const person = { name: "Lydia" }

compareMembers(person)
```

- A: `Not the same!`
- B: `They are the same!`
- C: `ReferenceError`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: B

对象通过引用传递。 当我们检查对象的严格相等性（===）时，我们正在比较它们的引用。

我们将“person2”的默认值设置为“person”对象，并将“person”对象作为“person1”的值传递。

这意味着两个值都引用内存中的同一位置，因此它们是相等的。

运行“ else”语句中的代码块，并记录`They are the same!` 。

</p>
</details>

---

### 输出什么?


```javascript
const colorConfig = {
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false,
}

const colors = ["pink", "red", "blue"]

console.log(colorConfig.colors[1])
```

- A: `true`
- B: `false`
- C: `undefined`
- D: `TypeError`

<details><summary><b>答案</b></summary>
<p>

答案: D

在JavaScript中，我们有两种访问对象属性的方法：括号表示法或点表示法。 在此示例中，我们使用点表示法（`colorConfig.colors`）代替括号表示法（`colorConfig [“ colors”]`）。

使用点表示法，JavaScript会尝试使用该确切名称在对象上查找属性。 在此示例中，JavaScript尝试在colorconfig对象上找到名为colors的属性。 没有名为“colors”的属性，因此返回“undefined”。
然后，我们尝试使用`[1]`访问第一个元素的值。 我们无法对未定义的值执行此操作，因此会抛出`Cannot read property '1' of undefined`。

JavaScript解释（或取消装箱）语句。 当我们使用方括号表示法时，它会看到第一个左方括号`[`并一直进行下去，直到找到右方括号`]`。 只有这样，它才会评估该语句。 如果我们使用了colorConfig [colors [1]]，它将返回colorConfig对象上red属性的值。


</p>
</details>

---

### 输出什么?

```javascript
const config = {
	languages: [],
	set language(lang) {
		return this.languages.push(lang);
	}
};

console.log(config.language);
```

- A: `function language(lang) { this.languages.push(lang }`
- B: `0`
- C: `[]`
- D: `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: D

方法 `language` 是一个 `setter`。Setters 并不保存一个实际值，它们的使命在于 _修改_ 属性。当调用方法 `setter`， 返回 `undefined`。

---

### 输出什么?

```javascript
const add = x => y => z => {
	console.log(x, y, z);
	return x + y + z;
};

add(4)(5)(6);
```

- A: `4` `5` `6`
- B: `6` `5` `4`
- C: `4` `function` `function`
- D: `undefined` `undefined` `6`

<details><summary><b>答案</b></summary>
<p>

答案: A

函数 `add` 是一个返回 返回箭头函数的箭头函数 的箭头函数（still with me?）。第一个函数接收一个值为 `4` 的参数 `x`。我们调用第二个函数，它接收一个值为 `5` 的参数 `y`。然后我们调用第三个函数，它接收一个值为 `6` 的参数 `z`。当我们尝试在最后一个箭头函数中获取 `x`, `y` 和 `z` 的值，JS 引擎根据作用域链去找 `x` 和 `y` 的值。得到 `4` `5` `6`.

</p>
</details>

---

###  输出什么？

```javascript
async function* range(start, end) {
	for (let i = start; i <= end; i++) {
		yield Promise.resolve(i);
	}
}

(async () => {
	const gen = range(1, 3);
	for await (const item of gen) {
		console.log(item);
	}
})();
```

- A: `Promise {1}` `Promise {2}` `Promise {3}`
- B: `Promise {<pending>}` `Promise {<pending>}` `Promise {<pending>}`
- C: `1` `2` `3`
- D: `undefined` `undefined` `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: C

我们给 函数range 传递： `Promise{1}`, `Promise{2}`, `Promise{3}`，Generator 函数 `range` 返回一个全是 async object promise 数组。我们将 async object 赋值给变量 `gen`，之后我们使用`for await ... of` 进行循环遍历。我们将返回的 Promise 实例赋值给 `item`： 第一个返回 `Promise{1}`， 第二个返回 `Promise{2}`，之后是 `Promise{3}`。因为我们正 _awaiting_ `item` 的值，resolved 状态的 promsie，promise数组的resolved _值_ 以此为： `1`，`2`，`3`.

</p>
</details>

---

### 输出什么？

```javascript
const myFunc = ({ x, y, z }) => {
	console.log(x, y, z);
};

myFunc(1, 2, 3);
```

- A: `1` `2` `3`
- B: `{1: 1}` `{2: 2}` `{3: 3}`
- C: `{ 1: undefined }` `undefined` `undefined`
- D: `undefined` `undefined` `undefined`

<details><summary><b>答案</b></summary>
<p>

答案: D

`myFunc` 期望接收一个包含 `x`, `y` 和 `z` 属性的对象作为它的参数。因为我们仅仅传递三个单独的数字值 (1, 2, 3) 而不是一个含有 `x`, `y` 和 `z` 属性的对象 ({x: 1, y: 2, z: 3})， `x`, `y` 和 `z` 有着各自的默认值 `undefined`.

</p>
</details>

---

### 输出什么？

```javascript
const name = "Lydia Hallie";
const age = 21;

console.log(Number.isNaN(name));
console.log(Number.isNaN(age));

console.log(isNaN(name));
console.log(isNaN(age));
```

- A: `true` `false` `true` `false`
- B: `true` `false` `false` `false`
- C: `false` `false` `true` `false`
- D: `false` `true` `false` `true`

<details><summary><b>答案</b></summary>
<p>

答案: C

通过方法 `Number.isNaN`，你可以检测你传递的值是否为 _数字值_ 并且是否等价于 `NaN`。`name` 不是一个数字值，因此 `Number.isNaN(name)` 返回 `false`。`age` 是一个数字值，但它不等价于 `NaN`，因此 `Number.isNaN(age)` 返回 `false`.

通过方法 `isNaN`， 你可以检测你传递的值是否一个 number。`name` 不是一个 `number`，因此 `isNaN(name)` 返回 `true`. `age` 是一个 `number` 因此 `isNaN(age)` 返回 `false`.

</p>
</details>

---

### 我们怎样才能在 `index.js` 中调用 `sum.js?` 中的 `sum`？

```javascript
// sum.js
export default function sum(x) {
	return x + x;
}

// index.js
import * as sum from "./sum";
```

- A: `sum(4)`
- B: `sum.sum(4)`
- C: `sum.default(4)`
- D: 默认导出不用 `*` 来导入，只能具名导出

<details><summary><b>答案</b></summary>
<p>

答案: C

使用符号 `*`，我们引入文件中的所有值，包括默认和具名。如果我们有以下文件：

```javascript
// info.js
export const name = "Lydia";
export const age = 21;
export default "I love JavaScript";

// index.js
import * as info from "./info";
console.log(info);
```

将会输出以下内容：

```javascript
{
  default: "I love JavaScript",
  name: "Lydia",
  age: 21
}
```

以 `sum` 为例，相当于以下形式引入值 `sum`：

```javascript
{ default: function sum(x) { return x + x } }
```

我们可以通过调用 `sum.default` 来调用该函数

</p>
</details>

---

### 输出什么？

```javascript
const handler = {
	set: () => console.log("Added a new property!"),
	get: () => console.log("Accessed a property!")
};

const person = new Proxy({}, handler);

person.name = "Lydia";
person.name;
```

- A: `Added a new property!`
- B: `Accessed a property!`
- C: `Added a new property!` `Accessed a property!`
- D: 没有任何输出

<details><summary><b>答案</b></summary>
<p>

答案: C

使用 Proxy 对象，我们可以给一个对象添加自定义行为。在这个 case，我们传递一个包含以下属性的对象 `handler` : `set` and `get`。每当我门 _设置_ 属性值时 `set` 被调用，每当我们 _获取_ 时 `get` 被调用。

第一个参数是一个空对象 `{}`，作为 `person` 的值。对于这个对象，自定义行为被定义在对象 `handler`。如果我们向对象 `person` 添加属性，`set` 将被调用。如果我们获取 `person` 的属性, `get` 将被调用。

首先，我们向 proxy 对象(`person.name = "Lydia"`)添加一个属性 `name`。`set` 被调用并输出 `"Added a new property!"`。

然后，我们获取 proxy 对象的一个属性，对象 handler 的属性 `get` 被调用。输出 `"Accessed a property!"`。

</p>
</details>

---

### 以下哪一项会对对象 `person` 有副作用？

```javascript
const person = { name: "Lydia Hallie" };

Object.seal(person);
```

- A: `person.name = "Evan Bacon"`
- B: `person.age = 21`
- C: `delete person.name`
- D: `Object.assign(person, { age: 21 })`

<details><summary><b>答案</b></summary>
<p>

答案: A

使用 `Object.seal` 我们可以防止新属性 _被添加_，或者存在属性 _被移除_.

然而，你仍然可以对存在属性进行更改。

</p>
</details>

---

### 以下哪一项会对对象 `person` 有副作用？

```javascript
const person = {
	name: "Lydia Hallie",
	address: {
		street: "100 Main St"
	}
};

Object.freeze(person);
```

- A: `person.name = "Evan Bacon"`
- B: `delete person.address`
- C: `person.address.street = "101 Main St"`
- D: `person.pet = { name: "Mara" }`

<details><summary><b>答案</b></summary>
<p>

答案: C

使用方法 `Object.freeze` 对一个对象进行 _冻结_。不能对属性进行添加，修改，删除。

然而，它仅 对对象进行 _浅_ 冻结，意味着只有 对象中的 _直接_ 属性被冻结。如果属性是另一个 object，像案例中的 `address`，`address` 中的属性没有被冻结，仍然可以被修改。

</p>
</details>

---

### 输出什么？

```javascript
class Counter {
  #number = 10

  increment() {
    this.#number++
  }

  getNum() {
    return this.#number
  }
}

const counter = new Counter()
counter.increment()

console.log(counter.#number)
```

- A: `10`
- B: `11`
- C: `undefined`
- D: `SyntaxError`

<details><summary><b>答案</b></summary>
<p>

答案: D

在 ES2020 中，通过 `#` 我们可以给 class 添加私有变量。在 class 的外部我们无法获取该值。当我们尝试输出 `counter.#number`，语法错误被抛出：我们无法在 class `Counter` 外部获取它!

</p>
</details>

---

### 我们需要向对象 `person` 添加什么，以致执行 `[...person]` 时获得形如 `["Lydia Hallie", 21]` 的输出？

```javascript
const person = {
  name: "Lydia Hallie",
  age: 21
}

[...person] // ["Lydia Hallie", 21]
```

- A: 不需要，对象默认就是可迭代的
- B: `*[Symbol.iterator]() { for (let x in this) yield* this[x] }`
- C: `*[Symbol.iterator]() { for (let x in this) yield* Object.values(this) }`
- D: `*[Symbol.iterator]() { for (let x in this) yield this }`

<details><summary><b>答案</b></summary>
<p>

答案: C

对象默认并不是可迭代的。如果迭代规则被定义，则一个对象是可迭代的（An iterable is an iterable if the iterator protocol is present）。我们可以通过添加迭代器symbol `[Symbol.iterator]` 来定义迭代规则，其返回一个 generator 对象，比如说构建一个 generator 函数 `*[Symbol.iterator]() {}`。如果我们想要返回数组 `["Lydia Hallie", 21]`: `yield* Object.values(this)`，这个 generator 函数一定要 yield 对象 `person` 的`Object.values`。

</p>
</details>

---

### 输出是什么？

```javascript
function getFruit(fruits) {
	console.log(fruits?.[1]?.[1])
}

getFruit([['🍊', '🍌'], ['🍍']])
getFruit()
getFruit([['🍍'], ['🍊', '🍌']])
```

- A: `null`, `undefined`, 🍌
- B: `[]`, `null`, 🍌
- C: `[]`, `[]`, 🍌
- D: `undefined`, `undefined`, 🍌

<details><summary><b>答案</b></summary>
<p>

答案: D

`?` 允许我们去选择性地访问对象内部更深层的嵌套属性。 我们尝试打印 `fruits` 数组索引值为 `1` 的子数组内部的索引值为 `1` 的元素。 如果在 `fruits` 数组索引值 为 `1` 的位置不存在元素，会直接返回 `undefined`。 如果 `fruits` 数组在索引值为 `1` 的位置存在元素，但是子数组在索引值为 `1` 的位置不存在元素，也会返回 `undefined`。

首先，我们尝试打印 `[['🍊', '🍌'], ['🍍']]` 的子数组 `['🍍']` 的第2个元素。这个子数组只包含一个元素，也就意味着在索引值为 `1` 的位置不存在元素，所以返回的是 `undefined` 。

其次，我们在没有传入任何参数调用了 `getFruits` 函数，也就意味着形参 `fruits` 的默认值为`undefined`。因为我们选择性地链接了 `fruits` 在索引值为 `1` 的元素，因为在索引值为 `1` 的位置不存在元素，因此返回的是 `undefined` 。

最后，我们尝试打印 `['🍍'], ['🍊', '🍌']` 的子数组 `['🍊', '🍌']` 的第2个元素。子数组索引值为 `1`的位置为 `🍌` ，因此它被打印出了。

</p>
</details>

---

### 输出什么?

```javascript
const user = {
	email: "e@mail.com",
	password: "12345"
}

const updateUser = ({ email, password }) => {
	if (email) {
		Object.assign(user, { email })
	}

	if (password) {
		user.password = password
	}

	return user
}

const updatedUser = updateUser({ email: "new@email.com" })

console.log(updatedUser === user)
```

- A: `false`
- B: `true`
- C: `TypeError`
- D: `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: B

 `updateUser` 函数更新user的 `email` 和 `password` 属性的值， 如果它们的值传入函数， 函数返回的就是 `user` 对象。 `updateUser` 函数的返回值是 `user` 对象，意味着updatedUser的值与 `user` 指向的是同一个 `user` 对象。`updatedUser === user` 为 `true`.

</p>
</details>

---

### 输出什么?

```javascript
const user = {
	email: "my@email.com",
	updateEmail: email => {
		this.email = email
	}
}

user.updateEmail("new@email.com")
console.log(user.email)
```

- A: `my@email.com`
- B: `new@email.com`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>答案</b></summary>
<p>

答案: A

`updateEmail` 函数是一个箭头函数，它没有和 `user` 对象绑定。这就意味着 `this` 关键字不会引用到 `user` 对象，但是会引用到全局对象。 `user` 对象内部的 `email` 的值不会更新。当打印 `user.email` 的时候， 原始值 `my@email.com` 被返回。

</p>
</details>

---

### 输出什么?

```javascript
const promise1 = Promise.resolve('First')
const promise2 = Promise.resolve('Second')
const promise3 = Promise.reject('Third')
const promise4 = Promise.resolve('Fourth')

const runPromises = async () => {
	const res1 = await Promise.all([promise1, promise2])
	const res2  = await Promise.all([promise3, promise4])
	return [res1, res2]
}

runPromises()
	.then(res => console.log(res))
	.catch(err => console.log(err))
```

- A: `[['First', 'Second'], ['Fourth']]`
- B: `[['First', 'Second'], ['Third', 'Fourth']]`
- C: `[['First', 'Second']]`
- D: `'Third'`

<details><summary><b>答案</b></summary>
<p>

答案: D

 `Promise.all` 方法可以并行式运行promise。如果其中一个promise失败了，`Promise.all` 方法会带上被reject的promise的值_rejects_。在这个例子中， `promise3` 带着 `"Third"` 值reject。我们在调用 `runPromises` 时在 `runPromises` 函数内部的 `catch` 方法去捕获任意error从而捕获到被reject的值。因为 `promise3` 带着 `"Third"` 被reject，所以只有 `"Third"` 打印。

</p>
</details>

---

###  哪个作为`method`的值可以打印`{ name: "Lydia", age: 22 }`?

```javascript
const keys = ["name", "age"]
const values = ["Lydia", 22]

const method = /* ?? */
Object[method](keys.map((_, i) => {
	return [keys[i], values[i]]
})) // { name: "Lydia", age: 22 }
```

- A: `entries`
- B: `values`
- C: `fromEntries`
- D: `forEach`

<details><summary><b>答案</b></summary>
<p>

答案: C

 `fromEntries` 方法可以将二维数组转换为对象。在每个子数组的第一个元素是key，在每个子数组的第二个元素是value。在这个例子中，我们映射了 `keys` 数组，它返回了一个数组，数组的第一个元素为keys数组当前索引的值，第二个元素为values数组当前索引的值。

这样就创建了一个包含正确keys和values的子数组的数组，因此结果为`{ name: "Lydia", age: 22 }`。

</p>
</details>

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

# 微信小程序
## 基础信息
开发流程
- 注册
- 小程序信息完善
- 开发小程序
- 提交审核和发布
  
启动方式
- 热启动（已经打开过一定时间内再次打开无需重新启动）
- 冷启动（首次打开或销毁后重新打开）
  
双线程架构（通过WXJSBridge和底层native通信）
- View视图线程
- App Service逻辑线程
  
WXS（setData更新瓶颈）
- WXS和WXML可构建出页面的组件结构
- 不依赖运行时基础库版本，可在所有版本小程序运行
- 运行在视图层，提高渲染更新效率
- 运行环境与js代码隔离且不能调用wx-api
- 不能作为事件函数绑定在标签上
- 在ios上比js快2-20倍
```
<view>
    <view>
        <text>{{tools.bar()}}</text>
        <text>{{tools.foo}}</text>
    </view>
    <wxs module="tools">
        var foo = 'helloworld'
        var bar = function(){
            return 'aaa'
        }
        module.exports = {
            foo:foo
            bar:bar
        }
    </wxs>
</view>
```
## icon组件
真机icon显示空白问题？

wxss内加载图片及字体文件资源时允许使用外域地址，检查机型及嵌入的字体文件类型（兼容性），推荐使用TTF和WOFF格式字体，如果问题依然存在考虑换SVG格式的数据嵌入



