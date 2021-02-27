---
id: hans
title: hansDoc
slug: hansDoc.html
---
# 零.javascript(es6)

## 0.看到了就记下来

### 基本数据类型（7种）

undefined，null，string，Number，Object，Boolean，Symbol（es6加入）

### globalThis

在js脚本中使用globalThis表示全局对象，在浏览器环境globalThis即为window，在node.js环境即为global，在不知道脚本的运行环境时可以用globalThis来表示全局对象

### Array.prototype.map()方法

- 作用：对于数组中的每一个元素执行map中定义的函数后返回一个新的数组

- 语法：

  ```javascript
  //主要用currentValue，即当前处理的元素
  var new_array = arr.map(function callback(currentValue[, index[, array]]) {
   // Return element for new_array 
  }
  ```

  eg：

  ```javascript
  //求数组中每个元素的平方根
  var list = [12,13,14];
  var res = list.map(Math.sqrt)
  
  //重新格式化数组中的对象
  var kvArray = [{key: 1, value: 10}, 
                 {key: 2, value: 20}, 
                 {key: 3, value: 30}];
  
  var reformattedArray = kvArray.map(function(obj) { 
     var rObj = {};
     rObj[obj.key] = obj.value;
     return rObj;
  });
  // reformattedArray 数组为： [{1: 10}, {2: 20}, {3: 30}], 
  // kvArray 数组未被修改
  ```

- **注意**：通常情况下`map` 方法中的 `callback` 函数只需要接受一个参数，就是正在被遍历的数组元素本身。但这并不意味着 `map` 只给 `callback` 传了一个参数。

  eg：["1", "2", "3"].map(parseInt);期望得到[1,2,3]，但是实际输出[1,NaN,NaN]，这是因为这里实际传递了2个参数，一个element：数组中的元素，一个index：数组的索引（其实还有第三个参数array即当前数组，但是被parseInt函数忽略了），parseInt（string, radix），实际的执行过程如下：

  ```javascript
  // parseInt(string, radix) -> map(parseInt(value, index))
  /*  first iteration (index is 0): */ parseInt("1", 0); // 1
  /* second iteration (index is 1): */ parseInt("2", 1); // NaN
  /*  third iteration (index is 2): */ parseInt("3", 2); // NaN
  ```

  正确的解决方案如下：

  ```javascript
  function myParseInt(element) {
      return parseInt(element, 10);
  }
  var res = list.map(myParseInt);
  //或者写成箭头函数
  var res = list.map(ele => myParseInt(ele))
  ```

  数组的forEach()和map类似，只是forEach没有返回值，更适用于只是对数据进行操作

### Array.prototype.filter()方法

- 作用：用于过滤数组中不满足指定条件的数据，返回过滤后的数组，不会改变原数组

- 语法：

  ```javascript
  //可以传入3个参数。主要用element即当前元素
  const newArray = arr.filter(callback(element[, index[, array]])[, thisArg])
  ```

  eg:

  ```javascript
  const list = [1,2,3,4,5,6];
  //过滤掉偶数，返回全是奇数
  const res = list.filter(item => item & 1)	//[1,3,5]
  ```
