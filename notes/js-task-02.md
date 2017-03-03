[零基础JavaScript编码（二）](http://ife.baidu.com/course/detail/id/91)

**学习笔记:**

# 数组方法forEach, map, filter, sort

## forEach

**示例:**

```js
const colors = ['red', 'green', 'blue'];

// 不使用forEach
// 遍历数组

for(var i = 0; i < colors.length; i++){
  console.log(colors[i]);
}

// 使用forEach

colors.forEach(color => {
  console.log(color);
});
```
![forEach](/images/array-forEach.jpg)

原数组的元素被遍历传入Iterator Function并执行.

**更实际的应用:**

![forEach1](/images/array-forEach1.jpg)

```js
const numbers = [1, 2, 3, 4];
let sum = 0;

numbers.forEach(number => {
  sum += number;
});

console.log(sum);
```

## map

**示例:**

```js
const numbers = [1, 2, 3, 4];
// 将原数组中各个元素X2输出

// 不使用map实现

let doubledNumbers = []; // 创建一个新数组来存储数据, 为了不改变原数组 (avoid mutating)
for(var i = 0; i < numbers.length; i++){
  doubledNumbers.push(numbers[i] * 2)
}
console.log(doubledNumbers); // [2, 4, 6, 8]

// 使用map实现

let doubledMap = numbers.map(number => number * 2)
console.log(doubledMap); // [2, 4, 6, 8]
```
![map](/images/array-map.jpg)

原数组的元素被遍历传入Iterator Function并执行, 执行后的结果被返回并存入新数组.

map可以用于汇总数组内各个元素的属性值, 并输出相关信息. 例子:

```js
const cars = [
  {model: 'Buick', price: 'cheap'},
  {model: 'Camaro', price: 'expensive'}
];

const model = cars.map(car => {
  return car.model;
});
console.log(model); // ['Buick', 'Camaro']

const price = cars.map(car => {
  return car.price;
});
console.log(price); // ['cheap', 'expensive']
```

渲染数据列表:

可在浏览器控制台输入以下代码片段查看效果

```js
const cars = [
  {model: 'Buick', price: 'cheap'},
  {model: 'Camaro', price: 'expensive'}
];  
const carsList = document.createElement('ul');

 const aboutCars = cars.map(car => {
   return `<li>${car.model} is ${car.price}</li>`;
 });

aboutCars.forEach(car => {
  carsList.innerHTML += car;
})
document.body.innerHTML = '';
document.body.appendChild(carsList);
```

**更实际的应用:**

![map-practical](/images/array-map-practical.jpg)


## filter

**示例:**

```js
const products = [
  { name: 'cucumber', type: 'vegetable', quantity: 10, price: 1 },
  { name: 'banana', type: 'fruit', quantity: 8, price: 15 },
  { name: 'cucumber', type: 'vegetable', quantity: 25, price: 12 },
  { name: 'orange', type: 'fruit', quantity: 30, price: 8 },
]

// 不使用filter实现
// 筛选出类型为水果的产品

let filteredProducts = [];
for(var i = 0; i < products.length; i++){
  if(products[i].type === 'fruit'){
    filteredProducts.push(products[i])
  }
}
console.table(filteredProducts);

// 使用filter实现
// 筛选出类型为水果的产品

const fruit = products.filter(product => product.type === 'fruit');
console.table(fruit);

// 筛选出类型为蔬菜, 且数量大于0, 且价格小于10的产品

const veg = products.filter(product => product.type === 'vegetable' && product.quantity > 0 && product.price < 10);
console.table(veg);
```

`console.table`将数组以表格的形式显示在控制台中, 可读性更强.

![filter](/images/array-filter.jpg)

原数组的元素被遍历传入Iterator Function, Iterator Function返回值的类型为布尔值, 如果返回true, 则该元素被存入结果数组.

**更实际的应用:**

筛选出指定post的comment内容:

![filter-practical](/images/array-filter-practical.jpg)

```js
const post = { id: 4, title: 'New Post'};

const comments = [
  { postId: 4, content: 'Awesome Post'},
  { postId: 3, content: 'It was ok'},
  { postId: 4, content: 'neat'}
];

function commentsForPost(post, comments){
  return comments.filter(comment => comment.postId === post.id);
}

const filteredComments = commentsForPost(post, comments);
console.table(filteredComments);

```

在Todo App中:

未完成的todo会一直显示, 完成的todo只有在showCompleted为true时才显示
```js
const filteredTodos = filteredTodos.filter((todo) => {
  return !todo.completed || showCompleted;
});
```

Ps: 逻辑操作符 `||`("或")

`expr1 || expr2`, 如果表达式结果为true, 则返回expr1, false则返回expr1, 因此当参数为布尔值时, 任意一个参数为true, `expr1 || expr2`返回的结果就为true.




## sort

```js
function compareFunction(a, b){
  // return -1, a出现在b之前
  // return 1,  a出现在b之后
  // return 0, 顺序不变
}
arr.sort(compareFunction);
```

**示例:**

```js
var numbers = [4, 20, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers); // [1, 3, 4, 5, 20]
```
如果没有comparisonFunction, 先将数列中的内容转化成字符串再根据Unicode顺序排序.

```js
var scores = [1, 10, 21, 2];
scores.sort();
console.log(scores); // [1, 10, 2, 21]
// 10在 2之前,
// 因为在Unicode码中'10'在'2'之前
```

```js
const inventors = [
  { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
  { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
  { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
  { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
  { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
  { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 }
];

// 生辰从早到晚

inventors.sort((a, b) => a.year - b.year ? 1 : -1);

console.table(inventors);

// 活得长的发明家排在后

inventors.sort((a, b) => {
  return (a.passed - a.year) - (b.passed - b.year);
});

console.table(inventors);
```

Todo App中, 未完成的Todo显示在已完成的之前:

```js
let sortedTodos;

sortedTodos.sort((a, b) => {
  if(!a.completed && b.completed){
   return -1;
  }else if (a.completed && !b.completed) {
   return 1;
  }else{
   return 0;
  }
})
```

Ps: 逻辑操作符 `&&`("与")

`expr1 && expr2`, 如果表达式结果为false, 则返回expr1, 否则返回expr2, 因此当参数为布尔值时, 若参数均为true, 则结果返回true, 否则返回false.
