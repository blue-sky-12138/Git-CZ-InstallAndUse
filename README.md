# Git-CZ-InstallAndUse

## 环境安装

1. Commitizen是一个格式化commit message的工具。它的安装需要NPM的支持，NPM是Node.js的包管理工具，首先需要自行安装node.js

2. 安装Commitizen

   ```bash
   npm install -g commitizen
   ```

3. 安装changelog，这是生成changelog的工具

   ```bash
   npm install -g conventional-changelog
   npm install -g conventional-changelog-cli
   ```

4. 安装standard-version，这是帮你做了自动打tag，自动生成changelog等过程

   ```bash
   npm install -g standard-version
   ```

5. 安装符合Angular风格的校验规则

   ```bash
   npm install -g @commitlint/config-conventional
   ```

6. 安装huksy（git钩子工具）

   ```bash
   npm install husky --save-dev
   ```

7. 检验是否安装成功

   ```bash
   npm ls -g -depth=0
   ```

8. 如果你的工程名目录下没有package.json文件，需要造在你的项目目录里执行一下命令以生成一空的package.json文件

   ```bash
   npm init --yes
   ```

   可以加入--froce来进行覆盖创建

9. 运行下面命令，使其支持Angular的Commit message格式

   ```bash
   commitizen init cz-conventional-changelog --save --save-exact
   ```

   如果当前已经有其他适配器被使用，则会报错，此时可以加上--force选项进行再次初始化

   一般来说，会有以下字段的依赖：

   - @commitlint/cli
   - @commitlint/config-conventional
   - cz-conventional-changelog
   - husky
   - standard-version

   如果有项目已初始化过，可以拷贝该项目package.json下的devDependencies和config下的commitizen字段内容到项目的package.json内以跳过该步骤

10. 运行下列命令自动生成一个更新日志

    ```bash
    conventional-changelog -p angular -i CHANGELOG.md -s
    ```

    上面命令不会覆盖以前的 Change log，只会在CHANGELOG.md的头部加上自从上次发布以来的变动

    如果你想生成所有发布的 Change log，要改为运行下面的命令

    ```bash
    conventional-changelog -p angular -i CHANGELOG.md -w -r 0
    ```

接下来你就可以使用cz的命令`git cz`代替`git commit`进行提交说明



## 懒人优化

为了方便使用，可以将其写入package.json的scripts字段

```
"release": "git cz  && git push origin master && standard-version && git push --follow-tags origin master"
```

这样下次commit时只需要先add你要提交的文件并运行下列命令

```bash
npm run release
```

就会自动迭代版本号、生成tag并提交到远程仓库



## 作者的字段保留部分

```
  "devDependencies": {
    "@commitlint/cli": "^12.0.0",
    "@commitlint/config-conventional": "^12.0.0",
    "cz-conventional-changelog": "^3.3.0",
    "husky": "^5.1.1",
    "standard-version": "^9.1.1"
  },
  
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "release": "git cz  && git push origin master && standard-version && git push --follow-tags origin master"
  },
  
  "config": {
    "commitizen": {
      "path": "D:/software/Nodejs/node_modules/cz-conventional-changelog"
    }
  },
  
```

