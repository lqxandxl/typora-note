# 安装步骤
## 具备ssh命令

## 生成密钥
```
ssh-keygen -t rsa
//生成路径，一路回车
/Users/liqixin/.ssh
```

一共两个文件
id_rsa和id_rsa.pub。

将id_rsa.pub内容复制到github 个人设置->ssh and gpg keys。

## 配置邮箱和用户名

```
git config --global user.name "liqixin"
git config --global user.email "liqixin@bupt.cn"
```

## 使用ssh拉取项目

```
git clone git@github.com:lqxandxl/typora-note.git

//使用本地sourcetree提交代码，或者使用命令行
git push origin master
```

# 操作命令

## 基本操作

```
//查看分支
git branch

//删除分支
git branch -D 分支名

//合并分支，先切换到master分支，然后进行合并
git checkout master
git merge 分支名

//创建分支 由master开始创建
git checkout -b 分支名

//推送
git push origin 分支名

//删除远程分支
git push origin --delete 分支名
```

## 回退

```
git log
git reset --hard commitid
git push -f
```

软回退，像注释写错了，可以用这种办法修改。

```
git reset --soft HEAD~1
git commit -m “info”
git push -f origin feature_v1.0.0
```

## gitignore

.gitignore 一般忽略内容如下

```
target/*
*/target/*
**/target/**
*/.idea/*
.idea/*
*.class
*.iml
*.jar
*.log
```

ignore 生效

```
git rm -r --cached .
git add .
git commit -m "update .gitignore"
git push origin master
```

## 打标签

```
git tag feature_v1.0.0
git push origin --tags
```

git clone整个项目后，

```
//列出所有标签
git tag -l
//切换到指定标签，及该标签所在分支上
git checkout tags/<tag_name> 
//更好的办法,切换到指定标签后，新建分支
git checkout tags/<tag_name> -b <branch_name>

//删除tag
git tag -d <tag_name>
git push origin :refs/tags/<tag_name>
```



# 错误解决

错误现象：

refusing to merge unrelated histories

解决方式：

```
git pull origin gh-pages --allow-unrelated-histories
git push origin gh-pages
```



错误现象：

pre-commit hook failed。

错误原因：

git提交进行代码检查。

解决方式：

最直观的做法是取消钩子。

```
//或者通过界面取消钩子后提交即可
git commit --no-verify
```

