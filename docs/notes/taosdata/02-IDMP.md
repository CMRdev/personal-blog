# IDMP

## 1. e2e 本地测试配置

- .env.development

```js
TEST_LANGUAGE=zh
LOGIN_USERNAME=mingrenchen@taosdata.com
LOGIN_PASSWORD=tbase125!
```

- playwright.config.ts

```js
// 设置浏览器语言为英语
locale: 'en-US',
//locale: 'zh-CN', // 设置为中文
```

## 2. backend

- `mvn -T 1C clean package -Dskip.tests=true -Drevision=1.0.10.1`
- 开启 h2
- 启动项目
- 查看端口占用：`lsof -i | grep LISTEN`

### `mvn clean install -DskipTests`

- clean — 清理
  - 删除 `target/` 目录，清除上次构建产生的所有文件（编译产物、jar 包等），保证构建环境干净。

- install — 安装到本地仓库。执行完整的构建生命周期：
  - compile — 编译源代码
  - test — 运行单元测试（被 `-DskipTests` 跳过）
  - package — 打包成 jar/war
  - install — 将打好的包安装到本地 Maven 仓库（默认 `~/.m2/repository/`）

## 3. license过期

- 重新安装TSDB || `skipLecense = true`

## 4. FIX

- 有时报错，需要删除旧数据：
  - TDasset/data
  - TDasset/tda-server/data

- `mvn clean` 执行这个命令，然后运行，让`idea`自己去编译
