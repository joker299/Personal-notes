# git使用方法

### 一：安装

#### Linux系统：

首先，你可以试着输入`git`，看看系统有没有安装Git：

```
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。

如果你碰巧用Debian或Ubuntu Linux，通过一条`sudo apt-get install git`就可以直接完成Git的安装，非常简单。

老一点的Debian或Ubuntu Linux，要把命令改为`sudo apt-get install git-core`，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫`git-core`了。由于Git名气实在太大，后来就把GNU Interactive Tools改成`gnuit`，`git-core`正式改为`git`。

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：`./config`，`make`，`sudo make install`这几个命令安装就好了。

#### Mac OS X系统：

如果你正在使用Mac做开发，有两种安装Git的方法。

一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。

第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！

#### Windows系统：

在Windows上使用Git，可以从Git官网直接下载 https://git-scm.com/downloads，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

### 二：git命令操作

#### 第一步：创建本地仓库

创建一个版本库非常简单，首先，选择一个合适的地方，创建一个文件夹，并在文件夹中右键菜单中选择用gitBush打开：

```
$ git init
```

或者直接用命令创建，在windows开始菜单中打开GitBush：

```
$ mkdir runoob //创建runoob文件夹
$ cd runoob/   //进入到文件夹根目录中
$ git init     //初始化git仓库
```

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

**注:**如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

#### 第二步：创建远程仓库

#### 提交文件

|               指令                |                             说明                             |
| :-------------------------------: | :----------------------------------------------------------: |
|          git add 文件名           |               将文件添加到缓存存区(git管理区)                |
|            git add *.c            |                 将以.c结尾的文件提交到缓存区                 |
|             git add .             | 除了能够判断出当前目录（包括其子目录）所有被修改或者已删除的文档，还能判断用户所添加的新文档，并将其信息追加到索引中。 |
|     git commit -m "注释内容"      |                   将被追踪的文件提交到仓库                   |
| git commit -a -m "提交的描述信息" | -a 选项可只将所有被修改或者已删除的且已经被git管理的文档提交倒仓库中。 |
|            git status             |               查看是否还有文件未提交，详细显示               |
|           git status -s           |               查看是否还有文件未提交，简短显示               |
|          git diff 文件名          |                      查看修改的详细内容                      |
|             git diff              |                      查看尚未缓存的改动                      |
|         git diff --cached         |                       查看已缓存的改动                       |
|          git diff --stat          |                       显示摘要而非整个                       |
|      git reset HEAD "文件名"      |                     用于取消已缓存的内容                     |

#### 下载文件

|                             指令                             |                   描述                   |
| :----------------------------------------------------------: | :--------------------------------------: |
|                    git pull origin master                    |            从远程仓库拉取文件            |
| git fetch origin(别名)  分支名(可选项，不填写则拉取全部，填写则拉取对应分支) |             拉取远程分支命令             |
|    git remote add origin(这个远程仓库的别名) 远程仓库路径    |            和远程仓库建立连接            |
|                       git clone <repo>                       | 从现有的git仓库中拷贝项目，repo为git仓库 |
|                 git clone <repo> <directory>                 |   拷贝到指定目录，directory为本地目录    |



#### 版本回退

|           指令            |                             描述                             |
| :-----------------------: | :----------------------------------------------------------: |
|          git log          |                   显示所有提交过的版本信息                   |
| git log --pretty=oneline  |                       将日志显示在一行                       |
|        git reflog         | 查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作） |
|  git reset --hard HEAD^   |          退回到上个版本内容 有个 ^ 就代表上一个版本          |
| git reset --hard HEAD~100 |                     退回到一百个版本之前                     |
|  git reset --hard 版本号  |                        退回到目标版本                        |

#### **Git撤销修改和删除文件操作**

如果只是简单地从工作目录中手工删除文件，运行 **git status** 时就会在 **Changes not staged for commit** 的提示。

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除，然后提交。可以用以下命令完成此项工作：

```
git rm <file>
```

如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 **-f**

```
git rm -f <file>
```

如果把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 **--cached** 选项即可：

```
git rm --cached <file>
```

如果后面跟的是一个目录做为参数，则会递归删除整个目录中的所有子目录和文件：

```
git rm –r *   //*表示所有文件，也可以替换成目录文件
```

git mv 命令用于移动或重命名一个文件、目录、软连接。

```
 git mv README  README.md  //将README，改为README.md文件
```



|               指令                |                             描述                             |
| :-------------------------------: | :----------------------------------------------------------: |
|      git checkout -- 文件名       | 把readme.txt文件在工作区做的修改全部撤销	1.自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。	2.已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。 |
|             rm 文件名             |                 删除文件需要在commit提交修改                 |
| find . -name ".git"\|xargs rm -Rf |                      恢复删除掉的文件库                      |

#### 上传到gitHub

```
ssh-keygen -t rsa -C "yourmail@youremail.com.cn" //生成SSH密钥

github 新建仓库 

github 配置SSH keys信息 把公钥id_rsa.pub的内容添加到 GitHub
```

```
git remote add origin git@github.com:GitHub账号名/git仓库名.git //关联远程仓库 
```

```
git push origin 本地分支名:远程仓库分支名 //上传远程仓库
```

```
# 由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，
git push -u origin master
#下次再从本地库上传内容的时候只需下面这样就可以了：
git push  origin master
```

#### 分支

|          指令          |         描述         |
| :--------------------: | :------------------: |
|       git branch       |       查看分支       |
|   git branch <name>    |       创建分支       |
|  git checkout <name>   |       切换分支       |
| git checkout -b <name> |    创建+切换分支     |
|    git merge <name>    | 合并某分支到当前分支 |
|  git branch -d <name>  |       删除分支       |

