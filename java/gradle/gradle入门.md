# brew

一键安装brew
```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

查看安装情况

```
brew list 
brew list maven
//安装地址
/opt/homebrew/Cellar/

brew install maven
brew unintsall maven

brew info maven
```



# gradle

指定版本

```
brew search gradle
brew install gradle@6
//可执行文件路径
/opt/homebrew/Cellar/gradle@6/6.9.1/bin
//添加至 /etc/profile 中
export PATH=$PATH:/opt/homebrew/Cellar/gradle@6/6.9.1/bin
//验证gradle功能
gradle -v
```

Spring代码下载

```
git clone git@github.com:spring-projects/spring-framework.git
```

Java17安装

```
brew install openjdk
//默认安装路径
/opt/homebrew/Cellar/openjdk/17.0.2

echo $PATH
//默认path
PATH=/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin
//修改文件
vim /etc/profile
//叠加path
PATH=$PATH:/opt/homebrew/Cellar/gradle@6/6.9.1/bin:/opt/homebrew/Cellar/openjdk/17.0.2/bin
source /etc/profile

//验证
gradle -v //6
java -version //17
```

