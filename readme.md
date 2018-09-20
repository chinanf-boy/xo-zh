# xo [![explain]][source] [![translate-svg]][translate-list] 
    
<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/xo-explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name
    


「 JavaScript幸福风格的linter 」

[中文](./readme.md) | [english](https://github.com/xojs/xo)


---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'xojs/xo' -->
<!-- commit = 'f435698295eb518eca73a74ff383dfcb79e6106a' -->
<!-- time = '2018 9.3' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018 9.3 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/xojs/xo.svg
[commit]: https://github.com/xojs/xo/tree/f435698295eb518eca73a74ff383dfcb79e6106a

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---


<h1 align="center">
	<br>
	<img width="400" src="https://github.com/xojs/xo/raw/master/media/logo.svg?sanitize=true" alt="xo">
	<br>
	<br>
	<br>
</h1>

> JavaScript幸福风格的linter

[![Build Status: Linux](https://travis-ci.org/xojs/xo.svg?branch=master)](https://travis-ci.org/xojs/xo) [![Build status: Windows](https://ci.appveyor.com/api/projects/status/mydb56kve054n2h5/branch/master?svg=true)](https://ci.appveyor.com/project/sindresorhus/xo/branch/master) [![Coverage Status](https://coveralls.io/repos/github/xojs/xo/badge.svg?branch=master)](https://coveralls.io/github/xojs/xo?branch=master) [![xo code style](https://img.shields.io/badge/code_style-xo-5ed9c7.svg)](https://github.com/xojs/xo) [![Gitter](https://badges.gitter.im/join_chat.svg)](https://gitter.im/xojs/Lobby)

固有己见,但包含许多好东西的可配置ESLint包装器.强制执行严格且可读的代码.再也不要在`Pull Request`上讨论代码样式了! 没有争论.没有`.eslintrc`或`.jshintrc`的管理.它只是工作!

下面会使用[ESLint](https://eslint.org),所以有关规则的问题应该打开在[eslint那里](https://github.com/eslint/eslint/issues).

*默认情况下支持JSX,但您需要[eslint-config-xo-react](https://github.com/xojs/eslint-config-xo-react#use-with-xo)用于React特定的linting.*

![](https://raw.githubusercontent.com/sindresorhus/eslint-formatter-pretty/master/screenshot.png)

## 强调

-   美丽的输出.
-   零配置,但是[可在需要时配置](#%E9%85%8D%E7%BD%AE).
-   强制执行可读代码,因为您阅读的代码一定多于您编写的代码.
-   无需指定lint的文件路径,因为它会审计除[常被忽略的路径](#ignores)之外的所有JS文件.
-   [配置覆盖每个 文件/globs.](#%E9%85%8D%E7%BD%AE%E8%A6%86%E7%9B%96)
-   包括许多有用的ESLint插件,比如[`unicorn`](https://github.com/sindresorhus/eslint-plugin-unicorn),[`import`](https://github.com/benmosher/eslint-plugin-import),[`ava`](https://github.com/avajs/eslint-plugin-ava),[`node`](https://github.com/mysticatea/eslint-plugin-node)等更多.
-   基于你的`package.json`的[`engines`](https://docs.npmjs.com/files/package.json#engines)自动启用.
-   在运行之间缓存结果,以获得更好的性能.
-   将xo添加到项目中非常简单`$ xo --init`.
-   自动修复许多问题`$ xo --fix`.
-   使用编辑器打开错误的文件正确的行`$ xo --open`.
-   指定喜欢的[缩进](#space)和[分号](#semicolon)很容易,而不会搞乱规则配置.
-   可选择使用[Prettier](https://github.com/prettier/prettier)代码风格.
-   伟大的[编辑器插件](#编辑器插件).

### 目录


<details>

<summary> >> 拉开 </summary>


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [安装](#%E5%AE%89%E8%A3%85)
- [用法](#%E7%94%A8%E6%B3%95)
- [默认代码样式](#%E9%BB%98%E8%AE%A4%E4%BB%A3%E7%A0%81%E6%A0%B7%E5%BC%8F)
- [工作流程](#%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B)
  - [之前](#%E4%B9%8B%E5%89%8D)
  - [之后](#%E4%B9%8B%E5%90%8E)
- [配置](#%E9%85%8D%E7%BD%AE)
  - [envs](#envs)
  - [globals](#globals)
  - [ignores](#ignores)
  - [space](#space)
  - [rules](#rules)
  - [semicolon](#semicolon)
  - [prettier](#prettier)
  - [nodeVersion](#nodeversion)
  - [plugins](#plugins)
  - [extends](#extends)
  - [extensions](#extensions)
  - [settings](#settings)
  - [parser](#parser)
  - [esnext](#esnext)
- [TypeScript和Flow](#typescript%E5%92%8Cflow)
  - [TypeScript](#typescript)
  - [Flow](#flow)
- [配置覆盖](#%E9%85%8D%E7%BD%AE%E8%A6%86%E7%9B%96)
- [提示](#%E6%8F%90%E7%A4%BA)
  - [使用父母的配置](#%E4%BD%BF%E7%94%A8%E7%88%B6%E6%AF%8D%E7%9A%84%E9%85%8D%E7%BD%AE)
  - [Monorepo](#monorepo)
  - [Transpilation](#transpilation)
- [常问问题](#%E5%B8%B8%E9%97%AE%E9%97%AE%E9%A2%98)
    - [xo是什么意思?](#xo%E6%98%AF%E4%BB%80%E4%B9%88%E6%84%8F%E6%80%9D)
    - [为什么不用标准风格?](#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E7%94%A8%E6%A0%87%E5%87%86%E9%A3%8E%E6%A0%BC)
    - [为什么不直接用ESLint?](#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E7%9B%B4%E6%8E%A5%E7%94%A8eslint)
- [编辑器插件](#%E7%BC%96%E8%BE%91%E5%99%A8%E6%8F%92%E4%BB%B6)
- [构建系统插件](#%E6%9E%84%E5%BB%BA%E7%B3%BB%E7%BB%9F%E6%8F%92%E4%BB%B6)
- [Configs](#configs)
- [支持](#%E6%94%AF%E6%8C%81)
- [有关](#%E6%9C%89%E5%85%B3)
- [徽章](#%E5%BE%BD%E7%AB%A0)
- [团队](#%E5%9B%A2%E9%98%9F)
        - [旧友](#%E6%97%A7%E5%8F%8B)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


</details>

## 安装

```
$ npm install --global xo
```

## 用法

```
$ xo --help

  Usage
    $ xo [<file|glob> ...]

  Options
    --init            将xo添加到项目中
    --fix             自动修复问题
    --reporter        记录使用
    --env             环境预设 [可多次设置]
    --global          全局变量 [可多次设置]
    --ignore          要忽略的其他路径 [可以多次设置]
    --space           使用空格缩进,而不是制表符 [默认值：2]
    --no-semicolon    不使用分号
    --prettier        符合更漂亮的代码风格
    --node-version    要支持的Node.js版本范围
    --plugin          包含第三方插件 [可多次设置]
    --extend          使用自定义配置扩展默认值 [可以多次设置]
    --open            在编辑器中打开包含问题的文件
    --quiet           仅显示错误，不显示警告
    --extension       lint的附加扩展 [可多次设置]
    --no-esnext       不执行 es2015+ 规则
    --cwd=<dir>       文件的工作目录
    --stdin           从stdin 验证/修复代码
    --stdin-filename  为--stdin 选项指定文件名

  Examples
    $ xo
    $ xo index.js
    $ xo *.js !foo.js
    $ xo --space
    $ xo --env=node --env=mocha
    $ xo --init --space
    $ xo --plugin=react
    $ xo --plugin=html --extension=html
    $ echo 'const x=true' | xo --stdin --fix

  Tips
    Put options in package.json instead of using flags so other tools can read it.
```

*请注意,使用全局CLI运行时,优先使用您本地安装的xo,即使在全局运行时也是如此.*

## 默认代码样式

*任何这些都可以[覆盖](#rules),如有必要.*

-   tab缩进*[(或空格)](#space)*
-   分号*[(或不要)](#semicolon)*
-   单引号
-   没有未使用的变量
-   代码关键字后的空格`if (condition) {}`
-   总用`===`代替`==`

看看[代码lint的例子](https://github.com/xojs/xo/blob/master/index.js)和[ESLint规则](https://github.com/xojs/eslint-config-xo/blob/master/index.js).

## 工作流程

建议的工作流程是: 在本地项目中添加xo,并使用测试运行它.

简单地运行`$ xo --init`(使用任何选项)将xo添加到`package.json`或创建一个.

### 之前

```json
{
	"name": "awesome-package",
	"scripts": {
		"test": "ava"
	},
	"devDependencies": {
		"ava": "^0.20.0"
	}
}
```

### 之后

```json
{
	"name": "awesome-package",
	"scripts": {
		"test": "xo && ava"
	},
	"devDependencies": {
		"ava": "^0.20.0",
		"xo": "^0.18.0"
	}
}
```

然后运行吧`$ npm test`,xo将在测试之前运行.

## 配置

您可以通过将它放在package.json中来配置xo中的一些选项:

```json
{
	"name": "awesome-package",
	"xo": {
		"space": true
	}
}
```

[eslint -> 全局](https://eslint.org/docs/user-guide/configuring#specifying-globals)和[eslint -> 规则](https://eslint.org/docs/user-guide/configuring#configuring-rules)可以在文件中内联配置.

### envs

name:| 环境变量
---|---
类型:|`Array`
默认:|`['node']`

哪一个[eslint -> 环境](https://eslint.org/docs/user-guide/configuring#specifying-environments)会在您的代码运行.

每个环境都带有一组预定义的全局变量.

### globals

类型:|`Array`
---|---
Desc:| 代码在执行期间访问的其他全局变量

### ignores

类型:|`Array`
---|---
Desc:| 一些[路径](https://github.com/xojs/xo/blob/master/lib/options-manager.js)默认情况下会被忽略,包括路径`.gitignore`.可以在此处添加其他忽略.

### space

name:|  空格
---|---
类型:|`boolean`,`number`
默认:|`false` *(Tab缩进)*

将其设置为`true`获得2空格缩进,或指定空格数.

出于实际原因,存在此选项,但我强烈建议您阅读["为什么tab更优越"](http://lea.verou.me/2012/01/why-tabs-are-clearly-superior/).

### rules

类型:|`Object`
---|---
Desc:| 覆盖任何一个[默认规则](https://github.com/xojs/eslint-config-xo/blob/master/index.js)

见[ESLint文档](https://eslint.org/docs/rules/)有关每条规则的更多信息.

请花一点时间考虑,是否确定需要使用此选项.

### semicolon

name:| 分号
---|---
类型:|`boolean`
默认:|`true` *(需要分号)*

将其设置为`false`,强制执行无分号样式.

### prettier

name:| prettier代码风格
---|---
类型:|`boolean`
默认:|`false`

用[Prettier](https://github.com/prettier/prettier)格式化代码.

该[Prettier的选项](https://prettier.io/docs/en/options.html)将从中[Prettier的配置](https://prettier.io/docs/en/configuration.html)读取,而如果 **没有设置** 将被确定为:

-   [semi](https://prettier.io/docs/en/options.html#semicolons): 基于[分号](#semicolon)选项
-   [useTabs](https://prettier.io/docs/en/options.html#tabs): 基于[space](#space)选项
-   [tabWidth](https://prettier.io/docs/en/options.html#tab-width): 基于[space](#space)选项
-   [trailingComma](https://prettier.io/docs/en/options.html#trailing-commas): 基于[esnext](#esnext)
-   [singleQuote](https://prettier.io/docs/en/options.html#quotes):`true`
-   [bracketSpacing](https://prettier.io/docs/en/options.html#bracket-spacing):`false`
-   [jsxBracketSameLine](https://prettier.io/docs/en/options.html#jsx-brackets):`false`

如果为 Prettier和xo 设置了矛盾的选项,则会抛出错误.

### nodeVersion

name:| node版本
---|---
类型:|`string`,`boolean`
默认值:|在项目`package.json`的`engines.node`字段

启用特定于配置范围内的Node.js版本的规则.如果设置为`false`,不会启用特定于Node.js版本的规则.

### plugins

类型:|`Array`
---|---
Desc:| 包括第三方[插件](https://eslint.org/docs/user-guide/configuring.html#configuring-plugins).

### extends

类型:|`Array`,`string`
---|---
Desc:| 使用一个或多个[可共享的配置](https://eslint.org/docs/developer-guide/shareable-configs.html)要么[插件配置](https://eslint.org/docs/user-guide/configuring#using-the-configuration-from-a-plugin)覆盖任何默认规则(如上面的[rules](#rules).

### extensions

类型:|`Array`
---|---
Desc:| 除`.js`和`.jsx`之外,还允许更多的扩展.确保它们受ESLint或ESLint插件的支持.

### settings

类型:|`Object`
---|---
Desc:| [共享ESLint设置](https://eslint.org/docs/user-guide/configuring#adding-shared-settings)给到[rules](#rules).

例如,要配置[`import`](https://github.com/benmosher/eslint-plugin-import#settings)插件,来使用您的webpack配置来确定搜索路径,你可以在这里加上`{"import/resolver": "webpack"}`.

### parser

类型:|`string`
---|---
Desc:| ESLint解析器.

例如,[`babel-eslint`](https://github.com/babel/babel-eslint)

如果您要使用ESLint尚不支持的语言功能.

### esnext

name:| es下一代语法
---|---
类型:|`boolean`
默认:|`true`

实施 es2015+ 规则.禁用此功能将不*执行* es2015+ 语法和约定.

即使没有此选项,也会解析 es2015+ .您已经可以使用 es2017等功能了[`async`/`await`](https://github.com/lukehoban/ecmascript-asyncawait).

## TypeScript和Flow

### TypeScript

看[eslint-config-xo-typescript#使用-xo](https://github.com/xojs/eslint-config-xo-typescript#use-with-xo)

### Flow

看[eslint-config-xo-flow#使用-xo](https://github.com/xojs/eslint-config-xo-flow#use-with-xo)

## 配置覆盖

xo可以轻松覆盖特定文件的配置.该`overrides`属性必须是覆盖对象的数组.每个覆盖对象必须包含一个glob字符串的`files`属性,或是一个glob字符串数组.其余属性与上述属性相同,并将覆盖基本配置的设置.

如果多个覆盖配置与同一个文件匹配,则每个匹配覆盖按其在数组中出现的顺序应用.这意味着数组中的最后一个覆盖,优先于先前的覆盖.请考虑以下示例:

```json
{
	"xo": {
		"semicolon": false,
		"space": 2,
		"overrides": [
			{
				"files": "test/*.js",
				"esnext": false,
				"space": 3
			},
			{
				 "files": "test/foo.js",
				 "esnext": true
			}
		]
	}
}
```

-   基本配置很简单`space: 2`,`semicolon: false`.除非另有说明,否则这些设置用于每个文件.

-   对于每个`test/*.js`文件,使用基本配置,但是`space`被覆盖为`3`,和`esnext`选项设置为`false`.生成的配置是:

```json
{
	"esnext": false,
	"semicolon": false,
	"space": 3
}
```

-   对于`test/foo.js`,首先应用基本配置,然后是第一个覆盖配置(它的glob模式也匹配`test/foo.js`),最后应用第二个覆盖配置.生成的配置是:

```json
{
	"esnext": true,
	"semicolon": false,
	"space": 3
}
```

## 提示

### 使用父母的配置

如果你有一个嵌套的目录结构`package.json`文件,您希望跳过其中一个子清单,您可以通过设置`"xo": false`.

例如,当你有单独的应用程序和`electron-builder`中的开发`package.json`文件.

### Monorepo

放一个`package.json`在你的根目录配置,和在您的捆绑包中添加`"xo": false`到了`package.json`.

### Transpilation

如果项目中的某些文件,被转换为支持较旧的Node.js版本,则可以使用[配置覆盖](#%E9%85%8D%E7%BD%AE%E8%A6%86%E7%9B%96)为这些文件设置特定[`nodeVersion`](#nodeversion)目标版本选项.

例如,如果您的项目以 *Node.js 4* 为目标(您的`package.json`配置了`engines.node`设置`>=4`),而你正在使用[AVA](https://github.com/avajs/ava),然后自动转换您的测试文件.你可以覆盖测试文件的`nodeVersion`:

```json
{
	"xo": {
		"overrides": [
			{
				"files": "{test,tests,spec,__tests__}/**/*.js",
				"nodeVersion": ">=9"
			}
		]
	}
}
```

## 常问问题

#### xo是什么意思?

它的意思是[拥抱与亲吻](https://en.wiktionary.org/wiki/xoxo).

#### 为什么不用标准风格?

[标准风格](https://standardjs.com)是一个非常酷的想法.我也希望我们可以有一种风格来统治它们! 但实际情况是,JS社区过于多样化,并且无法创造*统一*代码风格.他们也错误地推出自己的风格,而不是最受欢迎的风格.相比之下,xo更加务实,没有抱负*单一*样式.我使用xo的目的是，简单地接近无配置使用来实现一致的代码样式.xo默认带有我的代码样式首选项,因为我主要为自己制作,但一切都是可配置的.

#### 为什么不直接用ESLint?

xo基于ESLint.这个项目最初只是一个可共享的ESLint配置,但它很快就发展了.我想要更简单的东西.只是输入`xo`就完成.没有争论.没有配置.我也有一些令人兴奋的未来计划.但是,在使用ESLint时,您仍然可以获得大部分[ESLint可共享配置](https://github.com/xojs/eslint-config-xo),来自xo优势.

## 编辑器插件

-   [Sublime](https://github.com/xojs/SublimeLinter-contrib-xo)
-   [atom](https://github.com/xojs/atom-linter-xo)
-   [Vim](https://github.com/xojs/vim-xo)
-   [TextMate 2](https://github.com/claylo/xo.tmbundle)
-   [VSCode](https://github.com/SamVerschueren/vscode-linter-xo)
-   [Emacs](https://github.com/j-em/xo-emacs)
-   [WebStorm](https://github.com/jamestalmage/xo-with-webstorm)

## 构建系统插件

- [Gulp](https://github.com/xojs/gulp-xo)
- [Grunt](https://github.com/xojs/grunt-xo)
- [webpack](https://github.com/Semigradsky/xo-loader)
- [Metalsmith](https://github.com/blainsmith/metalsmith-xo)
- [Fly](https://github.com/lukeed/fly-xo)


## Configs

-   [eslint-config-xo](https://github.com/xojs/eslint-config-xo)- 带有tab缩进的xo的ESLint可共享配置
-   [eslint-config-xospace](https://github.com/xojs/eslint-config-xo-space)- 具有2空格缩进的xo的ESLint可共享配置
-   [eslint-config-xo-react](https://github.com/xojs/eslint-config-xo-react)- 用于上述的React的ESLint可共享配置
-   [stylelint-config-xo](https://github.com/xojs/stylelint-config-xo)- 带有tab缩进的xo的Stylelint可共享配置
-   [stylelint-config-xospace](https://github.com/xojs/stylelint-config-xo-space)- 具有2空格缩进的xo的Stylelint可共享配置
-   [tslint-xo](https://github.com/xojs/tslint-xo)-  xo的TSLint可共享配置
-   [eslint-config-xo-typescript](https://github.com/xojs/eslint-config-xo-typescript)-  TypeScript的ESLint可共享配置
-   [eslint-config-xo-flow](https://github.com/xojs/eslint-config-xo-flow)-  Flow的ESLint可共享配置

## 支持

-   [Gitter聊天](https://gitter.im/xojs/Lobby)
-   [推特](https://twitter.com/sindresorhus)

## 有关

-   [eslint-plugin-unicorn](https://github.com/sindresorhus/eslint-plugin-unicorn)- 各种棒棒的ESLint规则 *(捆绑在xo中)*
-   [xo-summary](https://github.com/LitoMore/xo-summary)- 显示`xo`样式的输出错误列表,按计数排序

## 徽章

向世界展示你正在使用xo→[![xo code style](https://img.shields.io/badge/code_style-xo-5ed9c7.svg)](https://github.com/xojs/xo)

```md
[![xo code style](https://img.shields.io/badge/code_style-xo-5ed9c7.svg)](https://github.com/xojs/xo)
```

## 团队

| [![Sindre Sorhus](https://github.com/sindresorhus.png?size=130)](https://sindresorhus.com) | [![Mario Nebl](https://github.com/marionebl.png?size=130)](https://github.com/marionebl) | [![Pierre Vanduynslager](https://github.com/pvdlg.png?size=130)](https://github.com/pvdlg) |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [Sindre Sorhus](https://sindresorhus.com)                                                  | [马里奥内布尔](https://github.com/marionebl)                                                   | [Pierre Vanduynslager](https://github.com/pvdlg)                                           |

###### 旧友

-   [詹姆斯塔尔马](https://github.com/jamestalmage)
-   [迈克尔迈耶](https://github.com/schnittstabil)

## 执照

MIT
