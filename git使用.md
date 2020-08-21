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

在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

### 二：git命令操作

#### 创建本地仓库

创建一个版本库非常简单，首先，选择一个合适的地方，创建一个文件夹，并在文件夹中右键菜单中选择用gitBush打开：

```
$ git init
```

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

**注:**如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

#### 提交文件

|               指令                |                             说明                             |
| :-------------------------------: | :----------------------------------------------------------: |
|          git add 文件名           |                将文件添加到暂存区(git管理区)                 |
|    git commit -m "注释的内容"     |                       将文件提交到仓库                       |
| git commit -a -m "提交的描述信息" | -a 选项可只将所有被修改或者已删除的且已经被git管理的文档提交倒仓库中。 |
|             git add .             | 除了能够判断出当前目录（包括其子目录）所有被修改或者已删除的文档，还能判断用户所添加的新文档，并将其信息追加到索引中。 |
|            git status             |                    查看是否还有文件未提交                    |
|          git diff 文件名          |                      查看修改的详细内容                      |

#### 版本回退

|           指令            |                             描述                             |
| :-----------------------: | :----------------------------------------------------------: |
|          git log          |                   显示所有提交过的版本信息                   |
| git log --pretty=oneline  |                       将日志显示在一行                       |
|        git reflog         | 查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作） |
|  git reset --hard HEAD^   |           退回到上个版本内容 有个^就代表上一个版本           |
| git reset --hard HEAD~100 |                     退回到一百个版本之前                     |
|  git reset --hard 版本号  |                        退回到目标版本                        |

#### **Git撤销修改和删除文件操作**

|               指令                |                             描述                             |
| :-------------------------------: | :----------------------------------------------------------: |
|      git checkout -- 文件名       | 把readme.txt文件在工作区做的修改全部撤销	1.自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。	2.已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。 |
|             rm 文件名             |                 删除文件需要在commit提交修改                 |
| find . -name ".git"\|xargs rm -Rf |                      恢复删除掉的文件库                      |

#### 上传到github

$ ssh-keygen -t rsa //生成SSH密钥

github 配置SSH keys信息 把公钥id_rsa.pub的内容添加到 GitHub

github 新建仓	库

git remote add origin git@github.com:Sinmeow/test.git  //关联远程仓库 

git push origin 本地分支名:远程仓库分支名 //上传远程仓库

#### 分支

|          指令          |         描述         |
| :--------------------: | :------------------: |
|       git branch       |       查看分支       |
|   git branch <name>    |       创建分支       |
|  git checkout <name>   |       切换分支       |
| git checkout -b <name> |    创建+切换分支     |
|    git merge <name>    | 合并某分支到当前分支 |
|  git branch -d <name>  |       删除分支       |

