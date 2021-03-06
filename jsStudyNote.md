
[toc]

---

`这是一个PHPer学习javascript的笔记`

### 数据类型
1. == 和 ===
    - ==会自动转换数据类型再比较
    - === 不会自动转换数据类型，如果数据类型不一致，返回false，如果一致则进行比较
2. NaN
    - NaN和所有的其他值都不相等，包括他自己。只有通过 isNaN() 函数才能进行判断
3. 浮点数比较
    - 浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小数。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值
4. null 和 undefined
    - null表示空
    - undifined表示值未定义，静静在判断函数参数是否传递的情况下使用
5. 对象
    - 对象的键都是字符串类型，值可以是任意类型
6. 字符串
    - 多行字符串用\` \`表示
    - 模板字符串 \`你好, 你今年${age}岁了!\`
    - 字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果
7. 数组
    - 如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化
    - 使用indexOf()进行搜索元素位置的时候，查询参数区分类型。例如：数字30和字符串'30'是不同的元素
    - arr.splice() 可以实现数组的删除、插入、修改操作
    - arr.concat() 相当于 array_merge()
    - arr.join() 相当于implode()
8. 对象
    - 对象属性名不包含特殊字符，这样定义 key: value，可以直接使用 . 操作符访问
    - 包含特殊字符，这样定义 'special_key': value, 必须使用x\['special_key'\]来访问   
    - delete obj.a  删除obj中的a属性
    - 'a' in obj    检查a属性是否在obj中
    - obj.hasOwnProperty('a'); 判断a属性是否是obj自身拥有的，而不是继承来的
9. 条件判断
    - null undefined 0 NaN '' false  视为 false
10. Map & Set
    - Map不会因为长度而降低查询速度
        ```
        var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
        m.get('Michael'); // 95
        // m.set m.get m.delete m.has
        ```
    - 重复元素在Set中自动被过滤, 区分字符串和数字
11. iterable
    - Array、Map和Set都属于iterable类型
    - 可以使用 for( var item of array) 来遍历
    - iterable 内置 forEach方法 `a.forEach(function (element, index, array) {})`;
    - 使用forEach 中 修改array的值， 无法影响当前循环，但是影响循环结束时的值

12. NaN:number true:boolean undefined:undefined null:object

### 函数
- 函数的参数可以多于预定参数，也可以少于预定参数。多于则忽略，少于则受到undefined
- arguments永远指向当前函数的调用者传入的所有参数。arguments类似Array但它不是一个Array
- arguments 常用于 调整传入参数和函数参数默认值
- function foo(a, b, ...rest) {}  可以将多余的参数传入 rest变量中，如果没有多余参数，rest则会变成一个空数组
- JavaScript引擎有一个在行末自动添加分号的机制，需要注意
- javascript的函数会先扫描整个函数体内的语句，并把所有申明的变量“提升”到函数顶部
- let 用来声明块级变量， const 用来声明常量
- 解构赋值 `var [x, y, z] = ['hello', 'JavaScript', 'ES6'];`
- 解构赋值还可以忽略某些元素`let [, , z] = ['hello', 'JavaScript', 'ES6'];`
- 函数本身自带apply方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。
- call方法和apply方法类似，区别在于apply是将参数打包成数组，call将参数顺序传入
    `Math.max.apply(null, [3, 5, 4]); // 5`
    `Math.max.call(null, 3, 5, 4); // 5`
- 可以使用自定义函数替换掉默认的函数
    ```
    window.parseInt = function () {
        count += 1;
        return oldParseInt.apply(null, arguments); // 调用原函数
    };
    ```
- 高阶函数

    - map()方法 `arr.map(String)`  为arr 中的所有项执行String()函数
    - reduce()方法 `[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)` Array的reduce()把一个函数作用在这个Array的[x1, x2, x3...]上，这个函数必须接收两个参数，reduce()把结果继续和序列的下一个元素做累积计算
    - map()中的回调函数要求只有一个参数，否则会出现意料之外的错误
    - filter() 筛选
    - sort() 排序;  Array的sort()方法默认把所有元素先转换为String再排序;sort()可以传入自定义函数;sort()方法会直接对Array进行修改，它返回的结果仍是当前Array

- 闭包  函数作为返回值：返回函数不要引用任何循环变量，或者后续会发生变化的变量 
- 箭头函数: `x => x * x`
- generator 

### 标准对象
- Date对象月份值从0开始 0表示1月，1表示2月
- 创建正则匹配分两种  一种 会直接定义字符串 '/ABC/'; 另一种 new RegExp('ABC'); 注意 第二种存在转义字符的问题
- (/ABC/).test('ABCDEFG'); 检查是否能够成功匹配
- 'a b   c'.split(/\s+/); // ['a', 'b', 'c'] 正则分割
- (/^(\d{3})-(\d{3,8})$/).exec('010-12345');
- \d+采用贪婪匹配; \d+?采用非贪婪匹配
- 全局搜索 var r = /test/g  或者  var r = new RegExp('test','g');
- 全局匹配可以多次执行exec()方法来搜索一个匹配的字符串。当我们指定g标志后，每次运行exec()，正则表达式本身会更新lastIndex属性，表示上次匹配到的最后索引
- json 序列化 JSON.stringify(value, null, ''); 第二个参数用于指定需要输出的属性 或 传入一个函数处理所有的键值对;
- json 反序列化 JSON.parse(value); 其第二参数可以传入一个函数，用来处理解析出来的属性;

### 面向对象编程
- JavaScript不区分类和实例的概念，而是通过原型（prototype）来实现面向对象编程
- 每个对象都有 __proto__ 属性，但只有函数对象才有 prototype 属性
- xiaoming.__proto__ = Student;    xiaoming 是一个用户对象    Student 是一个学生对象
- Object.create()方法可以传入一个原型对象，并创建一个基于该原型的新对象
- var arr = [1,2,3];  对象原型链 : `arr ----> Array.prototype ----> Object.prototype ----> null`
- 构造函数 new {function() {}}
- 创建的对象 会获得一个 constructor 属性，他指向原型本身
- 一个常用的模式
    ```
    function Student(props) {
        this.name = props.name || '匿名'; // 默认值为'匿名'
        this.grade = props.grade || 1; // 默认值为1
    }
    
    Student.prototype.hello = function () {
        alert('Hello, ' + this.name + '!');
    };
    
    function createStudent(props) {
        return new Student(props || {})
    }
    ```
- inherits 原型继承封装函数
- 使用 class 来声明类 extends 来继承类
- 使用super(); 来调用父类的构造方法
- [Babel](https://babeljs.io/) 一个把class代码转换为传统的prototype代码的工具

### 浏览器
- window; IE<=8不支持
- navigator 对象表示浏览器的信息
    - navigator.appName：浏览器名称；
    - navigator.appVersion：浏览器版本；
    - navigator.language：浏览器设置的语言；
    - navigator.platform：操作系统类型；
    - navigator.userAgent：浏览器设定的User-Agent字符串   
- screen 对象表示屏幕的信息
    - screen.width：屏幕宽度，以像素为单位；
    - screen.height：屏幕高度，以像素为单位；
    - screen.colorDepth：返回颜色位数，如8、16、24
- location 当前页面的URL信息
    - location.protocol; // 'http'
    - location.host; // 'www.example.com'
    - location.port; // '8080'
    - location.pathname; // '/path/index.html'
    - location.search; // '?a=1&b=2'
    - location.hash; // 'TOP'
- document 表示当前页面
    - document.getElementById();
    - ducument.getElementsByTagName();
    - document.cookie;
- history 浏览器的历史记录
    - history.back();
    - history.forward();
    - 不建议使用history 这个对象
- querySelector() querySelectorAll()

#### 操作DOM
- innerHTML innerText textContent;innerText不返回隐藏元素的文本，而textContent返回所有文本。另外注意IE<9不支持textContent
- DOM节点的style属性对应所有的CSS，可以直接获取或设置。因为CSS允许font-size这样的名称，但它并非JavaScript有效的属性名，所以需要在JavaScript中改写为驼峰式命名fontSize
- appendChild() 插入新元素
- 插入的js节点已经存在于当前的文档树，因此这个节点首先会从原先的位置删除，再插入到新的位置
- createElement(); 创建一个新的节点
- insertBefore(newElement, referenceElement) 子节点会插入到referenceElement之前
- 删除节点 var remove = parent.removeChild(self); 删除后的节点虽然不在文档树中了，但其实它还在内存中，可以随时再次被添加到别的位置。
- js处理文件上传的操作非常少，但是在html5中，提供了File和FileReader两个主要对象，可以获得文件信息并读取文件。
- 现在浏览器上AJAx主要依赖XMLHttpRequest对象 低版本使用ActiveXObject对象
- CORS (cross-origin resource sharing) 就目前html5主流的ajax方式。 先发送一个OPTIONS请求（称为preflighted请求）到目标域名，目标域名返回Access信息，然后由js判断是否可以继续执行。
- 等待回调 new Promise(function(resolve, reject){if(1){resolve()} else {reject()}}).then(function(a){log('success')}).catch(function(b){log('fail)});
- canvas 可以用JavaScript在上面绘制各种图表、动画等,(html5)
    - getContext('2d')方法让我们拿到一个CanvasRenderingContext2D对象，所有的绘图操作都需要通过这个对象完成。
    - getContext("webgl") 绘制3d图形
    
#### jQuery
- jQuery 目前有1.x和2.x两个版本， 区别在于2.x不支持ie6/7/8
- $() 选择器
    - 连写是完全选择
    - 用逗号分隔则是取并集
    - 空格分隔是层级选择
    - `>`分隔是子选择器，要求必须是父子关系
    - :分隔 过滤器，通常附加在选择器上
    - 表单相关的选择器 :input; :file; :checkbook; :radio; :focus; :checked; :disabled; :enabled;
    - 其他 :visible; :hidden;等
- 继续选择
    - find(); 向下查找
    - parent(); 向上查找
    - next(); prev(); 同级查找
    - filter(); 过滤 可以传入一函数 函数内部的this被绑定为DOM对象，不是jQuery对象；
    - map(); 一个jQuery对象包含的若干DOM节点转化为其他对象
    - 一个jQuery对象如果包含了不止一个DOM节点，first()、last()和slice()方法可以返回一个新的jQuery对象，把不需要的DOM节点去掉
- 操作DOM
    - text(); html(); 获取/设置文本或者html  可以被选择的一组节点的处理
    - css(); 修改css样式
    - 修改class: hasClass(); addClass(); removeClass();
    - show(); hidden() 显示和隐藏
    - width(); height();获取、设置宽高
    - attr(); removeAttr(); 设置节点属性
    - is(); 判断属性是否存在; prop(); 用于设置无值属性
    - val(); 设置value属性
    - append(); 添加节点到最后 可以使DOM节点、jQ对象、函数对象；prepend()添加到最前
    - after(); before(); 将新节点插入指定节点之前、之后
    - remove(); 删除节点
- 事件
    -  鼠标事件
       - click: 鼠标单击时触发；
       - dblclick：鼠标双击时触发；
       - mouseenter：鼠标进入时触发；
       - mouseleave：鼠标移出时触发；
       - mousemove：鼠标在DOM内部移动时触发；
       - hover：鼠标进入和退出时触发两个函数，相当于mouseenter加上mouseleave。
    - 键盘事件
       - 键盘事件仅作用在当前焦点的DOM上，通常是`<input>`和`<textarea>`。
       - keydown：键盘按下时触发；
       - keyup：键盘松开时触发；
       - keypress：按一次键后触发。
    - 其他事件
       - focus：当DOM获得焦点时触发；
       - blur：当DOM失去焦点时触发；
       - change：当`<input>`、`<select>`或`<textarea>`的内容改变时触发；
       - submit：当<form>提交时触发；
       - ready：当页面被载入并且DOM树完成初始化后触发。仅作用于document对象,且只触发一次。用法 $(document).ready(function(){}) 简化 $(function () {// init...});
    - on(); 绑定事件
    - off(); 解绑事件； 注意不能解绑匿名函数。可以使用off('click')一次性移除已绑定的click事件的所有处理函数。无参数调用off()一次性移除已绑定的所有类型的事件处理函数。
    - change(); 用户操作改变时触发，如文本框输入、下拉框改变..可以通过js代码手动触发
    - 有些方法只有由用户触发才能执行。如 window.open()
<<<<<<< HEAD
- 动画
    - show(); hide(); toggle(); 参数是毫秒,但也可以是'slow'，'fast'这些字符串。在自定义的时间内显示、影藏、自适应显示影藏一个DOM元素;原点是左上角；
    - slideUp();slideDown(); slideToggle(); 同上；原点是上边框；
    - fadeIn(); fadeOut(); fadeToggle(); 同上；效果是逐渐消失、显示；
    - animate(css,time,callbackFunction(){}); 自定义动画，jQuery在时间段内不断调整CSS直到达到我们设定的值；参数1为DOM最终的css样式
    - delay(); 暂停一段时间
- AJAX
    ```
        $.ajax('/test',{
            async: true,        //是否异步执行AJAX请求，默认为true
            method: 'POST',     //发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等
            contentType: 'application/x-www-form-urlencoded; charset=UTF-8',    //发送POST请求的格式,可以指定为text/plain、application/json
            data: data,         //发送的数据，可以是字符串、数组或object。如果是GET请求，data将被转换成query附加到URL上，如果是POST请求，根据contentType把data序列化成合适的格式
            headers: {          //发送的额外的HTTP头
                "header1" : 1,
                "header2" : 2
            },
            jsonp: 'callback',
            dataType: 'html'    //接收的数据格式，可以指定为'html'、'xml'、'json'、'text'等，缺省情况下根据响应的Content-Type自适应
        });
    ```
    - 处理返回数据和出错
        - done(function(){{})
        - fail(function(){})
        - always(functio(){})
    - 辅助方法： 
        - $.get(url, params);     params 默认被构造为query string
        - $.post(url, postData);  postData默认被序列化为application/x-www-form-urlencoded
        - $.getJSON(url, params).done(function(data){});            快速通过GET获取一个JSON对象  回传值被解析为json
        
- 扩展
通过 $.fn 对象实现。
$.fn.functionA = function() {
    alert('functionA');
    return this;
}
函数内部的this在调用时被绑定为jQuery对象，所以函数内部代码可以正常调用所有jQuery对象的方法
要求自定义扩展函数内部return this;方便链式操作
通过 $.extend(target, obj1, obj2, ...) 它把多个object对象的属性合并到第一个target对象中，遇到同名属性，总是使用靠后的对象的值，也就是越往后优先级越高
编写jQuery插件的原则:
    1. 给$.fn绑定函数，实现插件的代码逻辑；
    2. 插件函数最后要return this;以支持链式调用；
    3. 插件函数要有默认值，绑定在$.fn.<pluginName>.defaults上；
    4. 用户在调用时可传入设定值以便覆盖默认值。

#### 错误处理
`try{}cache(e){}finally{}`
当代码块被try { ... }包裹的时候，就表示这部分代码执行过程中可能会发生错误，一旦发生错误，就不再继续执行后续代码，转而跳到catch块。catch (e) { ... }包裹的代码就是错误处理代码，变量e表示捕获到的错误。最后，无论有没有错误，finally一定会被执行。
JavaScript有一个标准的Error对象表示错误，还有从Error派生的TypeError、ReferenceError等错误对象。我们在处理错误时，可以通过catch(e)捕获的变量e访问错误对象
throw new Error('error');程序也可以主动抛出一个错误，让执行流程直接跳转到catch块。抛出错误使用throw语句。
如果在一个函数内部发生了错误，它自身没有捕获，错误就会被抛到外层调用函数，如果外层函数也没有捕获，该错误会一直沿着函数调用链向上抛出，直到被JavaScript引擎捕获，代码终止执行。
try cache无法从外部捕获异步事件和事件驱动，如果需要进行错误捕获，则需要吧错误捕获加在事件里面。

#### underscore
underscore为集合类对象提供了一致的接口。集合类是指Array和Object，暂不支持Map和Set。

- collections
    和Array的map()与filter()类似，但是underscore的map()和filter()可以作用于Object。当作用于Object时，传入的函数为function (value, key)，第一个参数接收value，第二个参数接收key
    _.map(); _.filter(); 返回数组   _.mapObject(); 返回对象
=======
    
    
>>>>>>> bc640b3783a6521d589c1ee6775a6ed9b72937fb
    
    当集合的所有元素都满足条件时，_.every(arr,function(key, value){return true|false})函数返回true，当集合的至少一个元素满足条件时，_.some(arr,function(key, value){return true|false})函数返回true
    _.max(arr); _.min(arr); 直接返回集合中最大和最小的数
    _.groupBy(arr,function(key))把集合的元素按照key归类，key由传入的函数返回
    _.shuffle(arr)用洗牌算法随机打乱一个集合; _.sample(arr, n)则是随机选择一个或多个元素
    [官方文档](http://underscorejs.org/#collections)
- arrays
    underscore为Array提供了许多工具类方法，可以更方便快捷地操作Array。
    _.last(arr); _.first(arr); 分别取第一个和最后一个元素
    _.flatten(arr); flatten()接收一个Array，无论这个Array里面嵌套了多少个Array，flatten()最后都把它们变成一个一维数组
    _.zip(keyArr,valueArr); _.unzip(arr); zip()把两个或多个数组的所有元素按索引对齐，然后按索引合并成新数组。unzip()则是反过来。组合、拆分key、value
    _.object(keyArr, valueArr); 和zip类似
    _.range(max); _.range(start, max, offset); 快速生成一个序列 最大值小于max
    [官方文档](http://underscorejs.org/#arrays)

- functions
    因为underscore本来就是为了充分发挥JavaScript的函数式编程特性，所以也提供了大量JavaScript本身没有的高阶函数。
    - bind
        var fn = _.bind(s.trim, s); 将s对象直接绑定在fn()的this指针上
    - partial
        partial()就是为一个函数创建偏函数。
        假设我们要计算xy，这时只需要调用Math.pow(x, y)就可以了。
        假设我们经常计算2y，每次都写Math.pow(2, y)就比较麻烦，如果创建一个新的函数能直接这样写pow2N(y)就好了，这个新函数pow2N(y)就是根据Math.pow(x, y)创建出来的偏函数，它固定住了原函数的第一个参数（始终为2）
        var pow2N = _.partial(Math.pow, 2);     固定住第一个参数
        var cube = _.partial(Math.pow, _, 3);   固定住第二个参数
    - memoize
        用memoize()就可以自动缓存函数计算的结果
        var a = _.memoize(function(){});
    - once
        once()保证某个函数执行且仅执行一次
        var register = _.once(function(){});
    - delay
        delay()可以让一个函数延迟执行，效果和setTimeout()是一样的
        _.delay(alert, 2000);
        var log = _.bind(console.log, console);
        _.delay(log, 2000, 'Hello,', 'world!');
    - [官方文档](http://underscorejs.org/#functions)
    
- object
    和Array类似，underscore也提供了大量针对Object的函数。
    - keys
        keys()可以非常方便地返回一个object自身所有的key，但不包含从原型链继承下来的
    - allKeys
        allKeys()除了object自身的key，还包含从原型链继承下来的
    - values
        values()返回object自身但不包含原型链继承的所有值
    - mapObject
        mapObject()就是针对object的map版本
    - invert
        invert()把object的每个key-value来个交换，key变成value，value变成key
    - extend
        extend()把多个object的key-value合并到第一个object并返回
    - extendOwn
        extendOwn()和extend()类似，但获取属性时忽略从原型链继承下来的属性
    - clone
        如果我们要复制一个object对象，就可以用clone()方法，它会把原有对象的所有属性都复制到新的对象中
        注意，clone()是“浅复制”。所谓“浅复制”就是说，两个对象相同的key所引用的value其实是同一对象,修改子对象会影响原对象
    - isEqual
        isEqual()对两个object进行深度比较，如果内容完全相同，则返回true
    - [官方文档](http://underscorejs.org/#objects)
        
- chaining
    _.chain()将函数包装成为链式。
    因为每一步返回的都是包装对象，所以最后一步的结果需要调用value()获得最终结果。
    var r = _.chain([1, 4, 9, 16, 25]).map(Math.sqrt).filter(x => x % 2 === 1).value();

#### node.js
 - 安装 `yum -y install nodejs npm --enablerepo=epel`
 - 执行
    - `> node test.js`
    - `> node`
       `> console.log('hello world');`
 - IDE
    - [sublime text](http://www.imooc.com/learn/40)
    - [VSCode](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001470969077294a6455fc9cd1f48b69f82cd05e7fa9b40000)
 - 模块
    为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Node环境中，一个.js文件就称之为一个模块（module）。
    最大的好处是大大提高了代码的可维护性。其次，编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Node内置的模块和来自第三方的模块。
    使用模块还可以避免函数名和变量名冲突。相同名字的函数和变量完全可以分别存在不同的模块中，因此，我们自己在编写模块时，不必考虑名字会与其他模块冲突。
    ``` hello.js
        'use strict';
        var s = 'Hello';
        function greet(name) {
            console.log(s + ', ' + name + '!');
        }
        module.exports = greet;
    ```
    `module.exports = greet;`   把函数greet作为模块的输出暴露出去，这样其他模块就可以使用greet函数了
    
    ``` main.js
        'use strict';
        var greet = require('./hello'); // 引入hello模块:
        var s = 'Michael';
        greet(s); // Hello, Michael!
    ```
    `var greet = require('./hello');` require() 函数将引入的模块作为变量保存在greet变量中
    其实变量greet就是在hello.js中我们用module.exports = greet;输出的greet函数。所以，main.js就成功地引用了hello.js模块中定义的greet()函数，接下来就可以直接使用它了
    
    这种模块加载机制被称为CommonJS规范。在这个规范下，每个.js文件都是一个模块，它们内部各自使用的变量名和函数名都互不冲突，例如，hello.js和main.js都申明了全局变量var s = 'xxx'，但互不影响。
    一个模块想要对外暴露变量（函数也是变量），可以用module.exports = variable;，一个模块要引用其他模块暴露的变量，用var ref = require('module_name');就拿到了引用模块的变量。
    
    [module原理](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434502419592fd80bbb0613a42118ccab9435af408fd000)
    如果要输出一个键值对象{}，可以利用exports这个已存在的空对象{}，并继续在上面添加新的键值；
    如果要输出一个函数或数组，必须直接对module.exports对象赋值。
    
 - 基本模块
    - global   node.js 唯一的全局对象
    - process 代表当前node.js进程
        - process.nextTick(function(){}) 等待下次事件执行后调用
        - process.on('exit', function(){}) 可以在程序退出的时候执行函数
    - 判断JavaScript执行环境
        ```
            if (typeof(window) === 'undefined') {
                console.log('node.js');
            } else {
                console.log('browser');
            }
        ```
    - fs  文件系统模块
        fs模块同时提供了异步和同步的方法。
        - 异步读
            ```
                'use strict';
                var fs = require('fs');
                fs.readFile('sample.txt', 'utf-8', function (err, data) {
                    if (err) {
                        console.log(err);
                    } else {
                        console.log(data);
                    }
                });
            ```
            当读取二进制文件时，不传入文件编码时，回调函数的data参数将返回一个Buffer对象。Buffer对象可以和String作转换。
            ```
                // Buffer -> String
                var text = data.toString('utf-8');
                // String -> Buffer
                var buf = Buffer.from(text, 'utf-8');
            ```
        - 同步读
            ```
                var fs = require('fs');
                var data = fs.readFileSync('sample.txt', 'utf-8');
                console.log(data);
            ```
        
        - 写文件
            fs.writeFile(fileName, content, callbackFunc(err));  异步写
            writeFile()的参数依次为文件名、数据和回调函数。如果传入的数据是String，默认按UTF-8编码写入文本文件，如果传入的参数是Buffer，则写入的是二进制文件。回调函数由于只关心成功与否，因此只需要一个err参数。
            fs.writeFileSync(fileName, content); 异步读
            
        - stat [文档](https://github.com/michaelliao/learn-javascript/tree/master/samples/node/fs)
            如果我们要获取文件大小，创建时间等信息，可以使用fs.stat()，它返回一个Stat对象，能告诉我们文件或目录的详细信息
            stat();同步
            statSync(): 异步
            ```
                'use strict';
                var fs = require('fs');
                fs.stat('sample.txt', function (err, stat) {
                    if (err) {
                        console.log(err);
                    } else {
                        // 是否是文件: isFile: true
                        console.log('isFile: ' + stat.isFile());
                        // 是否是目录:   isDirectory: false
                        console.log('isDirectory: ' + stat.isDirectory());
                        if (stat.isFile()) {
                            // 文件大小:    size: 181
                            console.log('size: ' + stat.size);
                            // 创建时间, Date对象:    birth time: Fri Dec 11 2015 09:43:41 GMT+0800 (CST)
                            console.log('birth time: ' + stat.birthtime);
                            // 修改时间, Date对象:    modified time: Fri Dec 11 2015 12:09:00 GMT+0800 (CST)
                            console.log('modified time: ' + stat.mtime);
                        }
                    }
                });
            ```
            
    - stream [文档](https://github.com/michaelliao/learn-javascript/tree/master/samples/node/stream)
        流的特点是数据是有序的，而且必须依次读取，或者依次写入，不能像Array那样随机定位.
        在Node.js中，流也是一个对象，我们只需要响应流的事件就可以了：data事件表示流的数据已经可以读取了，end事件表示这个流已经到末尾了，没有数据可以读取了，error事件表示出错了。
        ```javascript
            var fs = require('fs');
            // 打开一个流:
            var rs = fs.createReadStream('sample.txt', 'utf-8');
            rs.on('data', function (chunk) {
                console.log('DATA:')
                console.log(chunk);
            });
            rs.on('end', function () {
                console.log('END');
            });
            rs.on('error', function (err) {
                console.log('ERROR: ' + err);
            });
        ```
        要注意，data事件可能会有多次，每次传递的chunk是流的一部分数据.
        
        要以流的形式写入文件，只需要不断调用write()方法，最后以end()结束。
        ```javascript
          var fs = require('fs');
          var ws1 = fs.createWriteStream('output1.txt', 'utf-8');
          ws1.write('使用Stream写入文本数据...\n');
          ws1.write('END.');
          ws1.end();
          var ws2 = fs.createWriteStream('output2.txt');
          ws2.write(new Buffer('使用Stream写入二进制数据...\n', 'utf-8'));
          ws2.write(new Buffer('END.', 'utf-8'));
          ws2.end();
        ```
        所有可以读取数据的流都继承自stream.Readable，所有可以写入的流都继承自stream.Writable。
        
        - pipe
        就像可以把两个水管串成一个更长的水管一样，两个流也可以串起来。一个Readable流和一个Writable流串起来后，所有的数据自动从Readable流进入Writable流，这种操作叫pipe。
        让我们用pipe()把一个文件流和另一个文件流串起来，这样源文件的所有数据就自动写入到目标文件里了，所以，这实际上是一个复制文件的程序
        ```javascript
          var fs = require('fs');
          var rs = fs.createReadStream('sample.txt');
          var ws = fs.createWriteStream('copied.txt');
          rs.pipe(ws);
        ```
        默认情况下，当Readable流的数据读取完毕，end事件触发后，将自动关闭Writable流。如果我们不希望自动关闭Writable流，需要传入参数
        `readable.pipe(writable, { end: false });`
     
    - http
        要开发HTTP服务器程序，从头处理TCP连接，解析HTTP是不现实的。这些工作实际上已经由Node.js自带的http模块完成了。应用程序并不直接和HTTP协议打交道，而是操作http模块提供的request和response对象。
        request对象封装了HTTP请求，我们调用request对象的属性和方法就可以拿到所有HTTP请求的信息；
        response对象封装了HTTP响应，我们操作response对象的方法，就可以把HTTP响应返回给浏览器。
        ```javascript
          // 导入http模块:
          var http = require('http');
          // 创建http server，并传入回调函数:
          var server = http.createServer(function (request, response) {
              // 回调函数接收request和response对象,
              // 获得HTTP请求的method和url:
              console.log(request.method + ': ' + request.url);
              // 将HTTP响应200写入response, 同时设置Content-Type: text/html:
              response.writeHead(200, {'Content-Type': 'text/html'});
              // 将HTTP响应的HTML内容写入response:
              response.end('<h1>Hello world!</h1>');
          });
          // 让服务器监听8080端口:
          server.listen(8080);
          console.log('Server is running at http://127.0.0.1:8080/');
        ```
        [代码](https://github.com/michaelliao/learn-javascript/tree/master/samples/node/http)
        
    - crypto 
        crypto模块的目的是为了提供通用的加密和哈希算法。用纯JavaScript代码实现这些功能不是不可能，但速度会非常慢。Nodejs用C/C++实现这些算法后，通过cypto这个模块暴露为JavaScript接口，这样用起来方便，运行速度也快。
        - md5/sha1
        ```javascript
          const crypto = require('crypto');
          const hash = crypto.createHash('md5');
          hash.update('Hello, world!');
          hash.update('Hello, nodejs!');
          console.log(hash.digest('hex'))
        ```
        update()方法默认字符串编码为UTF-8，也可以传入Buffer。
        如果要计算SHA1，只需要把'md5'改成'sha1'，就可以得到SHA1的结果1f32b9c9932c02227819a4151feed43e131aca40。
        还可以使用更安全的sha256和sha512
    - Hmac
        Hmac算法也是一种哈希算法，它可以利用MD5或SHA1等哈希算法。不同的是，Hmac还需要一个密钥
        只要密钥发生了变化，那么同样的输入数据也会得到不同的签名，因此，可以把Hmac理解为用随机数“增强”的哈希算法。
        ```javascript
          const crypto = require('crypto');
          const hmac = crypto.createHmac('sha256', 'secret-key');
          hmac.update('Hello, world!');
          hmac.update('Hello, nodejs!');
          console.log(hmac.digest('hex')); // 80f7e22570...
        ```
    - AES
        AES是一种常用的对称加密算法，加解密都用同一个密钥。crypto模块提供了AES支持，但是需要自己封装好函数，便于使用
        ```javascript
          const crypto = require('crypto');
          function aesEncrypt(data, key) {
              const cipher = crypto.createCipher('aes192', key);
              var crypted = cipher.update(data, 'utf8', 'hex');
              crypted += cipher.final('hex');
              return crypted;
          }
          function aesDecrypt(encrypted, key) {
              const decipher = crypto.createDecipher('aes192', key);
              var decrypted = decipher.update(encrypted, 'hex', 'utf8');
              decrypted += decipher.final('utf8');
              return decrypted;
          }
          var data = 'Hello, this is a secret message!';
          var key = 'Password!';
          var encrypted = aesEncrypt(data, key);
          var decrypted = aesDecrypt(encrypted, key);
          console.log('Plain text: ' + data);
          //Plain text: Hello, this is a secret message!
          console.log('Encrypted text: ' + encrypted);
          //Encrypted text: 8a944d97bdabc157a5b7a40cb180e7...
          console.log('Decrypted text: ' + decrypted);
          //Decrypted text: Hello, this is a secret message!
        ```
        注意到AES有很多不同的算法，如aes192，aes-128-ecb，aes-256-cbc等，AES除了密钥外还可以指定IV（Initial Vector），不同的系统只要IV不同，用相同的密钥加密相同的数据得到的加密结果也是不同的。
        加密结果通常有两种表示方法：hex和base64，这些功能Nodejs全部都支持，但是在应用中要注意，如果加解密双方一方用Nodejs，另一方用Java、PHP等其它语言，需要仔细测试。
        如果无法正确解密，要确认双方是否遵循同样的AES算法，字符串密钥和IV是否相同，加密后的数据是否统一为hex或base64格式。
    
    - Diffie-Hellman
        DH算法是一种密钥交换协议，它可以让双方在不泄漏密钥的情况下协商出一个密钥来。
        注意每次输出都不一样，因为素数的选择是随机的。
        ```javascript
          const crypto = require('crypto');
          // xiaoming's keys:
          var ming = crypto.createDiffieHellman(512);
          var ming_keys = ming.generateKeys();
          var prime = ming.getPrime();
          var generator = ming.getGenerator();
          console.log('Prime: ' + prime.toString('hex'));
          //Prime: a8224c...deead3
          console.log('Generator: ' + generator.toString('hex'));
          //Generator: 02
          
          // xiaohong's keys:
          var hong = crypto.createDiffieHellman(prime, generator);
          var hong_keys = hong.generateKeys();
          
          // exchange and generate secret:
          var ming_secret = ming.computeSecret(hong_keys);
          var hong_secret = hong.computeSecret(ming_keys);
          
          // print secret:
          console.log('Secret of Xiao Ming: ' + ming_secret.toString('hex'));
          //Secret of Xiao Ming: 695308...d519be
          console.log('Secret of Xiao Hong: ' + hong_secret.toString('hex'));
          //Secret of Xiao Hong: 695308...d519be
        ```
    - RSA [参考源码](https://github.com/michaelliao/learn-javascript/tree/master/samples/node/crypto)
        RSA算法是一种非对称加密算法，即由一个私钥和一个公钥构成的密钥对，通过私钥加密，公钥解密，或者通过公钥加密，私钥解密。其中，公钥可以公开，私钥必须保密。
        RSA算法是1977年由Ron Rivest、Adi Shamir和Leonard Adleman共同提出的，所以以他们三人的姓氏的头字母命名。
        首先，在命令行执行以下命令以生成一个RSA密钥对
        `openssl genrsa -aes256 -out rsa-key.pem 2048`
        根据提示输入密码，这个密码是用来加密RSA密钥的，加密方式指定为AES256，生成的RSA的密钥长度是2048位。执行成功后，我们获得了加密的rsa-key.pem文件。
        第二步，通过上面的rsa-key.pem加密文件，我们可以导出原始的私钥.
        `openssl rsa -in rsa-key.pem -outform PEM -out rsa-prv.pem`
        输入第一步的密码，我们获得了解密后的私钥。
        类似的，我们用下面的命令导出原始的公钥
        `openssl rsa -in rsa-key.pem -outform PEM -pubout -out rsa-pub.pem`
        这样，我们就准备好了原始私钥文件rsa-prv.pem和原始公钥文件rsa-pub.pem，编码格式均为PEM。
        下面，使用crypto模块提供的方法，即可实现非对称加解密。
        首先，我们用私钥加密，公钥解密：
        ```javascript
          const
              fs = require('fs'),
              crypto = require('crypto');
          // 从文件加载key:
          function loadKey(file) {
              // key实际上就是PEM编码的字符串:
              return fs.readFileSync(file, 'utf8');
          }
          let
              prvKey = loadKey('./rsa-prv.pem'),
              pubKey = loadKey('./rsa-pub.pem'),
              message = 'Hello, world!';
          // 使用私钥加密:
          let enc_by_prv = crypto.privateEncrypt(prvKey, Buffer.from(message, 'utf8'));
          console.log('encrypted by private key: ' + enc_by_prv.toString('hex'));
          let dec_by_pub = crypto.publicDecrypt(pubKey, enc_by_prv);
          console.log('decrypted by public key: ' + dec_by_pub.toString('utf8'));
        ```
        执行后，可以得到解密后的消息，与原始消息相同。
        接下来我们使用公钥加密，私钥解密
        ```javascript
          // 使用公钥加密:
          let enc_by_pub = crypto.publicEncrypt(pubKey, Buffer.from(message, 'utf8'));
          console.log('encrypted by public key: ' + enc_by_pub.toString('hex'));
          // 使用私钥解密:
          let dec_by_prv = crypto.privateDecrypt(prvKey, enc_by_pub);
          console.log('decrypted by private key: ' + dec_by_prv.toString('utf8'));
        ```
        执行得到的解密后的消息仍与原始消息相同。
        如果我们把message字符串的长度增加到很长，例如1M，这时，执行RSA加密会得到一个类似这样的错误：data too large for key size，这是因为RSA加密的原始信息必须小于Key的长度。
        那如何用RSA加密一个很长的消息呢？实际上，RSA并不适合加密大数据，而是先生成一个随机的AES密码，用AES加密原始信息，然后用RSA加密AES口令，这样，实际使用RSA时，给对方传的密文分两部分，一部分是AES加密的密文，另一部分是RSA加密的AES口令。
        对方用RSA先解密出AES口令，再用AES解密密文，即可获得明文。
    
    - 证书
        crypto模块也可以处理数字证书。数字证书通常用在SSL连接，也就是Web的https连接。一般情况下，https连接只需要处理服务器端的单向认证，如无特殊需求（例如自己作为Root给客户发认证证书），建议用反向代理服务器如Nginx等Web服务器去处理证书。
        
#### 书签
[链接](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434501549492cdf5d4013db14fa9ad8ca172f0664345000)
