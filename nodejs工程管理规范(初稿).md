# nodejs工程推荐目录结构
```
ROOT DIR /
  |- app.js               项目入口文件
  |- package.json         项目依赖以及打包
  |- README.md            总工程的README，子工程或任意一个子目录需要额外说明的都应增加对应的README
  |- .gitignore           排除在版本控制库之外的说明文件
  |- libs/                与业务无关的公用模块
  |- common/              跟业务相关的公用模块
  |- test/                项目的单元测试文件
  |- routers/             业务相关的逻辑代码
  |- public/              client端的相关代码
  |- views/               视图模板
  |- node_modules/        项目依赖文件(排除在项目外，依据package.json进行安装)
  |- tool/                构建/发布/测试等相关脚本
  |- doc/                 开发文档的目录
```