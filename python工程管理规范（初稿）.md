# python 工程推荐目录结构
[ref](http://monklof.com/post/19/)
```
project /
  |- bin/               项目可执行文件，通过pyinstaller等工具生成exe（排除在版本控制库之外）
  |- tests/             单元测试
  |- project/           package dir(包含模块modules以及各种包packages)
  |   |- __init__.py    指示project是一个package
  |   |- xxx.py         xxx module
  |   |- ...            ...
  |   |- package/       children-package
  |      |- __init__.py
  |      |- xxx.py  
  |- tool/              构建/发布/测试等相关脚本
  |- docs/              开发文档的目录
  |- README.md          总工程的README，子工程或任意一个子目录需要额外说明的都应增加对应的README
  |- .gitignore         排除在版本控制库之外的说明文件
  |- setup.py           安装、部署、打包的脚本
  |- requirements.txt   项目依赖的包以及对应包的版本号
  |- main.py            程序入口        
```