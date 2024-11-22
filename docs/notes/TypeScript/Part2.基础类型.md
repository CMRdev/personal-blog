# 基础知识

## 1、JS 的八种数据类型

- 基本数据类型：`number、string、boolean、null、undefined、symbol、bigint`
- 引用数据类型：`object`（包含 Function、Array、Date...）

## 2、TS 新增的数据类型

- 联合类型

  ```js
  let a: string | number = 'hello'
  ```

- 类型别名

  ```js
  type Person = { name: string, age: number }
  let person: Person = { name: 'John', age: 30 }
  ```

- interface

  ```js
  interface User { name: string email: string }
  let user: User = { name: 'Jane', email: 'jane@example.com' }
  ```

- tuple

  ```js
  let personTuple: [string, number] = ['John', 30]
  //（表示一个包含字符串和数字的元组）
  ```

- 字面量类型

  ```js
  let direction: 'up' | 'down' | 'left' | 'right' = 'up'
  //（变量direction只能是这四个字符串值之一）
  ```

- enum

  ```js
  enum Color {
    Red,
    Green,
    Blue
  }
  let color: Color = Color.Red
  ```

- void

  ```js
  function logMessage(): void {
    console.log('This is a log message.')
  }
  // （表示该方法没有返回值）
  ```

- any

  ```js
  let dynamicValue: any = 'This could be anything'
  dynamicValue = 123
  dynamicValue = { name: 'Dynamic' }
  ```

## 3、手册指南

- 定义数组写法

```js
let list: number[] = [1, 2, 3]
let list: Array<number> = [1, 2, 3] // 数组泛型
```

- never 类型

```js
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message)
}
```

- 类型断言

```ts
let someValue: any = 'this is a string'
// 尖括号语法
let strLength: number = (<string>someValue).length
// as语法
let strLength: number = (someValue as string).length
// 当你在TypeScript里使用JSX时，只有 as语法断言是被允许的
```
