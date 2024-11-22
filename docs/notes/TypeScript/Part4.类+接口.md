# 类、接口

## l、类

- 修饰符

```js
/**
 * public：内部、子类、外部都可以访问
 * protected：内部、子类可以访问
 * private：内部可以访问
 */
class Person {
  constructor(
    public name: string,
    public age: number,
    private readonly email: string
  ) { }
  speak(): void { // 默认public
    console.log('我是人')
  }
  protected getDetails() {
    return 'neibuxinxi'
  }
}
class Student extends Person {
  grade: number
  constructor(name: string, age: number, email: string, grade: number) {
    super(name, age, email)
    this.grade = grade
  }
  study() {
    this.name
  }
  override speak(): void {
    console.log('我是学生')
  }
}

const p1 = new Student('zhangsan', 10, '1566165', 2)
p1.speak()
p1.study()

```

- 抽象类

```js

/**
 * 抽象类：定义通用接口、提供基础实现、确保关键实现、共享代码和逻辑
 */
abstract class Package {
  constructor(public weight: number) { }
  // 抽象方法
  abstract calc(): string
  printPackage(): void {
    console.log('sfad' + this.calc())
  }
}

class pk extends Package {
  constructor(weight: number, public unit: string) {
    super(weight)
  }
  // 必须实现抽象方法
  calc(): string {
    return this.weight + this.unit
  }
}
```

## 2、接口

```js
/**
 * 接口interface：只能定义格式，不能包含任何实现
 * 可以限制类、对象、函数
 * 接口可继承：interface a extends IPerson {}
 */

/**
 * interface与抽象类的区别
 * interface：不能有任何实现，一个类能实现多个接口
 * abstract类：可包含抽象方法、具体方法，一个类只能继承一个抽象类
 */
interface IPerson {
  name: string
  age: number
  speak(n: number): void
}
class PersonOne implements IPerson {
  constructor(public name: string, public age: number){}
  speak(n: number): void {
    console.log(n + "")
  }
}
// 接口限制对象
interface IUser {
  name: string
  gender: string
  age?: number
  run: (n:number) => void
}
const userOne: IUser = {
  name: "123",
  gender: "456",
  run(n) {
    console.log(n + "")
  }
}
```
