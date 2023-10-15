# Git

---

> 分布式版本控制系统

- git学习网站 [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)

- git初始化

  - git Clone 克隆已存在项目
    - git Clone github链接
    - clone网络错误问题
    - 设置代理:7890 clash的代理端口号
      - git config --**global** http.proxy http:*//127.0.0.1:7890* 
      - git config --**global** https.proxy http:*//127.0.0.1:7890*
  - git init 将本地某个项目加入git管理
    - 如果新建的仓库,这个仓库的文件都是未被跟踪状态, 未被跟踪的文件不会加入版本控制
    - git add将状态改为已跟踪加入版本控制并且加入缓冲区

- 代码提交

  - git add 加入缓存区

    - git add. 操作当前目录所有文件

  - git commit -m "备注" 提交到本地仓库

    - 注意 如果直接输入git commit会打开vim让你填写备注,如果直接-m 备注不用打开vim
      - 输入i启动编辑模式开始输入
      - 输入esc退出编辑模式
      - 输入:wq保存内容  

  - git log 查看提交记录

    ![image-20230511214248026](C:%5CUsers%5CPhelop%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230511214248026.png)

    > commit 后面为此次提交id
    >
    > git reset --head 提交id 用来恢复到某次提交版本 
    >
    > --head:重置模式,会将工作空间,暂存区,仓库,全部重置
    >
    > head:当前活跃的分支

  - git push 提交到远程仓库

  - git branch 分支名根据当前分支状态创建分支,分支上提交代码不会影响主分支

    - git checkout 分支名 切换到该分支
    - git checkout -b 分支名 创建并切换到该分支

  - git pull拉取到工作目录

    - git fetch 拉取到本地仓库 执行git merge才会跟工作空间合并

  - git remote add upstream 改变merge分支']

  - originl:默认远端仓库名

- ### 基础命令
  
  - pwd:显示当前位置
  - ls:显示目录下所有文件
  - cd:切换目录,后面跟目录名是下一级,..是上一级
  - git config :设置配置文件
    - git config --global代表全局
    - git config --global user.name 用户名 设置用户名
    - git config --global user.email 邮箱 设置邮箱 
  
- 添加文件进缓冲区
  
  - git init 初始化当前文件夹 加入git控制
  - git add 文件名.后缀 提交到缓冲区,临时保存
    - git add 添加当前目录所有文件
  - git commit 提交到本地仓库  拥有历史记录
    - 会进入vim编辑器进行编辑提交备注
    - vim操作
      - i:进入编辑模式
      - esc退出编辑模式
      - :wq 保存并退出vim
    - git commit -m 消息 可以跳过vim编辑
  
- git log 查看提交日志
  
- ### 指令
  
  - git clone 拉取远程项目到工作空间
  - git push 从本地仓库提交到远程仓库
  - git init git初始化 当前文件夹设置为git文件夹
  - git status 查看当前文件状态
  - git add 加入暂存区
    - git add 文件名 指定文件加入
    - git add . 所有文件加入
  - git commit 提交本地仓库
    - git commit - m  "备注内容"
    - 提交时添加备注信息
  
- git push  提交到远程仓库
  
- ### 忽略文件

  - 将一部分本地配置文件或者不想提交的文件进行忽略配置

  - 主目录新键.gitignore文件,按照语法进行配置即可

    ![image-20230319181403577](https://raw.githubusercontent.com/1v10/Photo/main/photo/202303191814723.png)



- git提交到远程仓库时需要生成公钥, 注册到对应远程仓库,比如github,gitee

- 关于设置后仍然无法 clone和push 需要设置git代理
  
  - [Git - SSL_ERROR_SYSCALL 问题解决 | hyperzsb's ideas](https://hyperzsb.io/posts/git-ssl-error/)
  
- 命令: ssh-keygen -t rsa

- 会自动生成在用户名/.shh目录下
  
  - ![image-20230319185546591](https://raw.githubusercontent.com/1v10/Photo/main/photo/202303191855630.png)
  
- git branch 分支名称 创建分支

- git checkout 分支名称 切换到该分支

- git checkout -b 分支名称 创建并切换到该分支

- git checkout commitID 让HEAD指向某次提交记录

  - commitID:提交记录的ID hash值 sha算法
  - HEAD:变量 默认指向当前分支的最新提交记录

- 多条提交记录合并:

  - https://juejin.cn/post/7050705771218075684

    git rebase -i commitId(该提价记录之后的提交记录进行合并)

    ![img](data:image/png;base64,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)

    命令名称+commit hash +comment

    \#则是提示说明

    Pick:保留该提交记录 缩写p

    Squash:与前一个commit合并 缩写s

    这里使用的是Vim编辑器!

    https://juejin.cn/post/7050705771218075684

     Enter:进入编辑模式

    :q! 强制退出不保存

    :wq 保存后退出

    :wq! 强制保存后退出

     之后会进行编辑注释 提交即可

- Cherry pick 将指定的提交记录提交到其他分支

  - git cherry-pick commitid
  -  Git cherry-pick commitID 可以写多个ID 以空格分开

- 交互式rebase

  rebase加参数--interactive (-i)

  增加了该参数 git会打开一个UI界面列出可以被复制的备选提交记录 会显示Hash值

   这个UI可以做几件事:

  1.调整提交记录的顺序 通过鼠标拖放

  2.删除不想要的提交 通过切换PICK来完成

  3 合并提交

   如果有多次提交记录 需要只把某一次提交记录提交的主分支 那么就需要用到

  Git rebase - i

  Git cherry-pick

   git commit --amend 修正提交记录

   Git merge git rebase 要合并的分支或者提交记录

- 恢复

  - git reset commitID:直接退回到某次提交记录 抹除本次提交历史

  - git revert commitID: 增加一次提交 提交内容为想恢复的提交记录 会留下恢复历史

  - 假设有A,B,C三次提交 A为最新想要撤销

    撤销提交

    git reset HEAD~1 当前引用指向了B 恢复到了B的版本

    此时A就消失了 相当于改写了历史 

    于是最好使用另一个命令

    先把HEAD移动某次想恢复的提交记录上

    git revert 该命令就是在提交一次新提交D 而这个D与上一个B内容相同 只是留下了履历

    本地就用git reset 

    远程就用gir revert

    后面可以跟提交记录 也可以用HEAD

- HEAD 指向分支和提交的指针有什么区别?

  - HEAD 是一个特殊的指针，它指向当前所在的分支或提交。 当 HEAD 指向分支时，它指向该分支的最新提交，表示当前所在的分支。在这种情况下，如果进行提交，该分支将会移动到新的提交上，并且新的提交将成为分支的最新提交。 当 HEAD 指向具体的提交时，它指向一个特定的提交，而不是分支。这种情况被称为"分离 HEAD"。在分离 HEAD 的状态下，如果进行提交，将创建一个匿名分支，该分支不与任何命名分支关联，因此新的提交不会影响其他分支。这种情况下直接在分离 HEAD 上提交可能会导致提交被遗忘，因为没有其他分支引用该提交。 总结起来，HEAD 指向分支时表示当前所在的分支，而HEAD 指向提交时处于分离 HEAD 状态，表示当前位于一个特定的提交上，没有与该提交相关联的分支引用。

- git 远程操作

  - git clone
  - main 本地仓库
  - origin/main  远程仓库名/远程分支名  origin默认为远程仓库的名称 缩写o
    - 远程分支本质上用来反应远程仓库对应分支的状态   远程分支反映了远程仓库在你**最后一次与它通信时**的状态
  - 如果在本地直接切换到远程仓库 那么HEAD不会指向远程仓库 会成为分离HEAD 此时所有的提交都会提交到一个匿名分支 不会与其他任何分支有关联

- git fetch

  - 远程分支本质上用来反应远程仓库的状态   但是不会自动更新 可能会与远程有所差别 那么单独更新远程仓库分支 就需要用到git fetch
  - 当远程仓库获取数据时 远程分支也会更新以反应远程仓库的状态 
  - 本质上git fetch就是将本地仓库的远程分支更新成远程仓库对应分支的最新状态
  - git fetch不会更改你本地仓库的状态 也不会更新你本地的main分支 也不会修改磁盘上的文件
  - git fetch 只是单纯将更新下载下来了 并没有合并
  - 适用git fetch 将更新下载到了远程分支上 我们只需要将该远程分支上的更新合并到本地仓库的分支即可 比如适用 git merge

- git cherry-pick 针对于单个提交

- git rebase 和git merge针对整个分支的提交

- git pull

  - = git fetch + git merge

- git push

  - 与git pull相反
  - push有一些行为设定 与push.default文件有关

- 一般会在 feather的特性分支上工作!

- rebase和merge的优缺点

  - rebase整洁 但是由于会修改提交树 会将提交记录早的记录放在晚的记录之后
  - rebase会有多个提交合并 但是会保留提交历史

- 远程仓库分支与本地远程仓库分支关联

  - 本地分支是如何与远程分支关通过remote tracking进行关联

  - git clone时会将这种关系进行绑定 

  - git clone时首先会把远程仓库中分支都会在本地仓库创建对应远程分支

    然后会默认创建一个本地分支main用来跟踪本地的远程分支

  - 所以 git clone时 会输出 local branch "main" set to track remote branch "o/main"

  - 这种隐式关联会设置push目的地和pull的目标

- 指定remote tracking

  - git checkout -b feature origin/main
    - 此时创建一个分支feature 它跟踪 远程分支 origin/main
  - git brnach -u origin/main 在当前分支执行该命令 就会让当前分支追踪origin/main

- git push remote-name  local-branch-name

  - 想将本地更改推送都某个远程分支 但又不想切换分支 或者是游离HEAD状态 push时指定远程和分支名称进行推送
  -  git push origin(远程仓库名称) main(本地分支名称) 将main改动推送到到 origin仓库main分支中
  - 可以在分离HEAD下使用

- git push remote-name  local-branch-name: remote-branch-name

  - git push origin  feature:main
  - push也可以指定远程仓库的具体分支  比如上面就是将本地分支feature推送到远程的main分支  
  - 本地分支可以使用相对引用只提交一部分记录 feature^  
  - 如果指定的远程分支不存在 那么就会创建

- 本地的远程分支其实叫远程追踪分支

  - git clone 会把远程分支的快照保存到本地
  - 在 Git 中，本地仓库和远程仓库是分开管理的。当你克隆一个远程仓库时，Git 会在本地保存远程仓库的快照。这包括所有分支和标签。本地对远程的追踪是通过 "远程追踪分支" 实现的。

- git fetch 指定参数拉取 跟push类似 但方向相反

  - git fetch origin main :会到远程仓库的main分支进行拉取然后放到本地的o/main上
    - 该拉取只会下载对应本地远程分支更新 并不会下载其他远程分支  而且也不会合并的对应分支上
    - git fetch默认下载所有远程分支的更新

  - git fecht origin main:feature  会到远程仓库的main分支拉取并且放到本地的o/feature分支上 如果feature不存在 则会进行创建
    - 拉取指定分支 合并到指定分支
  - git push 指定参数的危险用法!
    - git push origin  :foo   把空推送到foo分支 这会删除远程分支foo!
    - git fetch origin   foo:  这会在本地创建foo分支
  - git pull本质上就是在git fetch后面加git merge 所有参数通用
    - git pull origin foo = git fetch origin foo + git merge origin/foo
    - git pull origin bar-1:bugfix = git fetch origin bar~1:bugFix + git merge bugFix
  - git pull 最终会合并到当前分支里
  - git pull origin main:feature
    - 如果feature不存在则会创建 然后拉取main分支最新 然后把合并到feature里面 然后再合并到当前分支