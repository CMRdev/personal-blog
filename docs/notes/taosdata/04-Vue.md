## vue3

- reactive

```bash
# 对一个已存在的代理对象调用 reactive() 会返回其本身
console.log(reactive(proxy) === proxy) // true
# 响应式对象内的嵌套对象依然是代理
const proxy = reactive({})
const raw = {}
proxy.nested = raw
console.log(proxy.nested === raw) // false
```

- 写代码时先考虑使用`reactive`能否实现，否则使用`ref`
- 解构`ref`、`reactive`将失去响应式
- props 可以解构：`const { foo } = defineProps(['foo'])`
- 写代码时先考虑是否需要计算缓存，需要则使用`computed`，不需要则使用`方法`
- watch 不能侦听响应式对象的属性值，可侦听`响应式对象、getter函数、多个来源组成的数组`
- `watchEffect()` 允许我们自动跟踪回调的响应式依赖，且仅会在其`同步`执行期间，才追踪依赖，所以无法追踪到 await 后的响应式变量
- `model、computed、props`都是`ref`

- `组件事件` - 假如你想改变 props 的值并同步给父组件

```bash
<script setup>
const emit = defineEmits(['inFocus', 'submit'])
function buttonClick() {
  emit('submit')
}
</script>
```
