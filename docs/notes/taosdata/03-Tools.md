# tools install

- 安装 node+npm （nvm）

```bash
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 24

# Verify the Node.js version:
node -v # Should print "v24.12.0".

# Verify npm version:
npm -v # Should print "11.6.2".
```

- nvm 命令失效

```bash
编辑：~/.zshrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

刷新配置：source ~/.zshrc
```

- 配置 maven

```bash
# 找到java的安装目录
/usr/libexec/java_home -V
# 写入环境变量
echo 'export JAVA_HOME=$(/usr/libexec/java_home)' >> ~/.zshrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.zshrc
source ~/.zshrc
```

## 进行 python 版本管理

- brew install pyenv
- 添加配置

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

- 安装： pyenv install 3.12.3
- 设置全局版本： pyenv global 3.12.3
