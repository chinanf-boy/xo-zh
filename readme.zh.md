
<h1 align="center">
	<br>
	<img width="400" src="media/logo.svg" alt="XO">
	<br>
	<br>
	<br>
</h1>

> JavaScript幸福风格的linter

[![Build Status: Linux](https://travis-ci.org/xojs/xo.svg?branch=master)](https://travis-ci.org/xojs/xo) [![Build status: Windows](https://ci.appveyor.com/api/projects/status/mydb56kve054n2h5/branch/master?svg=true)](https://ci.appveyor.com/project/sindresorhus/xo/branch/master) [![Coverage Status](https://coveralls.io/repos/github/xojs/xo/badge.svg?branch=master)](https://coveralls.io/github/xojs/xo?branch=master) [![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/xojs/xo) [![Gitter](https://badges.gitter.im/join_chat.svg)](https://gitter.im/xojs/Lobby)

包含许多好东西的Opinionated但可配置的ESLint包装器.强制执行严格且可读的代码.再也不要在拉取请求上讨论代码样式了!没有决策权.没有`.eslintrc`要么`.jshintrc`管理.它只是工作!

用途[ESLint](https://eslint.org)在下面,所以有关规则的问题应该打开[那里](https://github.com/eslint/eslint/issues).

*默认情况下支持JSX,但您需要[eslint-CONFIG-XO-反应](https://github.com/xojs/eslint-config-xo-react#use-with-xo)用于React特定的linting.*

![](https://raw.githubusercontent.com/sindresorhus/eslint-formatter-pretty/master/screenshot.png)

## 强调

-   美丽的输出.
-   零配置,但是[可在需要时配置](#config).
-   强制执行可读代码,因为您阅读的代码多于您编写的代码.
-   无需指定lint的文件路径,因为它会删除除.之外的所有JS文件[常被忽略的路径](#ignores).
-   [配置覆盖每个文件/ globs.](#config-overrides)
-   包括许多有用的ESLint插件,比如[`unicorn`](https://github.com/sindresorhus/eslint-plugin-unicorn),[`import`](https://github.com/benmosher/eslint-plugin-import),[`ava`](https://github.com/avajs/eslint-plugin-ava),[`node`](https://github.com/mysticatea/eslint-plugin-node)和更多.
-   自动启用基于的规则[`engines`](https://docs.npmjs.com/files/package.json#engines)在你的领域`package.json`.
-   在运行之间缓存结果以获得更好的性能.
-   将XO添加到项目中非常简单`$ xo --init`.
-   自动修复许多问题`$ xo --fix`.
-   使用编辑器中正确的行打开所有错误的文件`$ xo --open`.
-   指定[缩进](#space)和[分号](#semicolon)首选项很容易,而不会搞乱规则配置.
-   可选择使用[漂亮](https://github.com/prettier/prettier)代码风格.
-   大[编辑插件](#editor-plugins).

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
    --init            Add XO to your project
    --fix             Automagically fix issues
    --reporter        Reporter to use
    --env             Environment preset  [Can be set multiple times]
    --global          Global variable  [Can be set multiple times]
    --ignore          Additional paths to ignore  [Can be set multiple times]
    --space           Use space indent instead of tabs  [Default: 2]
    --no-semicolon    Prevent use of semicolons
    --prettier        Conform to Prettier code style
    --node-version    Range of Node.js version to support
    --plugin          Include third-party plugins  [Can be set multiple times]
    --extend          Extend defaults with a custom config  [Can be set multiple times]
    --open            Open files with issues in your editor
    --quiet           Show only errors and no warnings
    --extension       Additional extension to lint [Can be set multiple times]
    --no-esnext       Don't enforce ES2015+ rules
    --cwd=<dir>       Working directory for files
    --stdin           Validate/fix code from stdin
    --stdin-filename  Specify a filename for the --stdin option

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

*请注意,CLI将在可用时使用您本地安装的XO,即使在全局运行时也是如此.*

## 默认代码样式

*任何这些都可以[覆盖](#rules)如有必要.*

-   标签缩进*[(或空间)](#space)*
-   分号*[(或不)](#semicolon)*
-   单引号
-   没有未使用的变量
-   关键字后的空格`if (condition) {}`
-   总是`===`代替`==`

看看[例](index.js)和[ESLint规则](https://github.com/xojs/eslint-config-xo/blob/master/index.js).

## 工作流程

建议的工作流程是在项目中本地添加XO并使用测试运行它.

简单地跑`$ xo --init`(使用任何选项)将XO添加到package.json或创建一个.

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

### 后

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

然后跑吧`$ npm test`和XO将在测试之前运行.

## 配置

您可以通过将它放在package.json中来配置XO中的一些选项:

```json
{
	"name": "awesome-package",
	"xo": {
		"space": true
	}
}
```

[全局](https://eslint.org/docs/user-guide/configuring#specifying-globals)和[规则](https://eslint.org/docs/user-guide/configuring#configuring-rules)可以在文件中内联配置.

### envs

类型:`Array`<br>默认:`['node']`

哪一个[环境](https://eslint.org/docs/user-guide/configuring#specifying-environments)您的代码旨在运行.

每个环境都带有一组预定义的全局变量.

### 全局

类型:`Array`

代码在执行期间访问的其他全局变量.

### 忽略

类型:`Array`

一些[路径](lib/options-manager.js)默认情况下会被忽略,包括路径`.gitignore`.可以在此处添加其他忽略.

### 空间

类型:`boolean`,`number`<br>默认:`false` *(制表符缩进)*

将其设置为`true`获得2空格缩进或指定空格数.

出于实际原因存在此选项,但我强烈建议您阅读["为什么标签更优越"](http://lea.verou.me/2012/01/why-tabs-are-clearly-superior/).

### 规则

类型:`Object`

覆盖任何一个[默认规则](https://github.com/xojs/eslint-config-xo/blob/master/index.js).见[ESLint文档](https://eslint.org/docs/rules/)有关每条规则的更多信息.

请花一点时间考虑是否确实需要使用此选项.

### 分号

类型:`boolean`<br>默认:`true` *(需要分号)*

将其设置为`false`强制执行无分号样式.

### 漂亮

类型:`boolean`<br>默认:`false`

格式化代码[漂亮](https://github.com/prettier/prettier).

该[更漂亮的选择](https://prettier.io/docs/en/options.html)将从中读取[更漂亮的配置](https://prettier.io/docs/en/configuration.html)而如果**没有设置**将确定如下:

-   [半](https://prettier.io/docs/en/options.html#semicolons): 基于[分号](#semicolon)选项
-   [useTabs](https://prettier.io/docs/en/options.html#tabs): 基于[空间](#space)选项
-   [tabWidth](https://prettier.io/docs/en/options.html#tab-width): 基于[空间](#space)选项
-   [trailingComma](https://prettier.io/docs/en/options.html#trailing-commas): 基于[esnext](#esnext)
-   [singleQuote](https://prettier.io/docs/en/options.html#quotes):`true`
-   [bracketSpacing](https://prettier.io/docs/en/options.html#bracket-spacing):`false`
-   [jsxBracketSameLine](https://prettier.io/docs/en/options.html#jsx-brackets):`false`

如果为Prettier和XO设置了矛盾的选项,则会抛出错误.

### nodeVersion

类型:`string`,`boolean`<br>默认值:.的值`engines.node`关键在于项目`package.json`

启用特定于配置范围内的Node.js版本的规则.如果设置为`false`,不会启用特定于Node.js版本的规则.

### 插件

类型:`Array`

包括第三方[插件](https://eslint.org/docs/user-guide/configuring.html#configuring-plugins).

### 扩展

类型:`Array`,`string`

使用一个或多个[可共享的配置](https://eslint.org/docs/developer-guide/shareable-configs.html)要么[插件配置](https://eslint.org/docs/user-guide/configuring#using-the-configuration-from-a-plugin)覆盖任何默认规则(如`rules`以上).

### 扩展

类型:`Array`

除此之外,还允许更多的扩展`.js`和`.jsx`.确保它们受ESLint或ESLint插件的支持.

### 设置

类型:`Object`

[共享ESLint设置](https://eslint.org/docs/user-guide/configuring#adding-shared-settings)接触规则.例如,要配置[`import`](https://github.com/benmosher/eslint-plugin-import#settings)插件使用您的webpack配置来确定搜索路径,你可以把`{"import/resolver": "webpack"}`这里.

### 解析器

类型:`string`

ESLint解析器.例如,[`babel-eslint`](https://github.com/babel/babel-eslint)如果您正在使用ESLint尚不支持的语言功能.

### esnext

类型:`boolean`<br>默认:`true`

实施ES2015 +规则.禁用此功能将使其无效*执行*ES2015 +语法和约定.

\*即使没有此选项,也会解析ES2015 +.您已经可以使用ES2017等功能了[`async`/`await`](https://github.com/lukehoban/ecmascript-asyncawait).

## TypeScript和Flow

### 打字稿

看到[eslint-配置-XO-打字稿#使用与 -  XO](https://github.com/xojs/eslint-config-xo-typescript#use-with-xo)

### 流

看到[eslint-配置-XO流#使用与 -  XO](https://github.com/xojs/eslint-config-xo-flow#use-with-xo)

## 配置覆盖

XO可以轻松覆盖特定文件的配置.该`overrides`property必须是覆盖对象的数组.每个覆盖对象必须包含一个`files`属性是一个glob字符串,或一个glob字符串数组.其余属性与上述属性相同,并将覆盖基本配置的设置.如果多个覆盖配置与同一文件匹配,则每个匹配覆盖按其在数组中出现的顺序应用.这意味着数组中的最后一个覆盖优先于先前的覆盖.请考虑以下示例:

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

-   对于每个文件`test/*.js`,使用基本配置,但是`space`被覆盖了`3`,和`esnext`选项设置为`false`.生成的配置是:

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

如果你有一个嵌套的目录结构`package.json`文件,您希望跳过其中一个子清单,您可以通过设置`"xo": false`.例如,当你有单独的应用程序和开发`package.json`文件`electron-builder`.

### Monorepo

放一个`package.json`在您的配置在根和添加`"xo": false`到了`package.json`在您的捆绑包中.

### Transpilation

如果项目中的某些文件被转换为支持较旧的Node.js版本,则可以使用[配置覆盖](#config-overrides)设置特定的选项[`nodeVersion`](#nodeversion)这些文件的目标.

例如,如果您的项目以Node.js 4为目标(您的`package.json`配置了`engines.node`设置`>=4`)你正在使用[AVA](https://github.com/avajs/ava),然后自动转换您的测试文件.你可以覆盖`nodeVersion`对于测试文件:

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

#### XO是什么意思?

它的意思是[拥抱与亲吻](https://en.wiktionary.org/wiki/xoxo).

#### 为什么不标准?

该[标准风格](https://standardjs.com)这是一个非常酷的主意.我也希望我们可以有一种风格来统治它们!但实际情况是,JS社区过于多样化,并且无法创造*一*代码风格.他们也错误地推出自己的风格而不是最受欢迎的风格.相比之下,XO更加务实,没有抱负*该*样式.我使用XO的目的是简单地使用接近无配置来实现一致的代码样式.XO默认带有我的代码样式首选项,因为我主要为自己制作,但一切都是可配置的.

#### 为什么不是ESLint?

XO基于ESLint.这个项目最初只是一个可共享的ESLint配置,但它很快就发展了.我想要更简单的东西.只是打字`xo`并完成.没有决策权.没有配置.我也有一些令人兴奋的未来计划.但是,在使用ESLint时,您仍然可以获得大部分XO优势[ESLint可共享配置](https://github.com/xojs/eslint-config-xo).

## 编辑插件

-   [崇高文本](https://github.com/xojs/SublimeLinter-contrib-xo)
-   [原子](https://github.com/xojs/atom-linter-xo)
-   [Vim](https://github.com/xojs/vim-xo)
-   [TextMate 2](https://github.com/claylo/XO.tmbundle)
-   [VSCode](https://github.com/SamVerschueren/vscode-linter-xo)
-   [Emacs的](https://github.com/j-em/xo-emacs)
-   [WebStorm](https://github.com/jamestalmage/xo-with-webstorm)

## 构建系统插件

-   [吞](https://github.com/xojs/gulp-xo)
-   [咕噜](https://github.com/xojs/grunt-xo)
-   [的WebPack](https://github.com/Semigradsky/xo-loader)
-   [Metalsmith](https://github.com/blainsmith/metalsmith-xo)
-   [飞](https://github.com/lukeed/fly-xo)

## Configs

-   [eslint-配置-XO](https://github.com/xojs/eslint-config-xo)- 带有制表符缩进的XO的ESLint可共享配置
-   [eslint-配置-XO空间](https://github.com/xojs/eslint-config-xo-space)- 具有2空格缩进的XO的ESLint可共享配置
-   [eslint-CONFIG-XO-反应](https://github.com/xojs/eslint-config-xo-react)- 用于上述的React的ESLint可共享配置
-   [stylelint-配置-XO](https://github.com/xojs/stylelint-config-xo)- 带有制表符缩进的XO的Stylelint可共享配置
-   [stylelint-配置-XO空间](https://github.com/xojs/stylelint-config-xo-space)- 具有2空格缩进的XO的Stylelint可共享配置
-   [tslint-xo](https://github.com/xojs/tslint-xo)-  XO的TSLint可共享配置
-   [eslint-配置-XO-打字稿](https://github.com/xojs/eslint-config-xo-typescript)-  TypeScript的ESLint可共享配置
-   [eslint-CONFIG-XO-流](https://github.com/xojs/eslint-config-xo-flow)-  Flow的ESLint可共享配置

## 支持

-   [Gitter聊天](https://gitter.im/xojs/Lobby)
-   [推特](https://twitter.com/sindresorhus)

## 有关

-   [eslint-插件 - 麒麟](https://github.com/sindresorhus/eslint-plugin-unicorn)- 各种令人敬畏的ESLint规则*(捆绑在XO中)*
-   [XO-汇总](https://github.com/LitoMore/xo-summary)- 显示输出`xo`作为样式错误列表,按计数排序

## 徽章

向世界展示你正在使用XO→[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/xojs/xo)

```md
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/xojs/xo)
```

## 球队

| [![Sindre Sorhus](https://github.com/sindresorhus.png?size=130)](https://sindresorhus.com) | [![Mario Nebl](https://github.com/marionebl.png?size=130)](https://github.com/marionebl) | [![Pierre Vanduynslager](https://github.com/pvdlg.png?size=130)](https://github.com/pvdlg) |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [Sindre Sorhus](https://sindresorhus.com)                                                  | [马里奥内布尔](https://github.com/marionebl)                                                   | [Pierre Vanduynslager](https://github.com/pvdlg)                                           |

###### 前任的

-   [詹姆斯塔尔马](https://github.com/jamestalmage)
-   [迈克尔迈耶](https://github.com/schnittstabil)

## 执照

MIT
