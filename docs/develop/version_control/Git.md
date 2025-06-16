!!! abstract "简介"
    :fontawesome-brands-git-alt: __git__ （/ɡɪt/）是一个免费的开源分布式版本控制系统，用于快速高效地处理任何或小或大的项目。

    git 不仅仅是个版本控制系统，它也是个内容管理系统(CMS)，工作管理系统等。

## Git 安装配置

### Git 安装

Git 各平台安装包下载地址为：[http://git-scm.com/downloads](http://git-scm.com/downloads)

=== ":fontawesome-brands-windows: Windows"
    __官网__

    官网下载地址：[https://git-scm.com/download/win](https://git-scm.com/download/win)
    
    __msysGit 安装包__
    
    安装包下载地址：[https://gitforwindows.org/](https://gitforwindows.org/)

    __winget 工具__

    ``` powershell
    winget install --id Git.Git -e --source winget
    ```

=== ":fontawesome-brands-linux: Linux/Unix"

    __Debian/Ubuntu__

    ``` bash
    apt-get install git
    ```
    
    __Centos/RedHat__
    
    ``` bash
    yum -y install git-core
    ```

    __Fedora__

    === "Fedora 21 及之前的版本"
        ``` bash
        yum install git
        ```
    === "Fedora 22 及更高新版本"
        ``` bash
        dnf install git
        ```

    __kali__
    
    ``` bash
    sudo apt install git
    ```

=== ":fontawesome-brands-apple: Mac"

    __Homebrew__

    === "安装 git"
        ``` bash
        brew install git
        ```
    === "安装 git-gui 和 gitk"
        ``` bash
        brew install git-gui
        ```
    
    __MacPorts__
    
    ``` bash
    sudo port install git
    ```

    __图形化 Git__
    
    下载地址：[https://sourceforge.net/projects/git-osx-installer/](https://sourceforge.net/projects/git-osx-installer/)


=== ":fontawesome-brands-github: 源码"

    __官网镜像__

    源码包下载地址：[https://mirrors.edge.kernel.org/pub/software/scm/git/](https://mirrors.edge.kernel.org/pub/software/scm/git/)

    __GitHub__

    ``` bash
    git clone https://github.com/git/git
    ```

安装好后可进行版本查看：
``` bash
git --version
```
### Git 配置
Git 提供了一个 `git config` 命令，用来配置或读取相应的工作环境变量。

#### 用户信息
配置个人的用户名称和电子邮件地址，commit 操作显示的信息（每次提交代码时记录提交者的信息）：
``` shell
git config --global user.name "<你的名字>" 
git config --global user.email <你的邮箱>
```
`--global` 表示对所有本地仓库的用户信息进行配置，如果要在某个特定的项目中使用其他名字或者邮箱，去掉 `--global` 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

#### 查看配置
检查已有的配置信息：
``` shell
git config --list
```

#### 生成 SSH 密钥
需要通过 SSH 进行 Git 操作，可以生成 SSH 密钥并添加到 Git 托管服务（如 GitHub 等）上：
``` shell
ssh-keygen -t rsa -b 4096 -C "<你的邮箱>"
```
#### 其他常用配置

彩色的命令行输出：
``` shell
git config --global color.ui auto
```

显示历史记录时，每个提交的信息只显示一行：
``` shell
git config format.pretty oneline
```

## Git 工作流程

=== "Git flow"
    
    1. 项目存在两个长期分支，用于存放对外发布的版本，任何时候在这个分支拿到的，都是稳定的分布版
        * 主分支 `master`
        * 开发分支 `develop`
    2. 项目存在三种短期分支， 用于日常开发，存放最新的开发版
        * 功能分支 `feature branch`
        * 补丁分支 `hotfix branch`
        * 预发分支 `release branch`

=== "Github flow"
    只有一个长期分支 `master`

    1. 需要开发新功能或者修复 BUG 的时候，从 `master` 拉出新分支，不区分功能分支或补丁分支
    2. 新分支开发完成后，或者需要讨论的时候，就向 `master` 发起一个 PR（pull request）
    3. PR 既提交代码，也可让其他同事 review 你的代码，在这个过程中，你可以不断提交 PR
    4. 如果你的 PR 被接受，合并进 `master`

=== "Gitlab flow"

### github 最佳实践 ❤️
__1. 克隆仓库__
   
如果你要参与一个已有的项目，首先需要将远程仓库克隆到本地：
```bash
git clone https://github.com/username/repo.git
cd repo
```

__2. 创建新分支__

避免直接在 main 或 master 分支上进行开发，先获取主干最新代码：
```bash
git checkout master
git pull
```
再新建一个开发分支 new-feature：
```bash
git checkout -b new-feature
```

__3. 工作区编辑__

在工作目录中进行代码编辑、添加新文件、删除不需要的文件。

__4. 暂存文件__

将修改过的文件添加到暂存区，以便进行下一步的提交操作：
=== "添加所有修改的文件"

    ```bash

    git add .
    ```

=== "添加指定修改的文件"

    ```bash
    git add <指定文件名>
    ```

__5. 提交分支 commit__

将暂存区的更改提交到本地仓库，并添加提交信息：
```bash
git commit -m "描述你的更改"
```

__6. 拉取最新更改__

在推送本地更改之前，最好从远程仓库拉取最新的更改，以避免冲突：
```bash
git pull origin new-feature
```

__7. 推送更改__

将本地的提交推送到远程仓库：
```bash
git push origin new-feature
```

__8. 在 GitHub 上发起 PR__

* 打开远程仓库页面，点击  __:material-source-pull:Pull request__ 
* 填写 PR 标题和描述，确认无误后提交给团队成员进行代码审查
* PR 合并后，你的更改就会合并到主分支

__9. 合并更改__

PR 审核通过并合并后，可以将远程仓库的主分支合并到本地分支：
```bash
git checkout main
git pull origin main
git merge new-feature
```

__10. 删除分支__

如果不再需要新功能分支，可以将其删除：
```bash
git branch -d new-feature
```
或者从远程仓库删除分支：
```bash
git push origin --delete new-feature
```