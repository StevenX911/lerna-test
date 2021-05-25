# lerna实践

- lerna
- yarn


#### 参考文章

- https://juejin.cn/post/6844903918279852046
- https://juejin.cn/post/6844903911095025678
- https://juejin.cn/post/6844903749232623629
- https://www.jb51.net/article/171866.htm


#### FAQ：lerna 发布错误

* lerna http fetch PUT 404 https://registry.npmjs.org/@mo-demo%2fcli-shared-utils
    - 配置：`package.json > publishConfig > registry > https://registry.npmjs.org/`
    - 此方法无需修改全局镜像仓库配置，注意是修改的packages中具体包的package.json文件
* lerna ERR! E402 You must sign up for private packages
    - 配置：`package.json > publishConfig > access > public`
    - 此方法无需修改全局镜像仓库配置，注意是修改的packages中具体包的package.json文件
* lerna ERR! E404 Scope not found
    - 设置npm-scope: https://segmentfault.com/a/1190000017234785

#### lerna中集成yarn

```json
"npmClient": "yarn",
"useWorkspaces": true,
```

* 当使用yarn进行模块间的依赖建立时：
    * `yarn workspace package-1 add package-2`
    * 该命令需要请求网络，查找npm仓库
    * 现象：若包还没有发布，将报 `404错误`
    * 解决方法1：改用lerna创建依赖， `lerna add @tripfe/cli-mytest-app --scope @tripfe/cli`
    * 解决方法2：指定版本号安装，`yarn workspace @tripfe/cli-shared-utils add @tripfe/cli-mytest-app@^0.0.8`


#### prettier配置

- [官网](http://www.prettier.io/)
- [中文](无)

```json
{
  "printWidth": 80, //一行的字符数，如果超过会进行换行，默认为80
  "tabWidth": 2, //一个tab代表几个空格数，默认为80
  "useTabs": false, //是否使用tab进行缩进，默认为false，表示用空格进行缩减
  "singleQuote": false, //字符串是否使用单引号，默认为false，使用双引号
  "semi": true, //行位是否使用分号，默认为true
  "trailingComma": "none", //是否使用尾逗号，有三个可选值"<none|es5|all>"
  "bracketSpacing": true, //对象大括号直接是否有空格，默认为true，效果：{ foo: bar }
  "parser": "babylon" //代码的解析引擎，默认为babylon，与babel相同。
}
```

#### eslint配置

- [官网](https://eslint.org/)
- [中文](https://eslint.bootcss.com/)

```json
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "commonjs": true,
    "node": true,
    "es6": true,
    "jest": true
  },
  "parserOptions": {
    "ecmaVersion": 2018
  },
  "rules": {
    "no-console": "off",
    "strict": ["error", "global"],
    "curly": "warn"
  }
}
```


#### lerna 常用命令

| command                     | value                                                        | options                                                      |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `lerna init`                | 创建一个新的lerna项目或将已存在项目改造为lerna项目           | `--independent`/`-i`                                         |
| `lerna bootstrap`           | 当使用`yarn`并开启了`workspace`时等价于在根目录执行`yarn install` |                                                              |
| `lerna import <pathToRepo>` | 将本地路径`<pathToRepo>`中的包导入到`packages/<directory-name>`，并提交操作记录 |                                                              |
| `lerna publish`             | 对更新后的包发布新版本；使用新版本号标记；升级所有npm和git中的库 | `--npm-tag [tagname]`, `--canary/-c`, `--skip-git`, `--force-publish [packages]` |
| `lerna change`              | 检查自上次发布以来改动的包                                   |                                                              |
| `lerna diff [package?]`     | 比较自上次发布以来的所有或指定的包                           |                                                              |
| `lerna run [script]`        | 在每个包中执行一个npm script                                 |                                                              |
| `lerna ls`                  | 列出当前lerna项目中的public包                                |                                                              |