# 装饰器

- 实验性特性，需要配置（ts5.0 可直接使用）
- 类装饰器：应用在`类声明上的函数`

## 1、配置

- `tsc --init` -> `tsconfig.json` -> `experimentDecorator: true`

## 2、类装饰器

```ts
// demo函数会在Person类定义时执行
function Demo(target: Function) {
  console.log(target)
}
function CustomString(target: Function) {
  target.prototype.toString = function () {
    return JSON.stringify(this) // this -> 类的实例对象；target -> 类
  }
  // Object.seal(target.prototype) // seal封锁，不允许随便在原型上添加属性
}

@Demo
class Person {
  constructor(public name: string, public age: number) {}
}
```

## 3、构造类型

```js
/**
 * new: 该类型可以用new操作符调用
 * ...args：构造器可以接受任意数量的参数
 * any[]：构造器可以接受任意类型的参数
 * {}：返回类型是对象，非null、非undefined
 */
type Constructor = new (...args:any[]) => {}

// type Constructor = {
//    new (...args:any[]): {};
//    wife: string // 静态属性
// }

function test(fn: Constructor) {}
class Person {}
test(Person)
```

## 4、替换被装饰的类

```ts
type Constructor = new (...args: any[]) => {}
// extends -> 类型约束
function LogTime<T extends Constructor>(target: T) {
  return class extends target {
    // 将被装饰的类继承过来
    createdTime: Date
    constructor(...args: any[]) {
      // ...args为了动态适配参数
      super(...args)
      this.createdTime = new Date()
    }
    getTime() {
      return this.createdTime.getTime()
    }
  }
}
```

## 5、装饰器工厂

```js
// 工厂 -> 返回装饰器
function LogInfo(n: number) {
  return function(target: Function) {
    target.prototype.introduce = function() {
      for(let i = 0; i < n; i++) {
        console.log(i + ': ' + 'balabala')
      }
    }
  }
}
@LogInfo(5)
class Person {
  constructor(public name, public age) {}
}

/**
 * 打印顺序：工厂从上到下，装饰器从下到上
 * 输出：test2工厂 - test3工厂 - test4 - test3 - test2 - test1
 */
@test1
@test2()
@test3()
@test4
class Person {}

```
