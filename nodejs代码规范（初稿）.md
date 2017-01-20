
# 1.说明
- 参考来源：  
Felix Node.js Style Guide: [中文](https://github.com/dead-horse/node-style-guide/)  [英文](https://github.com/felixge/node-style-guide) 
- 文档未尽内容，可以参考上述文档
# 2.常用内容列举参考
## Formatting
### 2空格缩进(2 spaces for indentation)
使用2个空格缩进而不是tab进行代码段缩进，尽量不要tab与空格混用，因为在不同的编辑器中tab可能被认为是4个spaces or 2 spaces

### 换行(Newlines)
使用 UNIX 风格的换行符 (`\n`)，同时在每个文件的结尾添加一个换行符。
Windows 风格的换行符 (`\r\n`) 是绝对禁止出现在任何项目中的。

### 去除行末尾的多余空格(No trailing whitespace)
就像吃完饭要刷牙一样，在提交 (commit) 代码之前你需要清理掉所有的不必要的空格。

### 使用分号(Use Semicolons)
是否使用分号，在社区争论已久。
isaac 也写过一篇讨论的[文章](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding)，
但是，当可以用廉价的语法来消除一些可能引入的错误的时候，请当一个保守派。

### 使用单引号(Use single quotes)

除非编写.json文件，其他时候都请用单引号包裹字符串。

*Right:*

```js
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
```

### 大括号位置(Opening braces go on the same line)

请把你的所有的左大括号都放在语句开始的这一行。

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

同时，请注意在条件判断前后都添加一个空格。

### 每个变量声明都带一个 var(Declare one variable per var statement)

每个变量声明都带一个 var ，这样删除或者调整变量声明的顺序会更加容易。
不要把变量都声明在最前面，而是声明在它最有意义的地方。

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (items.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (items.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

## Naming Conventions

### 变量、属性和函数名都采用小驼峰( Use lowerCamelCase for variables, properties and function names)

变量、属性和函数的命名风格都需要遵循小驼峰风格。
同时所有的命名都是有意义的。
尽量避免用单字符变量和少见单词来命名。

*Right:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
var a = db.query('SELECT * FROM users ...');
```

### 类名采用大驼峰(Use UpperCamelCase for class names)

类名都采用大驼峰风格来命名。

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

### 用大写来标识常量(Use UPPERCASE for Constants)

常量变量和对象的静态常量属性都需要特殊表明，通过全部大写的方式来表明。

尽管 Node.js / V8 支持 mozilla 的 [const][const] 关键字，
但是不幸的是，对象的属性并不支持这个关键字，而且 const 没有包含于任何一个 ECMA 规范中。

*Right:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Variables
### 对象、数组的创建(Object/Array Creation)
使用尾随逗号，尽量用一行来声明，只有在编译器不接受的情况下才把对象的 key 用单引号包裹。
使用字面表达式，用 `{}, []` 代替 `new Array, new Object`。

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### 使用 === 比较符( Use the === operator)

写代码并不是在背这些 [stupid rules][comparisonoperators] 。使用 `===` 操作符来进行比较操作，它会完全按照你的期望来执行。

*Right:*

```js
var a = 0;
if (a === '') {
  console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### 三元操作符分多行(Use multi-line ternary operator)

三元操作符不应该写在一行，将它分割到多行。

*Right:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*Wrong:*

```js
var foo = (a === b) ? 1 : 2;
```
### 使用有意义的判断条件(Use descriptive conditions)

所有复杂的条件判断都需要赋予一个有意义的名字或者方法。

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```
## Functions

### 写精简的函数(Write small functions)

保持你的函数尽可能的精简。
一个好的函数应该能够在幻灯片上一屏显示，并且让坐在教室最后一排的人看清楚。
别再去数你的每一个函数并控制在15行以内了。

### 尽早的从函数中返回(Return early from functions)

为了避免深入嵌套的 if 语句，请尽早的从函数中返回。

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

针对这个示例，甚至可以进一步精简优化：

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### 给你的闭包命名(Name your closures)

请尽量给你的闭包、匿名函数命名。
这让人知道你在意这个函数，更重要的是，这将会产生可读性更好的堆栈跟踪和CPU调用信息等。

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function() {
  console.log('losing');
});
```

### 不要嵌套闭包(No nested closures)

使用闭包，但是不要嵌套他们，否则你的代码将会一团糟。

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

### 方法链(Method chaining)
如果你想使用方法链，最好每个方法单独占一行
缩进这些方法以尽早显示它们在同一个方法链上


*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

## Comments

### 使用单行注释风格(Use slashes for comments)

不管是单行注释还是多行注释，都使用 `//` 。
同时请尝试在更高层次来编写注释（解释函数整体的思路），
只在解释一些难以理解代码的时候添加注释，而不是给一些琐碎的东西加上注释。

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```
## Miscellaneous(其他)

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

这一堆屎一样的东西，你永远都不会需要他们。

### Requires 在程序文件开始(Requires At Top)

始终把requires放在程序文件的开始，一目了然的看到程序依赖

### Getters 和 Setters

不要使用 setters ，他们会引发一些使用你的代码的人无法解决的问题。
当没有[副作用][sideeffect]的时候，可以使用 getters，例如提供一个集合类的长度属性的时候。

### 不要扩展内建类型(Do not extend built-in prototypes)

不要扩展 javascript 内建对象的方法。将来的你会感谢你这个做法的。

*Right:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```
