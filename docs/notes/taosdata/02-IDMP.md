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

## 3. license过期

- 重新安装TSDB || `skipLecense = true`
