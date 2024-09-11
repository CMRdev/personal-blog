# 基础知识

## 1、代码改写

- 如果代码中出现了`三层及以上`的 if 嵌套，请考虑改写你的代码

---

## 2、[ES6 新特性(Array)](https://exploringjs.com/es6/ch_arrays.html)

[官网](https://262.ecma-international.org/6.0/)

### 解构赋值

```js
// 数组
const [a, b, c] = [1, 2, 3]
// 对象
const obj = { a: 1, b: 2 }
const { a, b } = obj
```

### 扩展运算符

```js
// 数组
let arr3 = [...arr1, ...arr2]
// 对象
const obj1 = { a: 1, b: 2 }
const obj2 = { b: 3, c: 4 }
const merged = { ...obj1, ...obj2 }
console.log(merged) // { a: 1, b: 3, c: 4 } (注意这里b的值被obj2中的值覆盖了)
```

### 模板字符串

```js
;`string text ${expression} string text`
```

### 箭头函数

```js
const materials = ['Hydrogen', 'Helium', 'Lithium', 'Beryllium']
console.log(materials.map((material) => material.length))
// Expected output: Array [8, 6, 7, 9]
```

### 块级作用域

```js
{
  // 作用域只在 `{}` 中
  let ...
  const ...
}
```

### 静态方法（from、of）

- `Array.from()` 用于从类似数组或可迭代的对象创建一个浅拷贝的数组实例

```js
console.log(Array.from('foo'))
// Expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], (x) => x + x))
// Expected output: Array [2, 4, 6]

let numbers = { 0: 1, 1: 4, 2: 9, length: 3 }
let roots = Array.from(numbers, Math.sqrt)
console.log(roots)
// Expected output: Array [1, 2, 3]
```

- `Array.of()` 创建一个新的 Array 实例，而不考虑参数的数量或类型

```js
console.log(Array.of('foo', 2, 'bar', true))
// Expected output: Array ["foo", 2, "bar", true]

console.log(Array.of())
// Expected output: Array []
```

### 实例方法（entries、keys 、values、find、findIndex、copyWithin、fill）

- `entries()` 返回一个新的数组迭代器对象，该对象包含数组中每个索引的键/值对

```js
const array1 = ['a', 'b', 'c']
const iterator1 = array1.entries()

console.log(iterator1.next().value)
// Expected output: Array [0, "a"]
console.log(iterator1.next().value)
// Expected output: Array [1, "b"]
```

- `keys()`返回一个新的数组迭代器对象，其中包含数组中每个索引的键

```js
const array1 = ['a', 'b', 'c']
const iterator = array1.keys()

for (const key of iterator) {
  console.log(key)
}
// Expected output: 0
// Expected output: 1
// Expected output: 2
```

- `values()` 返回一个新的数组迭代器对象，该对象迭代数组中每个元素的值

```js
const array1 = ['a', 'b', 'c']
const iterator = array1.values()

for (const value of iterator) {
  console.log(value)
}
// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```

- `find()` 返回数组中满足提供的测试函数的第一个元素的值，否则返回 `undefined`

```js
const array1 = [5, 12, 8, 130, 44]
const found = array1.find((element) => element > 10)

console.log(found)
// Expected output: 12
```

- `findIndex()` 返回数组中满足提供的测试函数的第一个元素的索引。否则返回 -1

```js
// 如果只是检查数组中每个元素是否与某个值相等，请使用 `indexOf()` 方法
const array1 = [5, 12, 8, 130, 44]
const isLargeNumber = (element) => element > 13

console.log(array1.findIndex(isLargeNumber))
// Expected output: 3
```

- `copyWithin()` 浅复制数组的一部分到另一个位置，并返回它，不会改变原数组的长度。

```js
// 是一种移动数组数据的高性能方法,虽然不常用
const array1 = ['a', 'b', 'c', 'd', 'e']
// Copy to index 0 the element at index 3
console.log(array1.copyWithin(0, 3, 4))
// Expected output: Array ["d", "b", "c", "d", "e"]
```

- `fill()` 用一个固定值填充一个数组，返回修改后的数组

```js
const array1 = [1, 2, 3, 4]
// Fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4))
// Expected output: Array [1, 2, 0, 0]
console.log(array1.fill(6))
// Expected output: Array [6, 6, 6, 6]
```

## 3、其他(Array) map、reduce、forEach、filter、some、includes、every、flat、flatMap

- `map()` 创建一个新数组，有返回值，原始数组不变

```js
const array1 = [1, 4, 9, 16]
const map1 = array1.map((x) => x * 2)
console.log(map1)
// Expected output: Array [2, 8, 18, 32]
```

- `reduce()` 提供一个 reducer 函数，每一次运行 reducer 会将先前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值

```js
const array1 = [1, 2, 3, 4]
// 0 + 1 + 2 + 3 + 4
const initialValue = 0
const sumWithInitial = arrayl.reduce((accumulator, currentValue) => accumulator + currentValue, initialValue)
console.log(sumWithInitial)
// Expected output:10
```

- `forEach()` 对数组的每个元素执行一次给定的函数，无返回值

```js
const array1 = ['a', 'b', 'c']
array1.forEach((element) => console.log(element))
```

- `filter()` 创建给定数组一部分的浅拷贝，其包含通过所提供函数实现的测试的所有元素

```js
const words = ['spray', 'elite', 'exuberant', 'destruction', 'present']
const result = words.filter((word) => word.length > 6)
console.log(result)
// Expected output: Array ["exuberant", "destruction", "present"]
```

- `includes()` 判断一个数组是否包含一个指定的值

```js
const pets = ['cat', 'dog', 'bat']
console.log(pets.includes('cat'))
// Expected output: true
```

- `some()` 测试数组中是否至少有一个元素通过了由提供的函数实现的测试

```js
// 如果只是检查数组中是否有与某个值相等的元素，请使用 `includes()` 方法
const array = [1, 2, 3, 4, 5]
const even = (element) => element % 2 === 0

console.log(array.some(even))
// Expected output: true
```

- `every()` 测试一个数组内的所有元素是否都能通过指定函数的测试

```js
const isBelowThreshold = (currentValue) => currentValue < 40
const array1 = [1, 30, 39, 29, 10, 13]
console.log(array1.every(isBelowThreshold))
// Expected output: true
```

- `flat()` 创建一个新的数组，并根据`指定深度`递归地将所有子数组元素拼接到新的数组中

```js
const arr1 = [0, 1, 2, [3, 4]]
console.log(arr1.flat())
// expected output: Array [0, 1, 2, 3, 4]

const arr2 = [0, 1, [2, [3, [4, 5]]]]
console.log(arr2.flat())
// expected output: Array [0, 1, 2, Array [3, Array [4, 5]]]
console.log(arr2.flat(2))
// expected output: Array [0, 1, 2, 3, Array [4, 5]]
console.log(arr2.flat(Infinity))
// expected output: Array [0, 1, 2, 3, 4, 5]
```

- `flatMap()` 对数组中的每个元素应用给定的回调函数，然后将结果展开一级，返回一个新数组

```js
// 等价于在调用 map() 方法后再调用深度为 1 的 flat() 方法（arr.map(...args).flat()）
const arr1 = [1, 2, 1]
const result = arr1.flatMap((num) => (num === 2 ? [2, 2] : 1))
console.log(result)
// Expected output: Array [1, 2, 2, 1]
```

## 4、js 判断数据类型的方法汇总

### 【返回表示数据类型的字符串】

```js
typeof entity.path.show === 'object'
```

### 【A instanceof B 可以判断 A 是不是 B 的实例】

```js
xxx instanceof Function // instanceof 后面一定要是对象类型，大小写不能写错
```

### 【用 Object 的 toString.call 来判断，返回一个字符串】

```js
toString.call(123) // [object Number]
```

### 【根据 contructor 判断】

```js
;[1, 2, 3].constructor === Array
```

## 5、==、===

- `null == undefined` // true
- `null === undefined` // false (判断值和类型是否都一样)

## 6、知识

- eval()：将字符串转为脚本执行
- NaN：`not a number`
