---
title: node安装
date: 2016-09-22 23:11:31
tags: 
---
  初探一下hexo的流程，以及复习复习之前学习的基础东西，也为了以后自己方便观看和分享学习成果。初学者，基础知识不是太官方。。见谅。。直奔主题。

------
## 一、Node简介

### **Node.js是什么？**
  Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

  **注意**：*Node.js 的包管理器 npm，是全球最大的开源库生态系统。node中只能运行ECMAScript，无法使用 BOM 和 DOM，也就是说，他只是一个js运行环境。*

## 二、Node简介及安装
### 使用nvm安装Node.js
  Node版本发展很快，版本前后差异性大，全局安装的第三方组件和node版本相关造成全局版本混乱。nvm是解决这一问题的利器。
  nvm是node版本管理工具。它的主要特点是：
    * 可安装多版本的node。
    * 灵活切换当前的node版本。
    * 全局安装第三方组件到对应版本的node中。
  ***ps：***nvm 是 Mac 下的 node 管理工具,如果是需要管理 Windows 下的 node，官方推荐是使用 nvmw 或 nvm-windows
  **下载 nvm 包 地址：https://github.com/coreybutler/nvm-windows/releases**
  下载安装nvm这里就不在赘述了(需要注意最好不要将其安装在中文目录下)。
  安装 nvm 之前最好先删除下已安装的 node 和全局 node 模块
### 配置相关的环境变量
  1. 先使用*管理员权限运行***install.cmd**
  2. 根目录生成一个***settings.txt***的文本文件,将其剪切到nvm目录下。
  然后我们把他修改成这样：
  ```
    root: D:\dev\nvm      //这里表示的是当前文件夹路径
    path: D:\dev\nodejs   //这里表示配置后要要生成的目录
    arch: 64              //这里为自己电脑的机器位数
    proxy: none
  ```
  3. 先***配置nvm的环境变量***，让其能够在cmd中使用其命令
  我们还会发现，在Path中也会自动添加上D:\dev\nvm;或者是D:\dev\nodejs，如果有的话，把他们删掉，没有的话更好。
    （1）先添加：NVM_HOME的变量值为：D:\dev\nvm
    （2）再在Path的最前面输入： ;%NVM_HOME%;
    （3）打开一个cmd窗口输入命令：nvm 若看到当前nvm的版本信息。就可以安装nodejs了
  4. **安装nodejs**并**配置相关环境**
    （1）配置node环境:先添加：NVM_HOME的变量值为：D:\dev\nodejs,再在Path的最前面输入： ;%NVM_SYMLINK%;
    （2）继续输入命令：nvm install latest 我们会看到正在下载的提示，下载完成后 会让你use那个最新的node版本。
    （3）如果你是第一次下载，在use之前，D:\dev目录下是没有nodejs这个文件夹的，在输入比如： nvm use 5.11.0之后，你会发现，D:\dev目录下多了一个nodejs文件夹，这个文件夹不是单纯的文件夹，它是一个快捷方式，指向了 D:\dev\nvm 里的 v5.11.0 文件夹。
    （4）同样的咱们可以下载其他版本的nodejs，这样通过命令:nvm use 版本号 比如：nvm use 5.11.0就可以轻松实现版本切换了。
    **备注**： 如果你的电脑系统是32位的，那么在下载nodejs版本的时候，一定要指明 32 如： nvm install 5.11.0 32这样在32位的电脑系统中，才可以使用，默认是64位的。

  5. ***安装npm及相关指令***
    **备注**：在每个版本的nodejs中，都会自带npm，为了统一起见，我们安装一个全局的npm工具，这个操作很有必要，因为我们需要安装一些全局的其他包,不会因为切换node版本造成原来下载过的包不可用。
    （1）首先我们进入命令模式,输入 npm config set prefix "D:\dev\nvm\npm" 回车，这是在配置npm的全局安装路径,然后在用户文件夹下会生成一个。npmrc的文件,用记事本打开后可以看到如下内容：prefix=D:\dev\nvm\npm
    （2）然后继续在命令中输入： npm install npm -g 回车后会发现正在下载npm包,在D:\dev\nvm\npm目录中可以看到下载中的文件,以后我们只要用npm安装包的时候加上 -g 就可以把包安装在我们刚刚配置的全局路径下了。
    （3）我们为这个npm配置环境变量： 变量名为：NPM_HOME，变量值为 ：D:\dev\nvm\npm在Path的最前面添加;%NPM_HOME%，注意了，这个一定要添加在 %NVM_SYMLINK%之前，所以我们直接把它放到Path的最前面.最后我们新打开一个命令窗口，输入npm -v ,此时我们使用的就是我们统一下载的npm包了。
    （4）相关指令：
    初始化：npm init
    安装： npm install PackageName --save-dev
    卸载： npm uninstall PackageName --save-dev