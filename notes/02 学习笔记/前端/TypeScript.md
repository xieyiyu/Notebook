TypeScript 是 JavaScript 的超集，扩展了 JavaScript 的语法，因此现有的 JavaScript 代码可与 TypeScript 一起工作无需任何修改，TypeScript 通过类型注解提供编译时的静态类型检查。

TypeScript 可处理已有的 JavaScript 代码，并只对其中的 TypeScript 代码进行编译。

## 安装
```sh
$ npm install -g typescript
```

## 编译 TypeScript 文件
tsc 是 TypeScript 编译器，可以将编译结果生成 js 文件， *.ts 是 TypeScript 文件的后缀
```sh
$ tsc file.ts
```

## js jsx ts tsx 的区别
### js 和 jsx
js 是前端开发语言
jsx 是 React 框架下用的，要在 React 框架中的使用编译器编译成 js 语言才能使用的。

jsx 相当于 javascript 和 XML 结合的一种格式，当遇到 <，JSX 就当 HTML 解析，遇到 { 就当 JavaScript 解析。
JSX 只是为 React.createElement(component, props, …children) 方法提供的语法糖。React 自创了JSX语法，是一个 JavaScript 的语法扩展，官方建议在 React 中配合使用 JSX 来替代原始的 JS。因为JSX 可以更好的描述 UI 应该呈现出它应有交互的本质形式。

### ts 和 js
JavaScript：是弱类型语言，容易出现一些编译时不报错，运行时crash的问题。
TypeScript: 是编译时语言，一些问题可以更早的别发现。TypeScript 是JavaScript 的超集，即包含JavaScript 的所有元素，能运行JavaScript 的代码，并扩展了JavaScript 的语法。相比于JavaScript ，它还增加了静态类型、类、模块、接口和类型注解方面的功能，更易于大项目的开发。

使用 TypeScript 语法写的 .ts .tsx 等后缀的程序是不能直接运行的，需要通过 tsconfig.json 文件中配置的 “target”: “es6”, 这项配置转换为 es6 语法的 .js 文件。

TypeScript 中的 import 只会加载 .ts .tsx 后缀的文件，而 Javascript 中的 import 只能加载 .js 等后缀的文件

### ts 和 tsx
将.ts用于纯 Typescript 文件。
将.tsx用于包含 JSX 的文件。

例如，react 组件是 .tsx，但是包含辅助函数的文件是 .ts

## TSLint
TSLint 是可扩展的静态分析工具，检查 typescript 的可读性、可维护性和功能性错误。支持规则配置。
tslint核心规则：https://palantir.github.io/tslint/rules/

## 相关文件
### tsconfig.json
tsconfig.json 文件中指定了用来编译这个项目的根文件和编译选项。
如果项目目录下存在一个tsconfig.json文件，那么它意味着这个目录是 TypeScript 项目的根目录。

在TS的项目中，TS最终都会被编译JS文件执行，TS编译器在编译TS文件的时候都会先在项目根目录的tsconfig.json文件，根据该文件的配置进行编译，默认情况下，如果该文件没有任何配置，TS编译器会默认编译项目目录下所有的.ts、.tsx、.d.ts文件。实际项目中，会根据自己的需求进行自定义的配置

配置说明参考 https://www.cnblogs.com/cczlovexw/p/11527708.html


## 参考文档
https://www.runoob.com/w3cnote/getting-started-with-typescript.html


