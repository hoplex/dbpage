# 第 3 节 运行前端项目

这章写给“非开发人员”.毕竟等着推送、等着部署,是一件特别难熬的事情.

这篇文档,来自我的库存,稍微整理了下.

### 1 运行前端项目

执行类似如下命令,就可以运行前端项目(框架+拉取的表单组).

```js
npm install
npm run dev
```



**没有npm命令?那就,继续看文档吧~~~**



### 2 利用nvm管理安装nodejs

先介绍nodejs和npm的关系.

##### 2.1 nodejs和npm关系

- 包含关系：nodejs中含有npm，比如说你安装好nodejs，你打开cmd输入npm -v会发现出现npm的版本号，说明npm已经安装好。
- node.js：是javascript的一种运行环境，是对Google V8引擎进行的封装。是一个服务器端的javascript的解释器。
- npm：是nodejs的包管理器（package manager）。我们在Node.js上开发时，会用到很多别人已经写好的javascript代码，如果每当我们需要别人的代码时，都根据名字搜索一下，下载源码，解压，再使用，会非常麻烦。于是就出现了包管理器npm。大家把自己写好的源码上传到npm官网上，如果要用某个或某些个，直接通过npm安装就可以了，不用管源码在哪里。并且如果我们要使用模块A，而模块A又依赖模块B，模块B又依赖模块C和D，此时npm会根据依赖关系，把所有依赖的包都下载下来并且管理起来。试想如果这些工作全靠我们自己去完成会多么麻烦！

**注意:我电脑是mac,对windows仅有参考意义,若有不同,请自行网络搜索.**

##### 2.2 安装NVM

查资料得出，要使用 curl 或 wget 来安装(版本可以选用官网最新版)：

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
```

或:

```
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
```

注意：安装完了，重新打开 Terminal(iTerm2) 来重启会话

##### cnpm

如果直接安装node多次不成功建议使用cnpm.参考链接:http://npm.taobao.org/

##### 2.3 安装 Node.js

```
nvm ls-remote
```
nvm ls-remote 会列出所有可用的 Nodejs 版本，如果输出中看到很多很多个版本号，就表示 nvm 安装好了。最后一个版本号就是当前最新的 Nodejs 版本，我这里是 v11.0.0 。


##### 最新版
1. 安装最新版 Node.js，命令：

```
nvm install node
/// $ nvm install v6.11.2
```
2. 查看安装效果，命令：

```
nvm use node
```
显示：Now using node v7.5.0 (npm v4.1.2)
##### 稳定版（LTS）
安装 LTS 版，命令：

```
nvm install --lts
```

查看安装效果，命令：nvm list(nvm ls)，显示：

```
   ->    v6.9.5
         v7.5.0
         system
default -> node (-> v7.5.0)
node -> stable (-> v7.5.0) (default)
stable -> 7.5 (-> v7.5.0) (default)
iojs -> N/A (default)
lts/* -> lts/boron (-> v6.9.5)
lts/argon -> v4.7.3 (-> N/A)
lts/boron -> v6.9.5
```
##### 设置默认版本

```
nvm alias default v10.10.0
```
##### 切换版本

从上面的安装列表上已经可以看到，我们安装了一个最新版，一个稳定版。分别是：v6.9.5 和 v7.5.0，我们要如何切换不同版本呢？
1. 切换到 v6.9.5，命令：nvm use v6.9.5，显示：Now using node v6.9.5 (npm v3.10.10)
2. 切换到 v7.5.0，命令：nvm use v7.5.0，显示：Now using node v7.5.0 (npm v4.1.2)

到这里，我们基本会使用 nvm 了，想用什么版本就可以自由切换。 但如果想玩得更爽一点，就要学习如下一些技巧。
##### 使用别名

你肯定也想到，每次输入v6.9.5 好麻烦。并且时间长了，不一定记得住后面是9.5，还是8.6的版本号。
1. 设定 LTS 版别名，命令：nvm alias 6 v6.9.5，显示：6 -> v6.9.5
2. 设定最新版别名，命令：nvm alias 7 v7.5.0，显示：7 -> v7.5.0

切换node版本
nvm use v6.10.2
将此版本设为默认
nvm alias default v6.10.2
这样就大功告成了。

##### 删除已定义的别名

```
nvm unalias <name>
```

##### 卸载

- homebrew安装的
直接一条命令 
brew uninstall node

- 官网下载pkg安装包的
一条命令 
```
sudo rm -rf /usr/local/{bin/{node,npm},lib/node_modules/npm,lib/node,share/man/*/node.*}
```

[Mac下彻底卸载node和npm](https://blog.csdn.net/shiquanqq/article/details/78032943)

### 3 运行pages前端项目

终于回到开头的命令.执行类似如下命令,就可以运行前端项目.

```js
npm install
npm run dev
```



**心中有疑惑?那就,继续看文档吧~~~**



##### 3.1 npm install 做了哪些事情

为了在开发过程中，安装功能模块的方便，产生了npm包管理器。npm类似于python的pip、mac下的brewhome等.前面提过.

在git clone项目的时候，项目中并没有 node_modules 文件夹。

为什么呢？

我们知道这个文件中保存的是我们项目开发中所使用的依赖模块。这个文件夹可能有几百兆大小，如果放到github上，其它人clone的时候会非常慢，这个时候就想到用一个package.json依赖配置文件解决这个问题。

这样每个人下载这个项目的时候，只需要进入该项目目录 直接npm install npm就会到里面去找需要的函数库，也就是依赖。

例如package.json里有一段

```
"dependencies": {"vue": "2.5.17","vue-router": "3.0.2", "element-ui": "2.4.6",},
```

那么npm install就会读取dependencies中的模块，下载这些模块文件。

那么这些依赖会放在什么地方呢？我们在哪里能找到这些依赖文件呢？

npm install执行完以后，我们会发现项目多了一个 node_modules文件夹。我们安装的依赖文件都可以在这里面找到哦~。

##### 3.2 npm install ...和npm install 有哪些区别呢

npm install <...> 只下载依赖模块，package.json中dependencies并没有改变。

npm install <...> --save 会自动往 package.json中"dependencies" 添加xxx属性。

npm install <...> --save -dev 自动往package.json中"devdependencies" 添加xxx属性。

注：

dependencies：生产环境需要依赖的库

devdependencies：只有开发环境下需要依赖的库

### 4 删除依赖模块

项目运行不了,有时是因为依赖模块安装有问题,这个时候就要删除依赖模块重新安装了.

```js
npm install rimraf -g
rimraf node_modules
```

