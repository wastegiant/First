# Git

**cmd控制台方法**

1. 方向键 ↑ 补全上一条指令
2. Tab键 补全联想指令



## Git快照

- 提交git快照 （对照修改后的打包新版本）

```
$ git commit
```



## Git Branch

- 新建git提交分支

<img src="D:\Program\picture_typora\image-20221014084200044.png" style:zoom=60%>



```basic
$ git branch <branch_name>
$ git checkout <branch_name> || $ git switch <branch_name>
//新版本采用get switch切换分支
$ git checkout -b bugFix //创建bugFix分支并指向
```



## 合并Git分支

### Git merge

- 合并git branch分支

```
git branch bugFix
git commit
git merge main //将两条分支合并，将旧的分支（main）合并到最新修改的一条主线(bugFix)中
```



### Git rebase

- 合并git分支(复制节点)

```bash
git branch -b bugFix //新建并指向bugFix分支结点
git commit
git checkout main
git commit
git checkout bugFix
git rebase main //将当前指向的分支(bugFix)合并到最新修改的分支(main)

```



## 移动Git指向

> 让当前head指向不指向分支名字，而是指向当前结点

### HEAD

![image-20221015214731486](picture_typora/Git/image-20221015214731486.png)

### 相对引用

```bash
git checkout C4^ //HEAD指向C4结点的父结点

git branch -f main c6  //强制修改main分支到c6节点

git branch -f  main HEAD~4 //强制修改main分支到HEAD的第4个父节点位置 
```



## 撤销更改/回退

```bash
//执行操作前必须checkout "操作分支"指向对应操作分支

git reset main^  //将main回退指向上一节点，仅对本地仓库有效

git revert HEAD  //生成HEAD的新一更改节点，可推送至远程仓库共享更改

```



## 修改提交树

<img src="picture_typora/Git/image-20221018092326953.png" style="zoom:60%"/>

```bash
git cherry-pick c2 c4  //将c2 c4节点复制到mian指向提交树

git reabase -i c2 //弹出c2节点后的节点，选择顺序与是否pick/omit
```





## 远程仓库操作

> 在本地创建一个远程仓库的拷贝（例如从GitHub.com）



### 创建远程仓库

```bash
git clone //创建远程仓库

//远程仓库命名格式
<remote name> / <branch name> 仓库名字/分支名字
```



### 远程分支

- 远程分支反映了远程仓库在你 最后一次与它通信时 的状态

- 远程分支有一个特别的属性，在你检出时自动进入分离 HEAD 状态。Git 这么做是出于不能直接在这些分支上进行操作的原因, 你必须在别的地方完成你的工作, （更新了远程分支之后）再用远程分享你的工作成果。

```bash
git checkout o/main
git commit
```



### 拉取远程仓库数据 git fetch

<img src="picture_typora/Git/image-20221018170747413.png" alt="image-20221018170747413" style="zoom:70%;" />





## 查看修改

- 要明白这3个概念，工作区（**working tree**），暂存区（**index /stage**），本地仓库（**repository**）
- git跟不同的参数，比较不同的区间的版本。

1. git diff：是查看working tree与index的差别的。
2. git diff --cached：是查看index与repository的差别的。
3. git diff HEAD：是查看working tree和repository的差别的。其中：HEAD代表的是最近的一次commit的信息。

 **综上所述：git diff 后面跟文件名称是是查看工作区（\**working tree\**）与暂存区（\**index\**）的差别的。**





# Github



## 生成密钥

```bash
$ ssh-keygen -t rsa -C "youremail@com" //生成.ssh文件 其中包含id_rsa与id_rsa.pub文件，前者为私钥，后者为公钥
```



## 查看密钥

```bash
//用cat打开id_rsa.pub文件
$ cat id_rsa.pub //获取到完整公钥
```



## 添加到GitHub

**个人-> SSH -> Add SSH key / New SSH key**

<img src="picture_typora/Git/image-20221030204220541.png" style="zoom:90%;" />



## 将GitHub仓库克隆到本地

1. 打开本地文档，Git bash here控制台
2. 执行"git clone "github.project_adress" "

<img src="picture_typora/Git/image-20221030210138019.png" alt="image-20221030210138019" style="zoom:80%;" />





## 关联本地仓库与远程仓库

> 通过情况下，一个本Git仓库对于一个远程仓库，每次pull和push仅涉及本地仓库和该远程仓库的同步

```bash
$ git remote add origin git@github.com:wastegiant/project.git //关联本地仓库与wastegiant下的project仓库

$ git remote -v //仓库目前关联的远程仓库信息

$ git remote rm origin //删除关联的仓库
```





## ！提交修改到远程仓库

1. ```bash
   //先add .而不是add
   $ git add .
   
   //commit提交，并且需要进行-m说明[进入vim页面后按 :wq 退出]
   $ git commit -m #第一次提交
   
   此时才能生成maste分支
   
   //采用add提交修改时，注意当前是否在目标文件路径下，才能正确找到要提交的文件
   $ git add "one.md" //可以采用ls查看当前路劲下的文件，是否有one.md
   
   //提交当前修改到远程仓库
   $ git push origin main //此处的main是最新修改分支，之前的add、commit操作也是基于main分支的
   
   
   ```

   
