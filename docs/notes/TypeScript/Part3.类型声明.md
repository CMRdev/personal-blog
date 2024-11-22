# 类型声明

## 1、对象

- 索引签名`[key: string]: any`

```ts
let person: { name: string; age?: number; [key: string]: any }
person = { name: 'John', age: 10, gender: 'male' }
```

## 2、函数

```ts
let count: (a: number, b: number) => number // 声明函数类型的形式
count = function (x, y) {
  return x + y
}
```

## 3、tuple 元组

```ts
let arr: [number, number, ...string[]] // 可以这样写
```

## 4、enum 枚举

```ts
// 常量枚举 `const enum Direction{}`，可优化代码，没用到的枚举值会被删除
enum Direction {
  Up, // 等价于 Up = 0，数字枚举是有反向映射的；若写成 Up = 'up' 字符串枚举，则没有反向映射
  Down,
  Left,
  Right
}
function walk(str: Direction) {
  if (str.Up) ...
}
```

## 5、type 定义类型

```ts
type Gender = '男' | '女'
type Status = number | string // 联合类型
type Area = {
  height: number
  width: number
}
type Address = {
  num: number
  cell: number
}
type House = Area & Address // 交叉类型
const house: House = {
  height: 100,
  width: 100,
  num: 201,
  cell: 4
}
```

```ts
type LogFunc = () => void
const f1: LogFunc = function () {
  return 666 // 此处有返回值也不会报错，是为了适配这样的箭头函数 let n = 0; [1,2,3].forEach(x => n += x);
}
```
