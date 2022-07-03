# Git
**本章节的内容按照[cs-self-learning](https://github.com/PKUFlyingPig/cs-self-learning)的内容参考了尚硅谷的git教程**

## 1. Git介绍
1. 是一种版本控制工具，Git的内容都是在本地的，性能优于SVN等
2. 版本控制指记录文件内容变化，记录文件修改历史记录
3. 从个人到团队协作，需要版本控制
4. 版本控制工具（集中式、分布式）
5. 工作机制：工作区（写代码后放的位置），暂存区（临时存储，可删），本地库（生成的历史版本，此时的历史版本已经删不掉了） ，远程库（系统中不一定有，代码托管中心*互联网GitHub、Gitee，局域网GitLab*）
## 2. Git安装
1. 去到git的官网，下载对应版本号、系统的安装包
2. 直接安装，路径选择**无中文无空格**的目录下
3. 勾选需要的组件，我一般主选项只勾选2桌面右键、3大文件、4文本编辑器、5关联.sh，其他都不勾选，建议直接默认
4. 选择你喜欢的编辑器
5. 后面的一路默认即可，关于是否要cmd中也能使用git bash（更改环境变量）我的建议是，如果您对计算机的环境变量理解深刻，则可以勾选第二个，否则勾选第一个
6. 打开Git Bash查看
## 3. Git命令
> 注：大多数命令在bash中使用`git --help`即可查看，要善用官方提供的工具

1. 设置用户签名
	+ 名字`git config --global user.name "your name"`
	+ 邮箱`git config --global user.email "your email"`
	+ 打开C:/用户/yourusername/.gitconfig，即可查看设置是否成功
2. 初始化本地库
	+ 打开需要用git管理的项目目录（*可以用命令行，也可以从文件资源管理器进入然后右键git bash*）
	+ use `git init`这样就初始化创建了一个本地库，然后我们用linux命令`ll`或`ll -a`来查看其中的文件和隐藏文件
3. 查看本地库状态
	+ use`git status`命令查询状态
4. 添加暂存区
	+ use `git add 文件名`来添加已有的文件到暂存盘
	+ use `git rm --cached 文件名`来删除添加到暂存盘的临时文件
5. 提交至本地库
	+ use `git commit -m "日志信息" 文件名`将文件添加至本地库中，bash会生成一段提示`[master (root-commit) *******]`这一串码就是当前的版本号
	+ 再次用`git status`查看项目信息时就会显示新的状态
	+ use `git reflog`查看日志信息和版本号，use `git log`查看详细信息
6. 修改文件
	+ 修改文件之后再次按照5的方法提交，就会看到文件修改情况
	+ 可以用`cat 文件名`查看文件
7. 版本穿梭
	+ use `git reflog`查看精简版本信息
	+ use `git log`查看详细版本信息
	+ use `git reset --hard ******(版本号)`穿梭至版本
## 4. Git分支
1. 分支指并行推进项目的过程，可以各个部分独立工作，各个部分互不影响，提高效率
2. 分支的操作
	+ use `git branch`查看当前分支
	+ use `git branch -v`查看当前的分支情况
	+ use `git branch 分支名称`添加新的分支
	+ use `git checkout 分支名`或`git switch 分支名`(*git2.23版本之后支持使用switch等新命令代替checkout的部分功能*)切换至分支
	+ use `git merge 分支名1`把目标分支（分支名1）的内容合并到当前所在的分支上
	+ 当我们合并时遇到代码冲突的问题时将采取以下的几步操作来merge项目
		+ 如果在B1和B2产生了冲突的代码，那么我们先在B1中直接`git merge B2`
		+ 随后分支名变化为B1|MERGING，我们再次打开编辑器
		+ 编辑器会展示两块东西不同的地方，我们做比对和采纳丢弃
		+ 完成后在B1中`git add 文件名`
		+ 随后`git commit -m "日志"`即可完成合并，注意这里的提交不需要加文件名，加上文件名则会报错
		+ 注意merge操作只会改动当前所在分支的文件，对其他的分支都没有影响
## 5. Git的连接功能（GitHub）
1. 团队协作
	+ 队内协作，使用远程库供大家使用，一号大哥push上去初始文件到远程库，二号大哥clone下来到自己的本地库，修完之后二号大哥再push上去到远程库，一号大哥看到了再从上面pull下来到自己的本地库让自己的项目和远程库的一致。**注意，pull和clone的区别就在于是把整个项目全部拉下来还是只把修改的部分拉去下来更新自己本地库的项目**
	+ 队间协作，首先两个团队都有远程库，A队希望B队对自己的项目修改，那么A就把自己的A远程库提供给B，让B把项目Fork（叉过来）到自己的B远程库，然后B从B远程库clone下来改完再push上去，同时发给A一个pull request让A把改好的拿过去，A受到后先审核，通过后即可把代码merge到自己的远程库了，合并完后，A队的成员就都可以pull自己远程库中已经被B改好的代码。
2. GitHub的基本使用
	1. 账号注册，这步不做详细解释
	2. 仓库创建，创建仓库时可以输入*仓库名称*、*仓库描述*，选择仓库*共有*or*私有*，选择是否要添加其他文件包括*readme*、*.gitignore*、*license*，这里的三个文件可以都选择没有，想拥有的话GitHub也提供了一些模板可以使用
	3. 为本地库提供GitHub远程库
		+ HTTPS协议篇：复制仓库HTTPS协议的地址
		+ 在本地库中Git Bash，use `git remote -v`查看别名，use `git remote add 别名 HTTPS地址`添加别名，**注意，这一步完成后会给这个地址创建两个别名，分别是fetch和push，分别代表拉取和推送**
		+ use `git push 远程库别名 要推送的分支名`推送项目到远程库上，**注意这一步以及后面几步操作都可能会因为网络原因报fatal错误，连接不上，请多试几次或者可以试试执行`git config --global --unset http.proxy 
		git config --global --unset https.proxy
		`
		有可能有用**
		+ use `git pull 远程库名 要拉取到的分支名`拉取项目到当前分支，拉取会自动帮你提交更改到本地库
		+ use `git clone 远程库的https地址`他会把整个项目都克隆下来到当前目录下，并且执行三个操作*1、下载整个项目的当前内容	2、初始化本地库	3、把克隆地址起一个叫origin的别名*
## 6. GitHub SSH
1. 在`C:/用户/当前用户`目录下打开Git Bash执行`ssh-keygen -t rsa -C 你的邮箱地址`然后按4次回车
2. 生成结束后`cd .ssh`，`cat id_rsa.pub`打开公钥，复制公钥的所有内容
3. 在GitHub网站进入个人设置（点击右上角头像，下面的settings），选择`SSH and GPG keys`
4. 在SSH keys选项中新建一个ssh起名，粘贴你的公钥并生成
5. 然后就可以使用项目的SSH来操作了