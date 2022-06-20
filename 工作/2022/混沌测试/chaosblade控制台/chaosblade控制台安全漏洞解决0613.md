# 升级记录

## 2022-06-13 版本1.0.1 uaa版本

### spring-aop

问题组件：

org.springframework:spring-aop 5.3.19 超危

依赖关系分析：

从依赖关系分析可以知道，是由于引入了spring-boot导致的，之前spring-boot版本为2.5.13。

```
[INFO] \- org.springframework.boot:spring-boot-starter:jar:2.5.13:compile
[INFO]    \- org.springframework.boot:spring-boot:jar:2.5.13:compile
[INFO]       \- org.springframework:spring-context:jar:5.3.19:compile
[INFO]          \- org.springframework:spring-aop:jar:5.3.19:compile
```

解决方案：

将org.springframework.boot:spring-boot-starter升级为2.5.14后，spring-aop版本自动升级为5.3.20。最外层pom下修改即可。

### mybatis-plus-core

问题组件：

com.baomidou:mybatis-plus-core 3.5.1 超危

依赖关系分析：

```
//执行命令
mvn dependency:tree -Dverbose -Dincludes=com.baomidou:mybatis-plus-core
//依赖关系
[INFO]    \- com.baomidou:mybatis-plus-boot-starter:jar:3.5.1:compile
[INFO]       \- com.baomidou:mybatis-plus:jar:3.5.1:compile
[INFO]          \- com.baomidou:mybatis-plus-extension:jar:3.5.1:compile
[INFO]             \- com.baomidou:mybatis-plus-core:jar:3.5.1:compile
```

来源于版本com.baomidou:mybatis-plus-boot-starter。

解决方案：

最外层pom下修改，升级com.baomidou:mybatis-plus-boot-starter为3.5.2版本。

### pagehelper

问题组件：

com.github.pagehelper:pagehelper 5.1.10 超危

依赖关系分析：

```
//依赖关系
[INFO] \- com.alibaba.chaosblade:chaosblade-box-dao:jar:0.4.2:compile
[INFO]    \- com.github.pagehelper:pagehelper-spring-boot-starter:jar:1.2.12:compile
[INFO]       \- com.github.pagehelper:pagehelper:jar:5.1.10:compile
```

问题解决：

依赖关系来源于最外层pom的引用。升级为1.4.2版本。

### kotlin-stdlib

问题组件：

org.jetbrains.kotlin:kotlin-stdlib 1.5.32

依赖关系分析：

升级com.baomidou:mybatis-plus-core，从3.5.1升级为3.5.2后，其新引入组件引起了安全漏洞。

```
[INFO] com.alibaba.chaosblade:chaosblade-box-dao:jar:0.4.2
[INFO] \- com.baomidou:mybatis-plus-boot-starter:jar:3.5.2:compile
[INFO]    \- com.baomidou:mybatis-plus:jar:3.5.2:compile
[INFO]       \- org.jetbrains.kotlin:kotlin-stdlib-jdk8:jar:1.5.32:compile
[INFO]          \- org.jetbrains.kotlin:kotlin-stdlib:jar:1.5.32:compile
```

问题解决：

从idea直接看依赖的第三方jar包内容，可以发现所有org.jetbrains.kotlin组件需要一起将版本升级为1.7.0。

```
            //父pom下修改如下
            <dependency>
                <groupId>com.baomidou</groupId>
                <artifactId>mybatis-plus-boot-starter</artifactId>
                <version>3.5.2</version>
                <exclusions>
                    <exclusion>
                        <groupId>org.jetbrains.kotlin</groupId>
                        <artifactId>kotlin-stdlib-jdk8</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>org.jetbrains.kotlin</groupId>
                        <artifactId>kotlin-stdlib-jdk7</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>org.jetbrains.kotlin</groupId>
                        <artifactId>kotlin-stdlib-common</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>org.jetbrains.kotlin</groupId>
                        <artifactId>kotlin-stdlib</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>

            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-jdk8</artifactId>
                <version>1.7.0</version>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-jdk7</artifactId>
                <version>1.7.0</version>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-common</artifactId>
                <version>1.7.0</version>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib</artifactId>
                <version>1.7.0</version>
            </dependency>
            
            //chaosblade-box-dao是唯一使用mybatis组件的module，在其pom中添加引用方式
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-jdk8</artifactId>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-jdk7</artifactId>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib-common</artifactId>
            </dependency>
            <dependency>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-stdlib</artifactId>
            </dependency>
```



### snakeyaml

问题组件：

org.yaml:snakeyaml 1.29

依赖关系分析：

无

问题解决：

内网将1.29更新至最新1.30。

```
        <dependency>
            <groupId>org.yaml</groupId>
            <artifactId>snakeyaml</artifactId>
            <version>1.30</version>
        </dependency>
```

