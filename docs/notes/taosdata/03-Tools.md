# 工具安装与配置

## 1、Node.js（nvm 管理）

### 安装 nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
```

### 安装 Node.js

```bash
nvm install 24
node -v  # v24.12.0
npm -v   # 11.6.2
```

### nvm 命令失效

编辑 `~/.zshrc`，添加以下内容：

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

```bash
source ~/.zshrc
```

---

## 2、Maven（配置 JAVA_HOME）

```bash
# 查找 Java 安装目录
/usr/libexec/java_home -V

# 写入环境变量
echo 'export JAVA_HOME=$(/usr/libexec/java_home)' >> ~/.zshrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.zshrc
source ~/.zshrc
```

---

## 3、Python（pyenv 管理）

### 安装 pyenv

```bash
brew install pyenv
```

### 配置环境变量（添加到 `~/.zshrc`）

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

### 常用命令

- `pyenv install 3.12.3` — 安装指定版本
- `pyenv global 3.12.3` — 设置全局默认版本
- `pyenv versions` — 查看已安装的所有版本
