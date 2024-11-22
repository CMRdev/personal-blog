# 泛型

## 1、泛型

- <泛型>：
  `参数化类型 ArrayList<String> list2 = new ArrayList<>()`
- <泛型类>
  `public class ClassName<T>{}`
- <泛型接口>
  `public interface IntercaceName<T>{}`
- <泛型方法>
  `private static <T> T 方法名(T a, T b) {}`

- 【作用】：提高代码复用率、泛型中的类型在使用时指定，不需要强制类型转换（类型安全，编译器会检查类型）【泛型只在编译阶段有效，运行时会将泛型的相关信息擦除】

## 2、试例

```js
/**
 * 泛型，T是自定义的类型名字可以自己取
 */
function logData<T>(data: T) {
  console.log(data)
}
logData<number>(100)
logData<string>('sdfasd')
/**
 * 泛型接口
 */
interface IPersonTom<T> {
  name: string
  info: T
}
let p: IPersonTom<number> = {
  name: 'tom',
  info: 13465
}
/**
 * 泛型类
 */
class PersonTom<T> {}
```
