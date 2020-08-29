### JavaScript 的诞生 (具体详细资料参考阮一峰写的一系列文章)（这里 5/26 过一遍）

## HTML 是由一名叫 Tim Berners-Lee 的科学家发明的

## 哈肯·维姆·莱发明了 CSS

## 布莱登发明了 JS

### JS 的历史：

 完整的 Javascript 实现包括三部分：ECMAScript（欧洲计算机制造商协会）、文档对象模型、浏览器对象模型。

 Netspace 最初将其脚本语言命名为 LiveScript，后来 Netspace 在于 Sun 合作之后将其改名为 JavaScript。

 发展初期，JavaScript 的标准并未确定，同期有 Netscape 的 JavaScript，微软的 JScript 和 CEnvi 的 ScriptEase 三足鼎立。1997 年，在 ECMA（欧洲计算机制造商协会）的协调下，由 Netscape、Sun、微软、Borland 组成的工作组确定统一标准：ECMA-262。

"1994 年，网景公司（Netscape）发布了 Navigator 浏览器 0.9 版。这是历史上第一个比较成熟的网络浏览器，轰动一时。但是，这个版本的浏览器只能用来浏览，不具备与访问者互动的能力。......网景公司急需一种网页脚本语言，使得浏览器可以与网页互动。"

网页脚本语言到底是什么语言？网景公司当时有两个选择：一个是采用现有的语言，比如 Perl、Python、Tcl、Scheme 等等，允许它们直接嵌入网页；另一个是发明一种全新的语言。

这两个选择各有利弊。第一个选择，有利于充分利用现有代码和程序员资源，推广起来比较容易；第二个选择，有利于开发出完全适用的语言，实现起来比较容易。

 总之，当时的形势就是，网景公司的整个管理层，都是 Java 语言的信徒，Sun 公司完全介入网页脚本语言的决策。因此，Javascript 后来就是网景和 Sun 两家公司一起携手推向市场的，这种语言被命名为"Java+script"并不是偶然的。

### Javascript 的主观设计缺陷

## 主观原因导致的设计缺陷：

 1\*设计阶段过于仓促，仅用了 10 天。其次设计初衷是解决一些简单的网页互动。

 2\*没有先例：结合了函数式编程和面向对象编程的特点。

 3\*过早的标准化：95 年方案定稿，10 月解释器开发成功，12 月向市场推广。

###  JavaScript 的 10 个设计缺陷：

1\*不适合开发大型程序：Javascript 没有名称空间（namespace），很难模块化；没有如何将代码分布在多个文件的规范；允许同名函数的重复定义，后面的定义可以覆盖前面的定义，很不利于模块化加载。

2\*非常小的标准库：Javascript 提供的标准函数库非常小，只能完成一些基本操作，很多功能都不具备。

3\*null 和 undefined：null 属于对象（object）的一种，意思是该对象为空；undefined 则是一种数据类型，表示未定义。

typeof null; // object

typeof undefined; // undefined

两者非常容易混淆，但是含义完全不同。

var foo;

alert(foo == null); // true

alert(foo == undefined); // true

alert(foo === null); // false

alert(foo === undefined); // true

在编程实践中，null 几乎没用，根本不应该设计它。

##4\*全局变量难以控制：Javascript 的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性。

a = 1;

(function(){

b=2;

alert(a);

})(); // 1

alert(b); //2

## 5\*自动插入行尾分号：vJavascript 的所有语句，都必须以分号结尾。但是，如果你忘记加分号，解释器并不报错，而是为你自动加上分号。有时候，这会导致一些难以发现的错误。

比如，下面这个函数根本无法达到预期的结果，返回值不是一个对象，而是 undefined。

function(){

return
　　　　　　{
　　　　　　　　 i=1
　　　　　　};

}

原因是解释器自动在 return 语句后面加上了分号。

function(){

return;
　　　　　　{
　　　　　　　　 i=1
　　　　　　};

}

v

## 6\*加号运算符:+号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。

alert(1+10); // 11

alert("1"+"10"); // 110

如果一个操作项是字符，另一个操作项是数字，则数字自动转化为字符。

alert(1+"10"); // 110

alert("10"+1); // 101

这样的设计，不必要地加剧了运算的复杂性，完全可以另行设置一个字符连接的运算符。

## 7\*NaN:NaN 是一种数字，表示超出了解释器的极限。它有一些很奇怪的特性：

NaN === NaN; //false

NaN !== NaN; //true

alert( 1 + NaN ); // NaN

与其设计 NaN，不如解释器直接报错，反而有利于简化程序。

## 8\*数组和对象的区分:由于 Javascript 的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。Douglas Crockford 的代码是这样的：

if ( arr &&
　　　　 typeof arr === 'object' &&
　　　　 typeof arr.length === 'number' &&
　　　　!arr.propertyIsEnumerable('length')){

alert("arr is an array");

}

## 9\*== 和 ===:==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉。

"" == "0" // false

0 == "" // true

0 == "0" // true

false == "false" // false

false == "0" // true

false == undefined // false

false == null // false

null == undefined // true

" \t\r\n" == 0 // true

因此，推荐任何时候都使用"==="（精确判断）比较符。

## 10\*:基本类型的包装对象:Javascript 有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。

new Boolean(false);

new Number(1234);

new String("Hello World");

与基本数据类型对应的对象类型，作用很小，造成的混淆却很大。

alert( typeof 1234); // number

alert( typeof new Number(1234)); // object

关于 Javascript 的更多怪异行为，请参见 Javascript Garden 和 wtfjs.com。
