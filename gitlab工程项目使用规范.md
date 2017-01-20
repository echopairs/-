### 工程筹建

按照工程要求建立基本的工程目录，如cpp版本：http://note.youdao.com/group/#/35619624/md/119366796?full


### 分支管理

- 分支概览
```
// all branches:
master
xiaoming_dev
jack_dev
tom_dev
...
release_0.1
release_0.1.1
release_0.2
...
// all tags:
v_0.1.1
v_0.2
...
```

- 保护分支
    
    `master`分支为核心主分支，只有指定的管理员有权限进行合并、提交和其他管理

- 个人分支

    一个工程里面的每个开发者，都应当建立自己的开发分支，并独立自主管理自己的分支（适时将别人的代码merge到自己的分支，将自己的代码主要提交到自己的开发分支），定期将自己的开发成果申请到master的merge request或pull request。

- 发布分支和Tag
    
    按照版本发布要求，定期从master分支分出发布分支，测试完备后，打出tag。发布分支和tag均进行保护处理。

### issue管理

- bug管理

- 需求管理


