# Modern JavaScript Cheatsheet 正體中文版

![Modern JavaScript cheatsheet](https://i.imgur.com/aexPxMb.png)
<small>圖片來源: [Ahmad Awais ⚡️](https://github.com/ahmadawais)</small>

## 介紹

### 動機

本文檔整理了各種現代化 JavaScript 開發過程中經常使用到的腳本。

該份指南的目標並不是放在幫助初學者從零基礎到入門，而是為了幫助那些因為 Javascript 新式語法導致可能很難熟悉現代函數庫使用方式 (以 React 做為舉例) 的開發人員。

此外我也會偶爾提供一些個人主觀的建議和技巧，而這些建議可能會造成部分的爭議性，但請務必留意，當我做出這些舉例時這僅僅是出自於個人的推薦作法。

> **注意:** 此處介紹的大部分概念出自於 JavaScript 的語言更新 (ES2015，更多人稱其作 ES6)。你可以在[這個好地方](http://es6-features.org)找到更多添加的新功能。

### 配套資源

當你在試圖理解一個新概念時，我建議你可以去瀏覽以下這些資源尋找解答：

- [MDN (Mozilla Developer Network)](https://developer.mozilla.org/fr/search?q=)
- [You don't know JS (book)](https://github.com/getify/You-Dont-Know-JS)
- [ES6 Features with examples](http://es6-features.org)
- [WesBos blog (ES6)](http://wesbos.com/category/es6/)
- [Reddit (JavaScript)](https://www.reddit.com/r/javascript/)
- [Google](https://www.google.com/) 搜尋特定相關主題的部落格文章和資源

## 目錄

- [Modern JavaScript cheatsheet 繁體中文版](#modern-javascript-cheatsheet)
  * [介紹](#introduction)
    + [動機](#motivation)
    + [配套資源](#complementary-resources)
  * [目錄](#table-of-contents)
  * [概念](#notions)
    + [變數聲明： var, const, let](#variable-declaration-var-const-let)
      - [簡短解釋](#short-explanation)
      - [範例程式碼](#sample-code)
      - [詳細說明](#detailed-explanation)
      - [外部資源](#external-resource)
    + [箭頭函數](#-arrow-function)
      - [範例程式碼](#sample-code-1)
      - [詳細說明](#detailed-explanation-1)
        * [簡潔性](#concision)
        * [*this* 關鍵字參照](#this-reference)
      - [有用資源](#useful-resources)
    + [函數預設值](#function-default-parameter-value)
      - [外部資源](#external-resource-1)
    + [objects 和 arrays 的解耦](#destructuring-objects-and-arrays)
      - [說明和範例程式碼](#explanation-with-sample-code)
      - [有用資源](#useful-resources-1)
    + [Array 的操作方法 - map / filter / reduce](#array-methods---map--filter--reduce)
      - [範例程式碼](#sample-code-2)
      - [說明](#explanation)
        * [Array.prototype.map()](#arrayprototypemap)
        * [Array.prototype.filter()](#arrayprototypefilter)
        * [Array.prototype.reduce()](#arrayprototypereduce)
      - [外部資源](#external-resource)
    + [展開運算子 "..."](#spread-operator-)
      - [範例程式碼](#sample-code-3)
      - [說明](#explanation-1)
        * [迭代用法 (如同 array)](#in-iterables-like-array)
        * [不定參數](#function-rest-parameter)
        * [Object 屬性擴展](#object-properties-spreading)
      - [外部資源](#external-resources)
    + [Object 屬性簡寫](#object-property-shorthand)
      - [說明](#explanation-2)
      - [外部資源](#external-resources-1)
    + [Promises](#promises)
      - [範例程式碼](#sample-code-4)
      - [說明](#explanation-3)
        * [創造 promise](#create-the-promise)
        * [使用 promise](#use-the-promise)
      - [外部資源](#external-resources)
    + [模板字符串](#template-literals)
      - [範例程式碼](#sample-code-5)
      - [外部資源](#external-resources-2)
    + [Imports / Exports](#imports--exports)
      - [說明與範例程式碼](#explanation-with-sample-code-1)
      - [外部資源](#external-resources-3)
    + [JavaScript *this*](#-javascript-this)
      - [外部資源](#external-resources-4)
    + [Class](#class)
      - [範例](#samples)
      - [外部資源](#external-resources-5)
    + [Async Await](#async-await)
      - [範例程式碼](#sample-code-6)
      - [說明](#explanation-4)
      - [外部資源](#external-resources-7)
  * [術語詞彙](#glossary)
    + [作用域範圍](#-scope)
    + [Variable mutation](#-variable-mutation)

## 概念

### 變數聲明： var, const, let

在 JavaScript 中有三個不同關鍵字可用於宣告一個變數，分別是 ```var```， ```let``` 和 ```const```。

#### 簡短解釋

使用 ```const``` 關鍵字宣告的變數無法被重新指派, 而 ```let``` 和 ```var``` 是可以的。

我會建議在默認情況下一律使用 ```const``` ，當你需要<i>改變</i>它或是稍後才重新指派時才使用 ```let``` 。

<table>
  <tr>
    <th></th>
    <th>作用域範圍</th>
    <th>是否可重新指派</th>
    <th>狀態變更</th>
   <th><a href="#tdz_sample">暫時性死區 (Temporal Dead Zone)</a></th>
  </tr>
  <tr>
    <th>const</th>
    <td>區塊</td>
    <td>不是</td>
    <td><a href="#const_mutable_sample">是</a></td>
    <td>是</td>
  </tr>
  <tr>
    <th>let</th>
    <td>區塊</td>
    <td>是</td>
    <td>是</td>
    <td>是</td>
  </tr>
   <tr>
    <th>var</th>
    <td>函數</td>
    <td>是</td>
    <td>是</td>
    <td>不是</td>
  </tr>
</table>

#### 範例程式碼

```javascript
const person = "Nick";
person = "John" // 會有錯誤跳出，person 不能被重新指派
```

```javascript
let person = "Nick";
person = "John";
console.log(person) // "John" 在 let 的使用下允許被重新指派
```

#### 詳細說明

變數的 [*作用域範圍 (scope)*](#scope_def) 大致上意味著 "這個變數的效力可被作用在哪段程式碼 (where is this variable available in the code)"。

##### var

```var``` 宣告的變數是 *函數範圍 (function scoped)* 的，這表示當函數中創造變數的時候，該函數中的所有內容都可以訪問並使用該變數。相反的，在函數外創造的 *區塊範圍 (block scoped)* 變數則無法被使用。

我會建議你把它看作是一個 *X scoped* 範圍的變數代表著這個變數是 X 的屬性之一。

```javascript
function myFunction() {
  var myVar = "Nick";
  console.log(myVar); // "Nick" - myVar 可以在函數範圍之內被使用
}
console.log(myVar); // Undefined, myVar 在函數範圍外部無法被使用
```

持續觀察變數的作用域範圍，這裡有個更細微的範例：

```javascript
function myFunction() {
  var myVar = "Nick";
  if (true) {
    var myVar = "John";
    console.log(myVar); // "John"
    // actually, myVar 是函數範圍之內的，我們剛剛覆蓋了之前的 myVar 變數，值從 "Nick" 變成 "John"
  }
  console.log(myVar); // "John" - 印出來看看區塊如何影響 myVar 這個變數的值
}
console.log(myVar); // Undefined, myVar 在函數範圍外部無法被使用
```

此外， *var* 宣告出來的變數在程式執行之時就會被移到作用域的頂部。這個就是我們所說的[變數提升 (var hoisting)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting)。

這段程式碼：

```js
console.log(myVar) // undefined -- 沒有錯誤發生
var myVar = 2;
```

在程式執行過程中被解讀為：

```js
var myVar;
console.log(myVar) // undefined -- 沒有錯誤發生
myVar = 2;
```

##### let

```var``` 和 ```let ``` 大致上行為相同， ```let``` 在宣告變數時

- 作用域是 *區塊範圍 (block scoped)*
- 在被指派值以前 **無法** 被存取使用
- 同一個作用域之下不能被重新宣告

採用我們前面的例子來看看區塊範圍 (block scoped) 的影響：

```javascript
function myFunction() {
  let myVar = "Nick";
  if (true) {
    let myVar = "John";
    console.log(myVar); // "John"
    // 事實上，myVar 是區塊範圍之內的，我們剛剛創造了一個全新的 myVar 變數
    // 這個變數是無法從區塊範圍以外的地方存取，
    // 而且它也是完全獨立於我們創造的第一個 myVar 變數！
  }
  console.log(myVar); // "Nick", 查看 if 區塊中的程式會不會影響到 myVar 這個值
}
console.log(myVar); // Undefined, myVar 在函數範圍外部無法被使用
```

<a name="tdz_sample"></a> 現在我們來看看 *let* ( 和 *const* ) 變數在被賦值以前無法被使用是什麼意思：

```js
console.log(myVar) // 觸發 ReferenceError 錯誤!
let myVar = 2;
```

和 *var* 變數比較之下，如果在指派 *let* 或是 *const* 變數的值之前嘗試讀取或是寫入的動作是會引發錯誤的。這種現象通常被稱之為 [*Temporal dead zone*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_Dead_Zone_and_errors_with_let) 或者是 *TDZ*。

> **注意：** 技術上而言， *let* 和 *const* 變數在聲明時也是會被提升的，但並不是指它們的賦值。因為他們在被指派之前是不能使用的，所以直觀上就像是沒有提升一樣，但它們其實是有的。如果你想知道更多的話請查看 [更加詳細解釋的這篇文章](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)。

此外，你不能重新宣告一個 *let* 變數：

```js
let myVar = 2;
let myVar = 3; // 跳出 SyntaxError 錯誤
```

##### const

```const``` 宣告出來的行為如同 *let* 變數，但它們同樣都不能被重新指派。

總結一下， *const* 變數：

- 作用域是 *區塊範圍 (block scoped)*
- 在被指派值以前 **無法** 被存取使用
- 同一個作用域之下不能被重新宣告
- 無法被重新指派新值

```js
const myVar = "Nick";
myVar = "John" // 跳出錯誤，不允許重新指派新值
```

```js
const myVar = "Nick";
const myVar = "John" // 跳出錯誤， 重新宣告是不被允許的
```

<a name="const_mutable_sample"></a> 但有個精妙之處 : ```const``` 變數是不[**可變的**](#mutation_def) ! 更具體而言，這代表著 *object* 和 *array* 中由 ```const``` 宣告出來的變數是 **可以** 被改變的。

對於 objects：

```js
const person = {
  name: 'Nick'
};
person.name = 'John' // 這完全可行！ person 這個變數尚未完全被重新指派，但它確實改變了
console.log(person.name) // "John"
person = "Sandra" // 跳出錯誤，因為重新指派時是不允許使用 const 宣告出來的變數的
```

對於 arrays：

```js
const person = [];
person.push('John'); // 這完全可行！ person 這個變數尚未完全被重新指派，但它確實改變了 
console.log(person[0]) // "John"
person = ["Nick"] // 跳出錯誤，因為重新指派時是不允許使用 const 宣告出來的變數的
```

#### 外部資源

- [How let and const are scoped in JavaScript - WesBos](http://wesbos.com/javascript-scoping/)
- [Temporal Dead Zone (TDZ) Demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)

### <a name="arrow_func_concept"></a> 箭頭函數

ES6 的更新正式引入了 *箭頭函數 (arrow functions)*，這是另外一種宣告和使用函數的方法。以下是它們所帶來的好處：

- 更為簡潔
- *this* 的值繼承自外圍作用域 (*this* is picked up from surroundings)
- 隱式回傳 (implicit return)

#### 範例程式碼

- 簡潔性和隱式回傳 (implicit return)

```js
function double(x) { return x * 2; } // 傳統作法
console.log(double(2)) // 4
```

```js
const double = x => x * 2; // 仍然是同樣的函數，寫成帶有隱式回傳的作法
console.log(double(2)) // 4
```

- *this* 關鍵字參照

在箭頭函數中， *this* 意味著封閉執行上下文的 *這個值*。基本上，透過使用箭頭函數，在函數中調用函數之前，你不需要去使用像是 "that = this" 這樣的用法。

```js
function myFunc() {
  this.myVar = 0;
  setTimeout(() => {
    this.myVar++;
    console.log(this.myVar) // 1
  }, 0);
}
```

#### 詳細說明

##### 簡潔性

箭頭函數在諸多方面都較傳統函數來的更為簡潔。讓我們來看看所有可能的情況：

- 隱式回傳 VS 顯式回傳

 **顯式回傳 (explicit return)** 是指在函數中明確的使用 *return* 這個關鍵字。

```js
  function double(x) {
    return x * 2; // 這個函數顯式回傳了 x * 2，並且使用了 return 這個關鍵字
  }
```

以傳統的作法撰寫，return 永遠都會是顯式的。但是如果是使用箭頭函數，你可以執行隱式回傳，這同時代表著你不需要使用關鍵字 return 去取得回傳值。

要做隱式回傳，程式碼必須用一行句子撰寫。

```js
  const double = (x) => {
    return x * 2; // 此處顯示 return 值
  }
```

由於這裡只有一個回傳值，我們可以做一個隱式回傳。

```js
 const double = (x) => x * 2;
```

做到上述的轉換，我們只需要 **移除括號** 以及 **return** 這個關鍵字。這就是為什麼它會被稱為 *隱式* 回傳，*return* 關鍵字不在了，但是這個函數確實會回傳 ```x * 2```。

> **注意：** 如果你的函數沒有回傳一個值 (這種作法有 *副作用*)，那麼它將不屬於顯式或是隱式返回中的任一種。

- 只有一個參數

如果你的函數只接受一個參數，你可以省略它周圍的括號。如果我們拿上述的 *double* 程式碼做為舉例：

```js
 const double = (x) => x * 2; // 這個箭頭函數只接受一個參數
```

括號是可以被省略的：

```js
 const double = x => x * 2; // 這個箭頭函數只接受一個參數
```

- 沒有參數

當沒有為箭頭函數提供任何參數時，你就必須加上括號，否則語法將會出錯。

```js
  () => { // 有加上括號，一切都正常運作
    const x = 2;
    return x;
  }
```

```js
  => { // 沒有括號，這樣的語法是行不通的！
    const x = 2;
    return x;
  }
```

##### *this* 關鍵字參照

要理解箭頭函數的精妙之處，你一定要清楚 [this](#this_def) 在 JavaScript 中是如何運作的。

在一個箭頭函數當中，*this* 等同於封閉執行上下文的 *這個值* 。意思就是說，一個箭頭函數並不會創造一個新的 *this*，而是從它的外圍作用域一併抓起。

沒有箭頭函數的這項功能，如果你想要取得位於函數的函數內部由 *this* 參照的變數，你就只能使用 *that = this* 或者是 *self = this* 這樣的技巧。

舉例來說，你在 myFunc 函數中使用 setTimeout 函數：

```js
function myFunc() {
  this.myVar = 0;
  var that = this; // 使用 that = this 這個技巧
  setTimeout(
    function() { // 創造了一個新的 this 
      that.myVar++;
      console.log(that.myVar) // 1

      console.log(this.myVar) // undefined -- 詳見上述的函數宣告
    },
    0
  );
}
```

但如果你使用了箭頭函數，*this* 的範圍將會是它的外圍作用域：

```js
function myFunc() {
  this.myVar = 0;
  setTimeout(
    () => { // this 的值來自於它的外圍作用域，也就是 myFunc 函數
      this.myVar++;
      console.log(this.myVar) // 1
    },
    0
  );
}
```

#### 有用資源

- [Arrow functions introduction - WesBos](http://wesbos.com/arrow-functions/)
- [JavaScript arrow function - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Arrow function and lexical *this*](https://hackernoon.com/javascript-es6-arrow-functions-and-lexical-this-f2a3e2a5e8c4)

### 函數預設值

從 ES2015 JavaScript 更新之後，你可以透過下列的語法為函數中的參數設定預設值：

```js
function myFunc(x = 10) {
  return x;
}
console.log(myFunc()) // 10 -- 沒有提供任何值，所以 10 在 myFunc 中做為預設值指派給 x
console.log(myFunc(5)) // 5 -- 有提供一個參數值，所以 x 在 myFunc 中等於 5   

console.log(myFunc(undefined)) // 10 -- 未定義的值，所以預設值被指派給 x
console.log(myFunc(null)) // null -- 提供一個值 (null)，詳細資料請見下文
```

預設值若且為若應用在兩種情況：

- 沒有傳入任何參數
- 傳入 *undefined* 這個參數

換句話說，如果你傳入的是 *null* ，那麼預設值的機制是不會被觸發的。

> **注意：** 預設值的指派可以搭配解耦參數一同使用 (參照下一個概念的實際例子)

#### 外部資源

- [Default parameter value - ES6 Features](http://es6-features.org/#DefaultParameterValues)
- [Default parameters - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

### objects 和 arrays 的解耦

*解耦 (Destructuring)* 的概念是從 objects 或是 arrays 當中提取部分用值一種相當方便的方法。

舉個簡單的實例，*destructuring* 可以被用來解耦函數中的參數或者像是 React 專案中 *this.props* 這樣的用法。

#### 說明和範例程式碼

- Object

試著想想以下這個 object：

```js
const person = {
  firstName: "Nick",
  lastName: "Anderson",
  age: 35,
  sex: "M"
}
```

沒有解耦的作法，你只能這樣做：

```js
const first = person.firstName;
const age = person.age;
const city = person.city || "Paris";
```

使用解耦，你只需要一行：

```js
const { firstName: first, age, city = "Paris" } = person; // 這樣就搞定了！

console.log(age) // 35 -- 一個名為 age 的新變數被創建出來了，其值等同於 person.age
console.log(first) // "Nick" -- 一個名為 first 的新變數被創建出來了，其值等同於person.firstName
console.log(firstName) // Undefined -- person.firstName 雖然存在，但是有個叫做 first 的新變數更早之前被創建了
console.log(city) // "Paris" -- 一個名為 city 的新變數被創建出來了，同時因為 person.city 是未被定義的，所以 city 將等同於預設值也就是 "Paris"。
```

**注意：** 在 ```const { age } = person;```當中， *const* 後的括號並不是用來宣告 object 或者是區塊，僅僅是 *解耦 (destructuring)* 的使用語法。

- 帶有參數的函數用法

*解耦 (Destructuring)* 經常被用來解 objects 中的參數。

沒有解耦的作法，你只能這樣做：

```js
function joinFirstLastName(person) {
  const firstName = person.firstName;
  const lastName = person.lastName;
  return firstName + '-' + lastName;
}

joinFirstLastName(person); // "Nick-Anderson"
```

在解耦 obejct 當中 *person* 這個參數時，我們可以得到一個更簡潔的函數：

```js
function joinFirstLastName({ firstName, lastName }) { 
  // 我們透過解耦 person 分別創造了 firstName 和 lastName 這兩個變數
  return firstName + '-' + lastName;
}

joinFirstLastName(person); // "Nick-Anderson"
```

解耦搭配[箭頭函數](#arrow_func_concept)使得開發過程更加愉快：

```js
const joinFirstLastName = ({ firstName, lastName }) => firstName + '-' + lastName;

joinFirstLastName(person); // "Nick-Anderson"
```

- Array

讓我們來想想下列這個 array：

```js
const myArray = ["a", "b", "c"];
```

沒有解耦的作法，你只能這樣做：

```js
const x = myArray[0];
const y = myArray[1];
```

使用解耦的作法：

```js
const [x, y] = myArray; // 就是這麼簡單！

console.log(x) // "a"
console.log(y) // "b"
```

#### 有用資源

- [ES6 Features - Destructuring Assignment](http://es6-features.org/#ArrayMatching)
- [Destructuring Objects - WesBos](http://wesbos.com/destructuring-objects/)
- [ExploringJS - Destructuring](http://exploringjs.com/es6/ch_destructuring.html)

### Array 的操作方法 - map / filter / reduce

*Map*，*filter* 和 *reduce* 都是 array 提供的方法，它們源自於 [*functional programming*](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0) 開發範式。

總結一下：

- **Array.prototype.map()** 接受一組 array，針對其中的元素進行某些操作和轉換的動作。
- **Array.prototype.filter()** 接受一組 array，依照元素本身決定是否保留，並且將會回傳一個僅含有保留元素的 array
- **Array.prototype.reduce()** 接受一組 array，將這些元素合併成一個值並回傳

我會建議在開發時盡可能的遵循函數式編程 (functional programming) 的原則，因為它們是可組合的，簡潔且優雅的。

透過這三種方法，你將可以避免在大多數情況下使用 *for* 和 *forEach*。當你想做一個 *for* 迴圈時，試著用 *map*，*filter* 和 *reduce* 組合看看。起初你可能會覺得窒礙難行，因為它需要你學習一種新的思維方式，但一旦你掌握它了，事情也將變得更加容易。

#### 範例程式碼

```js
const numbers = [0, 1, 2, 3, 4, 5, 6];
const doubledNumbers = numbers.map(n => n * 2); // [0, 2, 4, 6, 8, 10, 12]
const evenNumbers = numbers.filter(n => n % 2 === 0); // [0, 2, 4, 6]
const sum = numbers.reduce((prev, next) => prev + next, 0); // 21
```

透過 map，filter 和 reduce 這幾種組合技去計算出學生成績 >= 10 的總和：

```js
const students = [
  { name: "Nick", grade: 10 },
  { name: "John", grade: 15 },
  { name: "Julia", grade: 19 },
  { name: "Nathalie", grade: 9 },
];

const aboveTenSum = students
  .map(student => student.grade) // map the students array to an array of their grades
  .filter(grade => grade >= 10) // we filter the grades array to keep those above 10
  .reduce((prev, next) => prev + next, 0); // we sum all the grades above 10 one by one

console.log(aboveTenSum) // 44 -- 10 (Nick) + 15 (John) + 19 (Julia), Nathalie below 10 is ignored
```

#### 說明

讓我們來思考下列這個 array：

```js
const numbers = [0, 1, 2, 3, 4, 5, 6];
```

##### Array.prototype.map()

```js
const doubledNumbers = numbers.map(function(n) {
  return n * 2;
});
console.log(doubledNumbers); // [0, 2, 4, 6, 8, 10, 12]
```
發生了什麼事？我們在 *numbers* 這個 array 中使用了 .map 方法，map 將會去迭代 array 中的每一個元素並且回傳給我們的函數。該函數的目標是生成並回傳一個新的值使得 map 可以替換掉原本的 array。

讓我們提取這個函數以便讓解釋更清楚：

```js
const doubleN = function(n) { return n * 2; };
const doubledNumbers = numbers.map(doubleN);
console.log(doubledNumbers); // [0, 2, 4, 6, 8, 10, 12]
```

```numbers.map(doubleN)``` 將會產生 ```[doubleN(0), doubleN(1), doubleN(2), doubleN(3), doubleN(4), doubleN(5), doubleN(6)]``` ，而它們分別等同於 ```[0, 2, 4, 6, 8, 10, 12]```。

> **注意：** 如果你不需要回傳一個新的 array 且只想實作一個帶有副作用的迴圈，使用 for / forEach 迴圈會更為符合你所需。

##### Array.prototype.filter()

```js
const evenNumbers = numbers.filter(function(n) {
  return n % 2 === 0; // true if "n" is par, false if "n" isn't
});
console.log(evenNumbers); // [0, 2, 4, 6]
```

我們在這個充滿 *numbers* 的 array 上使用 .filter 方法，過濾器將會遍歷當中的每一個元素並回傳給我們的函數。函數的目標是回傳一個布林值，它將會確定當前值是否被保留。過濾之後回傳的是一個僅保留所需值的 array。

##### Array.prototype.reduce()

reduce 方法的目標是將進行迭代的 array 中的所有元素 *減少* 到只留下單一值。計算這些元素的方式將取決於你的需求。

```js
const sum = numbers.reduce(
  function(acc, n) {
    return acc + n;
  },
  0 // 進行迭代計算的初始值
);

console.log(sum) //21
```

就像 .map 和 .filter 方法一樣， .reduce 方法被應用在 array 上並將函數做為第一個參數。


這次有些變化了：

- .reduce 接受兩個參數

第一個參數是在每個迭代步驟中調用的函數。

第二個參數是在第一個迭代步驟（讀取下一個之用）的累加器變數的值（此處是 *acc*）。

- 帶有參數的函數用法

做為 .reduce 的第一個參數所傳遞的函數需要兩個參數。第一個（此處是 *acc*）是累加器變數，而第二個參數（*n*）則是當前元素。

累加器變數的值等於 **上一次** 迭代步驟中函數的回傳值。在迭代過程的第一步，*acc* 等於你做為 .reduce 時第二個參數所傳遞的值。

###### 進行第一次迭代

```acc = 0``` 因為我們把 0 做為 reduce 的第二個參數

```n = 0```  *number* array 的第一個元素

函數回傳 *acc* + *n* --> 0 + 0 --> 0

###### 進行第二次迭代

```acc = 0``` 因為它是上次迭代所回傳的值 

```n = 1``` *number* array 的第二個元素

函數回傳 *acc* + *n* --> 0 + 1 --> 1

###### 進行第三次迭代

```acc = 1``` 因為它是上次迭代所回傳的值 

```n = 2``` *number* array 的第三個元素

函數回傳 *acc* + *n* --> 1 + 2 --> 3

###### 進行第四次迭代

```acc = 3``` 因為它是上次迭代所回傳的值

```n = 3``` *number* array 的第四個元素

函數回傳 *acc* + *n* --> 3 + 3 --> 6

###### [...] 進行最後一次迭代

```acc = 15``` 因為它是上次迭代所回傳的值

```n = 6``` *number* array 的最後一個元素

函數回傳 *acc* + *n* --> 15 + 6 --> 21

因為它是最後一個迭代步驟了， **.reduce** 將回傳 21。

#### 外部資源

- [Understanding map / filter / reduce in JS](https://hackernoon.com/understanding-map-filter-and-reduce-in-javascript-5df1c7eee464)

### 展開運算子 "..."

The spread operator ```...``` has been introduced with ES2015 and is used to expand elements of an iterable (like an array) into places where multiple elements can fit.

#### 範例程式碼

```js
const arr1 = ["a", "b", "c"];
const arr2 = [...arr1, "d", "e", "f"]; // ["a", "b", "c", "d", "e", "f"]
```

```js
function myFunc(x, y, ...params) {
  console.log(x);
  console.log(y);
  console.log(params)
}

myFunc("a", "b", "c", "d", "e", "f")
// "a"
// "b"
// ["c", "d", "e", "f"]
```

```js
const { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1
console.log(y); // 2
console.log(z); // { a: 3, b: 4 }

const n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 }
```

#### 說明

##### 迭代用法 (如同 array)

If we have the two following arrays:

```js
const arr1 = ["a", "b", "c"];
const arr2 = [arr1, "d", "e", "f"]; // [["a", "b", "c"], "d", "e", "f"]
```

*arr2* the first element is an array because *arr1* is injected as is into *arr2*. But what we want is *arr2* to be an array of letters. To do so, we can *spread* the elements of *arr1* into *arr2*.

With spread operator

```js
const arr1 = ["a", "b", "c"];
const arr2 = [...arr1, "d", "e", "f"]; // ["a", "b", "c", "d", "e", "f"]
```

##### 不定參數

In function parameters, we can use the rest operator to inject parameters into an array we can loop in. There is already an **argument** object bound to every function that is equal to an array of all the parameters passed into the function.

```js
function myFunc() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

myFunc("Nick", "Anderson", 10, 12, 6);
// "Nick"
// "Anderson"
// 10
// 12
// 6
```

But let's say that we want this function to create a new student with its grades and with its average grade. Wouldn't it be more convenient to extract the first two parameters into two separate variables, and then have all the grades in an array we can iterate over?

That's exactly what the rest operator allows us to do!

```js
function createStudent(firstName, lastName, ...grades) {
  // firstName = "Nick"
  // lastName = "Anderson"
  // [10, 12, 6] -- "..." takes all other parameters passed and creates a "grades" array variable that contains them

  const avgGrade = grades.reduce((acc, curr) => acc + curr, 0) / grades.length; // computes average grade from grades

  return {
    firstName: firstName,
    lastName: lastName,
    grades: grades,
    avgGrade: avgGrade
  }
}

const student = createStudent("Nick", "Anderson", 10, 12, 6);
console.log(student);
// {
//   firstName: "Nick",
//   lastName: "Anderson",
//   grades: [10, 12, 6],
//   avgGrade: 9,33
// }
```

> **Note:** createStudent function is bad because we don't check if grades.length exists or is different from 0. But it's easier to read this way, so I didn't handle this case.

##### Object 屬性擴展

For this one, I recommend you read previous explanations about the rest operator on iterables and function parameters.

```js
const myObj = { x: 1, y: 2, a: 3, b: 4 };
const { x, y, ...z } = myObj; // object destructuring here
console.log(x); // 1
console.log(y); // 2
console.log(z); // { a: 3, b: 4 }

// z is the rest of the object destructured: myObj object minus x and y properties destructured

const n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 }

// Here z object properties are spread into n
```

#### 外部資源

- [TC39 - Object rest/spread](https://github.com/tc39/proposal-object-rest-spread)
- [Spread operator introduction - WesBos](https://github.com/wesbos/es6-articles/blob/master/28%20-%20Spread%20Operator%20Introduction.md)
- [JavaScript & the spread operator](https://codeburst.io/javascript-the-spread-operator-a867a71668ca)
- [6 Great uses of the spread operator](https://davidwalsh.name/spread-operator)

### Object 屬性簡寫

When assigning a variable to an object property, if the variable name is equal to the property name, you can do the following:

```js
const x = 10;
const myObj = { x };
console.log(myObj.x) // 10
```

#### 說明

Usually (pre-ES2015) when you declare a new *object literal* and want to use variables as object properties values, you would write this kind of code:

```js
const x = 10;
const y = 20;

const myObj = {
  x: x, // assigning x variable value to myObj.x
  y: y // assigning y variable value to myObj.y
};

console.log(myObj.x) // 10
console.log(myObj.y) // 20
```

As you can see, this is quite repetitive because the properties name of myObj are the same as the variable names you want to assign to those properties.

With ES2015, when the variable name is the same as the property name, you can do this shorthand:

```js
const x = 10;
const y = 20;

const myObj = {
  x,
  y
};

console.log(myObj.x) // 10
console.log(myObj.y) // 20
```

#### 外部資源

- [Property shorthand - ES6 Features](http://es6-features.org/#PropertyShorthand)

### Promises

A promise is an object which can be returned synchronously from an asynchronous function ([ref](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261#3cd0)).

Promises can be used to avoid [callback hell](http://callbackhell.com/), and they are more and more frequently encountered in modern JavaScript projects.

#### 範例程式碼

```js
const fetchingPosts = new Promise((res, rej) => {
  $.get("/posts")
    .done(posts => res(posts))
    .fail(err => rej(err));
});

fetchingPosts
  .then(posts => console.log(posts))
  .catch(err => console.log(err));
```

#### 說明

When you do an *Ajax request* the response is not synchronous because you want a resource that takes some time to come. It even may never come if the resource you have requested is unavailable for some reason (404).

To handle that kind of situations, ES2015 has given us *promises*. Promises can have three different states:

- Pending
- Fulfilled
- Rejected

Let's say we want to use promises to handle an Ajax request to fetch the resource X.

##### 創造 promise

We firstly are going to create a promise. We will use the jQuery get method to do our Ajax request to X.

```js
const xFetcherPromise = new Promise( // Create promise using "new" keyword and store it into a variable
  function(resolve, reject) { // Promise constructor takes a function parameter which has resolve and reject parameters itself
    $.get("X") // Launch the Ajax request
      .done(function(X) { // Once the request is done...
        resolve(X); // ... resolve the promise with the X value as parameter
      })
      .fail(function(error) { // If the request has failed...
        reject(error); // ... reject the promise with the error as parameter
      });
  }
)
```

As seen in the above sample, the Promise object takes a function which takes two parameters **resolve** and **reject**. Those parameters are functions which when called are going to move the promise *pending* state to respectively a *fulfilled* and *rejected* state.

But at the moment, the promise has not been used but only has been declared and stored into *xFetcherPromise* variable! So it doesn't have a current state.

##### 使用 promise

To use the promise, we do the following:

```js
xFetcherPromise
  .then(function(X) {
    console.log(X);
  })
  .catch(function(err) {
    console.log(err)
  })
```

```.then``` is a method that once called will put the xFetcherPromise in **pending** state. When called, the promise body runs, and in this case, an Ajax call is being done.

If it succeeds, *resolve* is called and the function passed as ```.then``` parameter is executed.

If it fails, *reject* is called and the function passed as ```.catch``` parameter is executed.

#### 外部資源

- [JavaScript Promises for dummies - Jecelyn Yeen](https://scotch.io/tutorials/javascript-promises-for-dummies)
- [JavaScript Promise API - David Walsh](https://davidwalsh.name/promises)
- [Using promises - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [What is a promise - Eric Elliott](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)
- [JavaScript Promises: an Introduction - Jake Archibald](https://developers.google.com/web/fundamentals/getting-started/primers/promises)
- [Promise documentation - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

### 模板字符串

Template literals is an [*expression interpolation*](https://en.wikipedia.org/wiki/String_interpolation) for single and multiple-line strings.

In other words, it is a new string syntax in which you can conveniently use any JavaScript expressions (variables for instance).

#### 範例程式碼

```js
const name = "Nick";
`Hello ${name}, the following expression is equal to four : ${2+2}`;

// Hello Nick, the following expression is equal to four: 4
```

#### 外部資源

- [String interpolation - ES6 Features](http://es6-features.org/#StringInterpolation)
- [ES6 Template Strings - Addy Osmani](https://developers.google.com/web/updates/2015/01/ES6-Template-Strings)

### Imports / Exports

ES6 modules are used to access variables or functions in a module explicitly exported by the modules it imports.

I highly recommend to take a look at MDN resources on import/export (see external resources below), it is both straightforward and complete.

#### 說明與範例程式碼

- Named exports

Named exports are used to export several values from a module. You can only name-export variables (not functions or class), so if you want to name-export a function, you have to store it in a variable before.

```js
// mathConstants.js
export const pi = 3.14;
export const exp = 2.7;
export const alpha = 0.35;

// -------------

// myFile.js
import { pi, exp } from './mathConstants.js'; // Destructuring import
console.log(pi) // 3.14
console.log(exp) // 2.7

// -------------

// mySecondFile.js
import * as constants from './mathConstants.js'; // Inject all exported values into constants variable
console.log(constants.pi) // 3.14
console.log(constants.exp) // 2.7
```

- Default import / export

Concerning the default export, there is only a single default export per module. A default export can be a function, a class, an object or anything else. This value is considered the "main" exported value since it will be the simplest to import. [Ref: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export#Description)

```js
// coolNumber.js
const ultimateNumber = 42;
export default ultimateNumber;

// ------------

// myFile.js
import number from './coolNumber.js';
// Default export, independently from its name, is automatically injected into number variable;
console.log(number) // 42
```

Function exporting:

```js
// sum.js
export default function sum(x, y) {
  return x + y;
}
// -------------

// myFile.js
import sum from './sum.js';
const result = sum(1, 2);
console.log(result) // 3
```

#### 外部資源

- [Export - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [Import - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
- [Understanding ES6 Modules](https://www.sitepoint.com/understanding-es6-modules/)
- [Modules in JavaScript](http://exploringjs.com/es6/ch_modules.html#sec_modules-in-javascript)

### <a name="this_def"></a> JavaScript *this*

*this* operator behaves differently than in other languages and is in most cases determined by how a function is called. ([Ref: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)).

This notion is having many subtleties and being quite hard, I highly suggest you to deep dive in the external resources below. Thus, I will provide what I personally have in mind to determine what *this* is equal to. I have learned this tip from [this article written by Yehuda Katz](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/).

```js
function myFunc() {
  ...
}

// After each statement, you find the value of *this* in myFunc

myFunc.call("myString", "hello") // "myString" -- first .call parameter value is injected into *this*

// In non-strict-mode
myFunc("hello") // window -- myFunc() is syntax sugar for myFunc.call(window, "hello")

// In strict-mode
myFunc("hello") // undefined -- myFunc() is syntax sugar for myFunc.call(undefined, "hello")
```

```js
var person = {
  myFunc: function() { ... }
}

person.myFunc.call(person, "test") // person Object -- first call parameter is injected into *this*
person.myFunc("test") // person Object -- person.myFunc() is syntax sugar for person.myFunc.call(person, "test")

var myBoundFunc = person.myFunc.bind("hello") // Creates a new function in which we inject "hello" in *this* value
person.myFunc("test") // person Object -- The bind method has no effect on the original method
myBoundFunc("test") // "hello" -- myBoundFunc is person.myFunc with "hello" bound to *this*
```

#### 外部資源

- [Understanding JavaScript Function Invocation and "this" - Yehuda Katz](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)
- [JavaScript this - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

### Class

JavaScript is a [prototype-based](https://en.wikipedia.org/wiki/Prototype-based_programming) language (whereas Java is [class-based](https://en.wikipedia.org/wiki/Class-based_programming) language, for instance). ES6 has introduced JavaScript classes which are meant to be a syntactic sugar for prototype-based inheritance and **not** a new class-based inheritance model ([ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)).

The word *class* is indeed error prone if you are familiar with classes in other languages. If you do, avoid assuming how JavaScript classes work on this basis and consider it an entirely different notion.

Since this document is not an attempt to teach you the language from the ground up, I will believe you know what prototypes are and how they behave. But here are some links I found great to understand this notion:

- [Understanding Prototypes in JS - Yehuda Katz](http://yehudakatz.com/2011/08/12/understanding-prototypes-in-javascript/)
- [A plain English guide to JS prototypes - Sebastian Porto](http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/)
- [Inheritance and the prototype chain - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

#### 範例

Before ES6, prototype syntax:

```js
var Person = function(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.stringSentence = function() {
  return "Hello, my name is " + this.name + " and I'm " + this.age;
}
```

With ES6 class syntax:

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  stringSentence() {
    return "Hello, my name is " + this.name + " and I'm " + this.age;
  }
}

const myPerson = new Person("Manu", 23);
console.log(myPerson.age) // 23
console.log(myPerson.stringSentence()) // "Hello, my name is Manu and I'm 23
```

#### 外部資源

For prototype understanding:

- [Understanding Prototypes in JS - Yehuda Katz](http://yehudakatz.com/2011/08/12/understanding-prototypes-in-javascript/)
- [A plain English guide to JS prototypes - Sebastian Porto](http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/)
- [Inheritance and the prototype chain - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

For classes understanding:

- [ES6 Classes in Depth - Nicolas Bevacqua](https://ponyfoo.com/articles/es6-classes-in-depth)
- [ES6 Features - Classes](http://es6-features.org/#ClassDefinition)
- [JavaScript Classes - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

### Async Await

除了 [Promises](#promises) 以外，還有一種新語法你可能會遇到，那就是被稱作非同步的 *async / await*。

The purpose of async/await functions is to simplify the behavior of using promises synchronously and to perform some behavior on a group of Promises. Just as Promises are similar to structured callbacks, async/await is similar to combining generators and promises. ([Ref: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function))

> **Note :** You must understand what are promises and how they work before trying to understand async / await since they rely on it.

> **Note 2:** [*await* must be used in an *async* function](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9#f3f0), which means that you can't use await in the top level of our code since that is not inside an async function.

#### 說明與範例程式碼

*Async / Await* is built on promises but they allow a more imperative style of code.

An `await` expression causes `async` function to pause the execution, wait for promise to resolve, and then resume the execution once the value is resolved. Any `async` function returns the `Promise`, and will be resolved to returned value.

```js
async function getGithubUser(handle) { // async keyword allows usage of await in the function and means function returns a promise 
  try { // this is how errors are handled with async / await
    const url = `https://api.github.com/users/${handle}`;
    const response = await fetch(url); // "synchronously" waiting fetch promise to resolve before going to next line
    return response.json();
  } catch (err) {
    alert(err);
  }
}

getGithubUser('mbeaudru').then(user => console.log(user)); // logging user response - cannot use await syntax since this code isn't in async function
```

#### 外部資源

- [Async/Await - JavaScript.Info](https://javascript.info/async-await)
- [ES7 Async/Await](http://rossboucher.com/await/#/)
- [6 Reasons Why JavaScript’s Async/Await Blows Promises Away](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9)
- [JavaScript awaits](https://dev.to/kayis/javascript-awaits)
- [Using Async Await in Express with Node 8](https://medium.com/@Abazhenov/using-async-await-in-express-with-node-8-b8af872c0016)
- [Async Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [Await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

## 術語詞彙

### <a name="scope_def"></a> 作用域範圍 (scope)

The context in which values and expressions are "visible," or can be referenced. If a variable or other expression is not "in the current scope," then it is unavailable for use.

資料來源： [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope)

### <a name="mutation_def"></a> Variable mutation

一個變數在被宣告之後發生初始值變化的過程。

```js
var myArray = [];
myArray.push("firstEl") // myArray 正在變化
```

如果變數不能被改變的話，我們會說這個變數是 *不可變的 (immutable)* 。

[查看 MDN Mutable 文章](https://developer.mozilla.org/en-US/docs/Glossary/Mutable) 了解更多詳細資料。
