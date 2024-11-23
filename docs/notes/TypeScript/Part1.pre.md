# Prepare

- TS 是`微软`开发的基于 JS 的`扩展`语言
- TS 包含了 JS 的所有内容，是 JS 的`超集`
- TS 更适合`大型项目`，增加了`静态类型检查、接口、泛型`等很多现代开发特性
- TS 需要`编译`为 JS，然后交给浏览器或其他 JS 运行环境执行

## 1、安装

- `npm install -g typescript`
- `tsc greeter.ts` // 将 greeter.ts 转为 greeter.js

## 2、生成 `tsconfig.json` 文件

- `tsc --init`
- tsconfig.json 配置

  ```json
  {
    "compilerOptions": {
      "target": "ES5", // 目标语言的版本
      "module": "CommonJS", // 生成代码的模板标准
      "allowJS": true, // 允许编译器编译JS，JSX文件
      "checkJs": true, // 允许在JS文件中报错，通常与allowJS一起使用
      "outDir": "./dist", // 指定输出目录
      "rootDir": "./", // 指定输出文件目录(用于输出)，用于控制输出目录结构
      "removeComments": true, // 删除注释
      "noEmit": true, // 不输出文件,即编译后不会生成任何js文件
      "noEmitOnError": true, // 发送错误时不输出任何文件
      "strict": true, // 开启所有严格的类型检查
      "alwaysStrict": true // 在代码中注入'use strict'
    },
    // 指定一个匹配列表（属于自动指定该路径下的所有 ts 相关文件）
    "include": ["src/**/*"],
    // 指定一个排除列表（include 的反向操作）
    "exclude": ["demo.ts"],
    // 指定哪些文件使用该配置（属于手动一个个指定文件）
    "files": ["demo.ts"]
  }
  ```

- `tsc -w` 自动生成`.js` 文件

## 3、.d.ts

- `.d.ts` 文件用来：在 ts 文件中引入 js 不提示报错
