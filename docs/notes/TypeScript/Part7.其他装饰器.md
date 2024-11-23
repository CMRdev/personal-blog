# 其他装饰器

## 1、属性装饰器

```ts
/**
 * target:对于静态属性来说值是类，对于实例属性来说值是类的原型对象
 * propertyKey:属性名
 */
function Demo(target: object, propertyKey: string) {
  console.log(target, propertyKey)
}

class Person {
  @Demo name: string
  @Demo age: number
  @Demo static school: string
  constructor(name, age) {
    this.name = name
    this.age = age
  }
}

// const p1 = new Person('zhangsan', 18) // 不会属性遮蔽，实例属性age为18和原型属性age为130
let value = 130
Object.defineProperty(Person.prototype, 'age', {
  // 给原型添加属性
  get() {
    return value
  },
  set(val) {
    value = val
  }
})
const p1 = new Person('zhangsan', 18) // 会属性遮蔽，实例属性age和原型属性age都会变为18
```

## 2、方法装饰器

```ts
/**
 * target:对于静态方法来说值是类，对于实例方法来说值是类的原型对象
 * propertyKey:方法名
 * descriptor:方法的描述对象，其中value属性是被装饰的方法
 */
function Demo(target: object, propertyKey: string, descriptor: any) {
  console.log(target, propertyKey, descriptor)
  const original = descriptor.value // 保存原始方法
  // 替换原始方法
  descriptor.value = function (...args) {
    console.log('方法执行前的操作')
    const result = original.call(this, ...args) // call和apply都可修改函数的this，call的参数要一个一个传，apply的参数要一起传递
    console.log('方法执行后的操作')
    return result
  }
}

class Person {
  name: string
  age: number
  static school: string
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  @Demo speak() {
    console.log('speak')
  }
}
```

## 3、访问器装饰器

```ts
class Person {
  private _name: string

  @Demo
  get name() {
    return this._name
  }
  set name(val) {
    this._name = val
  }
}
```
