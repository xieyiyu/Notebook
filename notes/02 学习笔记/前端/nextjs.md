Next.js是一个基于React的一个服务端渲染简约框架。它使用React语法，可以很好的实现代码的模块化，有利于代码的开发和维护。

## Next的功能：
- 服务器端渲染(默认)
- 自动代码切分, 加速页面加载
- 简单的客户端路由(基于页面)
- 基于 Webpack 的开发环境, 支持热模块替换(HMR: Hot Module Replacement)
- 使用 React 的 JSX 和 ES6 的 module，模块化和维护更方便
- 可以使用 Express 或其他 Node.js 服务器实现
- 使用 Babel 和 Webpack 配置定制

## 文件含义
### package.json 
每个项目的根目录下面，一般都有一个 package.json 文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。
有了 package.json文件，直接使用npm install命令，就会在当前目录中安装所需要的模块，也就是配置项目所需的运行和开发环境

1. scripts 指定了运行脚本命令的 npm 命令行缩写，比如 start 指定了运行 npm run start 时，所要执行的命令。
下面的设置指定了 npm run start、npm run test 时，所要执行的命令。
```json
"scripts": {
    "start": "node index.js",
    "test": "tap test/*.js"
}
```

2. dependencies 字段指定了项目运行所依赖的模块，devDependencies 指定项目开发所需要的模块。
版本限制：
- 指定版本：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。
- 波浪号（tilde）+指定版本：比如 ~1.2.2，表示安装 1.2.x 的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。
- 插入号（caret）+指定版本：比如 ˆ1.2.2，表示安装 1.x.x 的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。
- latest：安装最新版本。

参考文档：https://javascript.ruanyifeng.com/nodejs/packagejson.html

### package-lock.json
package-lock.json 是在 `npm install` 时生成一份文件，用以记录当前状态下实际安装的各个 npm package 的具体来源和版本号。即锁定安装时的包版本号，需要上传到 git 上，以保证其他人在 install 时候，大家的依赖版本相同。

package.json 文件只能锁定大版本，即版本号的第一位，不能锁定后面的小版本，你每次npm install时候拉取的该大版本下面最新的版本。
一般为了稳定性考虑我们不能随意升级依赖包，因为如果换包导致兼容性bug出现很难排查，所以package-lock.json就是来解决包锁定不升级问题的。



