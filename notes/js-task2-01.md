[2-1. 表单（一）单个表单项的检验](http://ife.baidu.com/course/detail/id/97)

[代码](https://github.com/icyfish/IFE2017/blob/master/js-task2-01.html)

[Demo](https://icyfish.github.io/IFE2017/js-task2-01.html)


**学习笔记:**


## 将字符串转换为数组进行验证

[精选笔记-如何判断中文字符，特别是占32位的中文字符](http://ife.baidu.com/note/detail/id/583)中通过分析字符串的方式判断占32位的中文字符, 个人认为还可以有另一种解决方法, 使用split方法将字符串转换成数组形式后, 会将32位中文字符分成数组中的两个元素返回, 此时再对数组内的元素Unicode码进行判断即可.


## Array.prototype.reduce()


**示例:**

```js
const numbers = [10,20,30];
let sum = 0;

// 不使用 reduce
// 计算numbers数组中所有值的和

for(var i = 0; i < numbers.length; i++){
  sum += numbers[i];
}

console.log(sum); //60

//使用 reduce

const reduceSum = numbers.reduce((sum, number)=>{
  return sum + number;
}, 0);

console.log(reduceSum); //60
```

![reduce](/images/array-reduce.jpg)

传入reduce的第二个参数是初始值(initial value), 第一个参数是Iterator Function, Iterator Function接受两个参数, 第一次执行接受初始值和原数组中的第一个元素作为参数, 执行结束后返回的值作为Iterator Function的第一个参数, 原数组中的第二个元素作为第二个参数, 以此类推.

reduce功能强大, 可以使用reduce实现以上所有数组方法的功能.

**reduce实现map的功能:**

```js
let primaryColors = [
  {color: 'red'},
  {color: 'yellow'},
  {color: 'blue'},
];
const reducedColor = primaryColors.reduce((accumulator, primaryColor)=>{
  accumulator.push(primaryColor.color);
  return previous;
}, []);

console.log(reducedColor); // ["red", "yellow", "blue"]

// 若使用map, 则是:

const mappedColor = primaryColors.map(primaryColor => primaryColor.color);
console.log(mappedColor); // ["red", "yellow", "blue"]
```

**计算order总量**:

```js
const orders = [
	{ amount: 250 },
	{ amount: 200 },
	{ amount: 340 },
	{ amount: 100 }
]

let totalAmount = orders.reduce((sum, order) => {
	return sum + order.amount
}, 0);

console.log(totalAmount);
```

**计算各个交通工具的个数**

```js
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck'];

const transportation = data.reduce((obj, item) => {
  if (!obj[item]) {
    obj[item] = 0;
  }
  obj[item]++;
  return obj;
}, {});

console.log(transportation);
//{car: 5, truck: 3, bike: 2, walk: 2, van: 2}
```

**检查括号是否对称**

(必须是一对括号且左括号在前) [balanced parentheses]:

```js
function balancedParens(string){
  return !string.split('').reduce(function (counter, char){
    if (counter < 0) {return counter;}
    if (char === "(") {return ++counter;}
    if (char === ")") {return --counter;}
    return counter;
  },0);
}

balancedParens("((())))"); // false
balancedParens("))((()"); // false
balancedParens("(((())))"); // true
balancedParens("()()()()"); // true
balancedParens('()()()skoaksod'); //true
```

1. `string.split('')`: 因为reduce只能在数组中使用, 所以先将参数的类型从string转化为array;
2. 将初始值设为0, 若数组中出现`(`, 计数器(counter)+1, 出现`)`计数器减1, 只有当计数器最后结果为0时返回true;
3. `!`会将结果强制转换(coercion)为布尔值;
4. `if (counter < 0) {return counter;}`: 如果计数器值为负, 直接返回, 最后结果就为false, 因为左括号必须在右括号之前.
