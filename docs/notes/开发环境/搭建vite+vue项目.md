# 搭建vite + vue项目

## 1、搭建项目

```bash
# 使用 . 作为项目名称，在当前目录中创建项目脚手架
# npm 7+，需要添加额外的 --：
npm create vite@latest . -- --template vue-ts
```

## 2、安装依赖

```bash
# 安装element-plus
npm install element-plus --save
npm install @element-plus/icons-vue
# 自动导入
npm install -D unplugin-vue-components unplugin-auto-import
npm install -D sass
npm install vue-router
npm install pinia
```

```js
// vite.config.ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      imports: [
        'vue', //可以节省vue引用
        'vue-router', //节省router引用
        'pinia' //节省pinia引用
      ],
      resolvers: [ElementPlusResolver()]
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```