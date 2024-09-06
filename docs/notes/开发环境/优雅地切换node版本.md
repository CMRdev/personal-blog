## 1、优雅地切换node版本（windows）

- 卸载已安装的node：控制面板-程序-找到node并卸载

  ~~~bash
  通常在控制面板中卸载后，nodejs目录、环境变量、注册表就自动删除了，不放心可在卸载前在cmd窗口下输入命令`where node`查看node的安装路径。
  检查是否卸载干净：
  	检查nodejs目录是否删除
  	检查环境变量中有关nodejs的变量是否删除
  	检查注册表删除nodejs相关：windows+R -- regedit -- 计算机\HKEY_LOCAL_MACHINE\SOFTWARE
  ~~~

- 下载并安装`nvm`

  ~~~js
  https://github.com/coreybutler/nvm-windows/releases
  下载：nvm-setup.zip
  自定义安装路径：
  	nvm（D:\nvm）			// 自动创建用户/系统变量：NVM_HOME = D:\nvm 并添加到path
  	nodejs（D:\nodejs）	// 自动创建用户/系统变量：NVM_SYMLINK = D:\nodejs 并添加到path
  			             // 在D盘下创建nodejs快捷方式，指向`nvm use <version>`正在使用的nodejs版本
  cmd窗口下输入`nvm -v` 显示版本信息则安装成功
  ~~~

## 2、`nvm`的使用

> ```js
> nvm off                     // 禁用node.js版本管理(不卸载任何东西)
> nvm on                      // 启用node.js版本管理
> nvm install <version>       // 安装node.js的命名 version是版本号 例如：nvm install 8.12.0
> nvm uninstall <version>     // 卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
> nvm ls                      // 显示所有安装的node.js版本
> nvm list available          // 显示可以安装的所有node.js的版本
> nvm use <version>           // 切换到使用指定的nodejs版本，【若失败尝试以管理员身份运行】
> nvm v                       // 显示nvm版本
> nvm install stable          // 安装最新稳定版
> ```

## 3、处理`npm`版本与`nodejs`版本不匹配问题（通常不会有这个问题）

- 更新`npm`版本

  ~~~bash
  官网查看nodejs对应的npm版本：https://nodejs.org/zh-cn/download/releases
  更新到指定版本 `npm -g install npm@8.3.1`
  ~~~

## 4、npm install太慢问题

- 更换npm镜像：`npm config set registry https://registry.npm.taobao.org`
	- (验证`npm config get registry` 或 `npm info express`)

- 或：`npm i -g cnpm --registry=https://registry.npm.taobao.org`
