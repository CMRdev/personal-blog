## 使用`prettier`插件统一代码风格

- 在`vscode`中打开扩展并安装`Prettier-Code formatter`插件

- `ctrl+shift+p`打开`用户设置（JSON）`开始配置【只需配置`第1、4`行就好】

  ```json
  "editor.tabSize": 2,
  "editor.linkedEditing": true,
  "editor.formatOnSave": false,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[vue]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[scss]": {
      "editor.formatOnSave": true,
      "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
      "editor.defaultFormatter": "vscode.typescript-language-features"
  },
  "[html]": {
      "editor.defaultFormatter": "vscode.html-language-features"
  },
  ```

- 项目根目录下创建`.prettierrc`文件，配置代码的格式化风格

  ```json
  {
    "eslintIntegration": true,
    "singleQuote": true,
    "semi": false,
    "trailingComma": "none",
    "printWidth": 150
  }
  ```

  **属性解释**

  | 属性                         | 解释                                                         | 默认值                               |
  | :--------------------------- | ------------------------------------------------------------ | ------------------------------------ |
  | `eslintIntegration`          | 让 prettier 使用`eslint`的代码格式进行校验                   | false                                |
  | `arrowParens`                | 在唯一的箭头函数参数周围添加括号                             | always                               |
  | `bracketSpacing`             | 是否在对象属性与大括号之间填充空格                           | true                                 |
  | `endOfLine`                  | 设置换行风格，避免不同操作系统造成的大量代码`diff`           | `lf`(可选:`crlf、cr、auto`)          |
  | `htmlWhitespaceSensitivity`  | `html`空格敏感度                                             | `css`(可选:strict、ignore)           |
  | `insertPragma`               | 是否在文件插入标记表明该文件已被格式化处理过了               | false                                |
  | `singleAttributePerLine`     | 标签中有多个属性时进行换行，每行一个属性                     | false                                |
  | `bracketSameLine`            | 标签的右尖括号`>`是否跟随在最后一行属性末尾                  | false                                |
  | `jsxBracketSameLine`         | `jsx`中标签的右尖括号`>`是否跟随在最后一行属性末尾           | false                                |
  | `jsxSingleQuote`             | 是否在`JSX`中使用单引号                                      | false                                |
  | `printWidth`                 | 每行代码长度限制，超过则换行                                 | 80                                   |
  | `proseWrap`                  | (Markdown) wrap prose over multiple lines.                   | preserve                             |
  | `quoteProps`                 | 对象中的属性是否用引号包裹                                   | as-needed(可选:consistent、preserve) |
  | `requirePragma`              | 是否仅格式化文件开始位置存在特殊注释的代码                   | false                                |
  | `semi`                       | 是否在每行末尾添加分号                                       | true                                 |
  | `singleQuote`                | 使用单引号替代双引号                                         | false                                |
  | `tabWidth`                   | 制表符的空格长度                                             | 2                                    |
  | `trailingComma`              | 控制尾部逗号的打印                                           | `es5`(可选:none、all)                |
  | `useTabs`                    | 是否用制表符代替空格执行缩进                                 | false                                |
  | `vueIndentScriptAndStyle`    | 是否在`Vue`文件中对代码和标签进行缩进，script 和 style 部分  | false                                |
  | `embeddedLanguageFormatting` | 是否格式化一些文件中被嵌入的代码片段的风格，如果插件可以识别 | auto                                 |

- `vscode`默认格式化代码快捷键：`shift + alt + f`

