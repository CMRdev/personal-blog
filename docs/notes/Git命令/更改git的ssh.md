1. 配置一下 name 、eamil

```bash
git config --global user.name '用户名'
git config --global user.email '邮箱'
```

2. 生成 SSH KEY

```bash
ssh-keygen -t rsa -C '邮箱'
# -t：type 指定密钥的类型 通常为RSA或DSA
# -C：commit 提供一个注释 通常用于标注密钥的用途或其他信息
```

3. 复制 .ssh/id_rsa.pub 文件内容
4. 打开 git 网站，右上角用户头像，点击 settings，左侧菜单 SSH KEYS，将文件内容复制到 key 里 添加就可以了
