# npm包管理

### 1. npm常用命令

```

1) npm init // 初始化工程
2) npm init -y  // 初始化工程时忽略package.json的一堆问题，直接采用默认值
3) npm install -g npm // 更新npm版本
4) npm list <--depth=0> // 显示所有依赖模块
5) npm home <package> // 直接打开依赖包主页
6）npm repo <package> // 直接打开依赖包主页
7）npm docs <package> // 直接打开依赖包的文档页
8）npm bugs <package> // 直接打开依赖包的issue页
9）npm outdated <-g> // 找到过时的模块
10）npm list <package> // 查看一个独立模块的版本
11）npm view <package> // 显示一个模块的所有信息
12）npm link // 该命令为模块在全局目录创建一个符号链接，开发npm模块本地调试时可以实现边开发边试用， require('***') 会自动加载本机开发中的模块。
            // Node规定，使用一个模块时，需要将其安装到全局的或项目的 node_modules 目录之中。对于开发中的模块，解决方法就是在全局的 node_modules 目录之中，
            // 生成一个符号链接，指向模块的本地目录。

```

### 2. package.json详解

每个项目的根目录下面，一般都有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。
npm install 命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

package.json文件就是一个JSON对象，该对象的每一个成员就是当前项目的一项设置，一项完成的package.json如下：

```
{
    "name": "demo", //必填
    "version": "", //必填
    "description": "",
    "keywords": ["", ""], // npm搜索关键字
    "homepage": "https://github.com/owner/project", //一般工程git地址 npm home <name> 会直接网址
    // 运行npm bugs 会自动打开浏览器以及issue地址
    "bugs": {
        "url": "https://github.com/owner/project/issues",
        "email": "project@hostname.com"
    } OR "https://github.com/owner/project/issues",
     "license": "",
    "private": ture | false, //(和license: "UNLICENSED" 效果一致)
    "author": "",
    "contributors": [{
        "name": "",
        "email": "",
        "url": ""
    },{},……],
    "files":[],
    "main": "js相对地址", //用户安装此工程依赖包(该工程已发布到npm)，require("name")时获取的就是该配置js exports出的模块，默认根目录下的index.js
    "browser": "js相对地址"  //和main的配置一样，只是该依赖只能用于浏览器端，可以使用window等浏览器对象
    "bin": "",
    "man": "" OR ["",""], // 指定一个单一的文件名或一个文件名数组来让man程序使用
    "directories": {

    },
    "repository": {
        //指明你的代码被托管在何处
        "type": "git/svn",
        "url": "https://github.com/npm/cli.git"
    },
    "scripts": {
        // 指定运行脚本的npm命令行缩写
        "build": "需执行脚本命令"
    },
    "config": {
        // 设置全局配置,用于添加命令行的环境变量，可以通过process.env.npm_package_config_<key>获取字段
        "port": "8080"  //process.env.npm_package_config_port可以获取，通过npm config set demo:port 8180可以覆盖
    },
    "dependencies": {
        //依赖包
    },
    "devDependencies": {
        //依赖包
    },
    "peerDependencies": {
        // 传递依赖过来的依赖包要求的版本，使用某个依赖时，该依赖包必须提前安装某个版本的它的依赖包
    },
    "bundledDependencies": {

    },
    "optionalDependencies": {

    },
    "engines": {
        // 该模块运行的平台
        {
            "node": "版本",
            "npm": "版本"
        }
    },
    "os": ["darwin","linux","!win32"],
    "cpu" ["x64","ia32","!arm"],
    "publishConfig": {
        "tag": "",
        "registry": "",
        "access": ""
    }
}

```

### 3. 发布npm包

1）创建账户：[npm官网 https://www.npmjs.com/](https://www.npmjs.com/)

2）命令行内通过npm login 登录

3）创建工程

4）npm publish 发布npm包

5）修改版本号，重新发布来实现更新

6）删除发布包：npm unpublish <package> --force

### 4. 开发命令行工具

在实际开发时，搭建项目时一件很繁琐的事情，尤其是在对一个框架的用法还不熟悉的时候，于是很多框架都自带一套脚手架工具，在初始化前端项目的时候就可以不用自己从头搭建
只要在命令行输入初始化命令即可。那么如果自行开发出这样一个命令行工具来初始化自定义项目呢？

准备知识：
* package.json  bin配置项
* commander.js  // git风格的命令行开发工具
* inquirer.js // guide风格的命令行开发工具
* chalk.js   // 设置终端字符串输出风格工具

开发步骤：

1). 在package.json里面添加bin配置项

```
"bin": {
    "命令": "可执行文件位置"
}

```

2). 安装commonder.js 或者 in inquirer.js依赖，在可执行文件内引入

```
#!/usr/bin/env node   // 在代码的开头第一行，必须指定我们的脚本执行所需要的解释程序，/usr/bin/env,可以查看到PATH，使用env找到node作为程序的解释程序

// 引入依赖
var program = require('commander');
const chalk = require('chalk');

// 链式调用方法，定义programe的相关配置
program
    .version('1.0.0','-v,--version')  // 定义版本号(必须), 自定义标志(可省略),默认为-V和--version
    .usage('')   // 设置Usage(用法)提示语
    // 第一个参数必须，分为长短两种命令，中间用逗号，竖线或者空格分割，命令后面可跟必须参数(用<>包含)和可选参数(用[]包含)，第二个参数为命令描述，
    // 使用--help命令时显示命令描述，第三个参数默认值可省略
    .option('-n[param], --name<param>', 'name description', 'default name') 
    // 第一个参数命令名称<必须>：命令后面可跟用 <> 或 [] 包含的参数；命令的最后一个参数可以是可变的，像实例中那样在数组后面加入 ... 标志；在命令后面传入的参数会被传入
    // 到 action 的回调函数以及 program.args 数组中，第三个参数配置选项
    .commond('系统命令<param1>[param2...]','description',opts)
    .action(fn) // 定义命令执行完的回调函数
    .on('--help',fn)  // 自定义--help显示内容，必须在parse前
    .parse(process.argv) //用于解析process.argv，设置options以及触发commands

...其他业务逻辑...

```

3). 调试与发布
    
**本地调试：**
    通过 npm link 命令建立全局符号链接，使用本地模块

**线上使用：**
    * 通过npm publish发布npm包
    * cd新的目录下，通过npm install <package> -g 全局安装
    * <package> init 命令 创建脚手架即可或运行其他命令

### 5.常用npm包介绍