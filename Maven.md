# Maven

## 传统项目管理问题

- jar包不统一，jar包不兼容

  但我们在做项目的时候，会用到特别多的jar包，大部分为大家都在用的技术，如mybatis、JUnit，log4j，还有一些可能是同事写好的jar包。此时出现的问题就会有：

  突然我的mybatis升级了，但它下载需要5.0版本的JUnit，但项目的JUnit没有去升级，就会出现严重问题。

- 工程升级维护过程操作繁琐

  一个项目我们在windows上写好了，需要发布给其他人用。是必须要在Linux服务器上进行编译，打包，测试、、、等等的工作的。但是哦，windows上的代码和Linux上的可不一样，两者的写法很多不同，而且Linux上可没有IDEA这样的工具，所有会引起超级多不好解决的问题

- 还有很多很多其他的.........

## 使用Maven的好处

Maven是专门用于管理和构建Java项目的工具，它的主要功能有：

* 提供了**一套标准化的项目结构**，，所有的IDE使用Maven构建的项目完全一样，所以IDE创建的Maven项目可以通用。
* 提供了**一套标准化的构建流程（编译，测试，打包，发布……）**，Maven提供了一套简单的命令来完成项目构建。
* 提供了**一套新的依赖管理机制**，管理你项目所依赖的第三方资源（jar包、插件）。如之前我们项目中需要使用JDBC和Druid的话，就需要去网上下载对应的依赖包，复制到项目中，还要将jar包加入工作环境这一系列的操作。而Maven使用标准的坐标 配置来管理各种依赖，只需要简单的配置就可以了，其他的下载复制导入，Maven都会帮我们做了。

这里说的项目暂时我们就认为是，工程下的模块。其实工程也可以变成Maven项目，这样的话，该工程下的模块（也是Maven）就可以直接使用这个工程的依赖，这样有一个父子关系，后面到了高级阶段再细说。

**标准化的项目结构：**

项目结构我们都知道，每一个开发工具（IDE）都有自己不同的项目结构，它们互相之间不通用。我再eclipse中创建的目录，无法在idea中进行使用，这就造成了很大的不方便，如下图:前两个是以后开发经常使用的开发工具。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726153521381.png" alt="image-20210726153521381" style="zoom:80%;" />

而Maven提供了一套标准化的项目结构，所有的IDE使用Maven构建的项目完全一样，所以IDE创建的Maven项目可以通用。如下图就是Web项目结构。java项目的话就少了一个webapp包

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726153815028.png" alt="image-20210726153815028" style="zoom:80%;" />

**标准化的构建流程：**

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726154144488.png" alt="image-20210726154144488" style="zoom:80%;" />

如上图所示我们开发了一套系统，代码需要进行编译、测试、打包、发布，这些操作如果需要反复进行就显得特别麻烦，而Maven提供了一套简单的命令来完成项目构建。其中打包就是生成jar包，里面存放我们的字节码文件（.class文件）

**依赖管理：**

依赖管理其实就是管理你项目所依赖的第三方资源（jar包、插件）。如之前我们项目中需要使用JDBC和Druid的话，就需要去网上下载对应的依赖包（当前之前是老师已经下载好提供给大家了），复制到项目中，还要将jar包加入工作环境这一系列的操作。如下图所示

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726154753631.png" alt="image-20210726154753631" style="zoom:80%;" />

而Maven使用标准的坐标 配置来管理各种依赖，只需要简单的配置就可以完成依赖管理。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726154922337.png" alt="image-20210726154922337" style="zoom:80%;" />

如上图右边所示就是mysql驱动包的坐标，在项目中只需要写这段配置，其他都不需要我们担心，Maven都帮我们进行操作了，他会自己去我们设置的网站下

市面上有很多构建工具，而Maven依旧还是主流构建工具，如下图是常用构建工具的使用占比

![image-20210726155212733](https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726155212733.png)

## 2. Maven简介

> Apache Maven 是一个项目管理和构建工具，它基于项目对象模型(POM)的概念，**通过一小段描述信息来管理项目的构建、报告和文档。**
>
> 官网 ：http://maven.apache.org/ 

通过上面的描述大家只需要知道Maven是一个工具即可。Apache 是一个开源组织，将来我们会学习很多Apache提供的项目。

**他是一个单独的工具/软件，与Java是单独分开的东西哦**



### 2.1 Maven模型

* 项目对象模型 (Project Object Model)
* 依赖管理模型(Dependency)
* 插件(Plugin)

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129133847498.png" alt="image-20220129133847498" style="zoom:80%;" />

**插件(Plugin)**如上图所示就是Maven的模型，而我们先看紫色框框起来的部分，他就是用来完成 `标准化构建流程` 。如我们需要编译，Maven提供了一个编译插件供我们使用，我们需要打包，Maven就提供了一个打包插件提供我们使用等。最终会有很多插件（Maven已经写好了）来帮我们做好项目最终需要的东西。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128231341598.png" alt="image-20220128231341598" style="zoom:80%;" />

**模型** 然后上图中紫色框起来的部分，项目对象模型就是将我们自己这个项目抽象成一个对象模型，有自己专属的坐标，如下图所示是一个Maven项目：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128231409802.png" alt="image-20220128231409802" style="zoom:80%;" />

依赖管理模型则是使用**坐标来描述当前项目依赖哪儿些第三方jar包**，如下图所示

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128231510075.png" alt="image-20220128231510075" style="zoom:80%;" />

两者是一个双向箭头的含义：项目对象管理需要jar，这个工作依赖管理帮我们做，而我们自己这个项目对象模型也可以被当成一个资源，去让别人去使用。

最后，Maven模型图中还有一部分是仓库。如何理解仓库呢？

### 2.2 仓库

大家想想这样的场景，我们创建Maven项目，在项目中使用坐标来指定项目的依赖，那么依赖的jar包到底存储在什么地方呢？其实依赖jar包是存储在我们的本地仓库中。而项目运行时从本地仓库中拿需要的依赖jar包。

**仓库分类：**

* 本地仓库：自己计算机上的一个目录

* 中央仓库：由Maven团队维护的全球唯一的仓库

  * 地址： https://repo1.maven.org/maven2/

* 远程仓库(私服)：一般由公司团队搭建的私有仓库。我们一般用阿里巴巴的仓库，中央仓库太慢了


当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包：

* 如果有，则在项目直接引用;

* 如果没有，则去中央仓库中下载对应的jar包到本地仓库。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726162605394.png" alt="image-20210726162605394" style="zoom:70%;" />

如果还可以搭建远程仓库，将来jar包的查找顺序则变为：

> 本地仓库 --> 远程仓库--> 中央仓库

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726162815045.png" alt="image-20210726162815045" style="zoom:70%;" />

### 2.3 坐标

* Maven 中的坐标是**仓库里面资源的唯一标识**
* **我们使用坐标来定义项目或引入项目中需要的依赖**

**Maven 坐标主要组成**

* **groupId：**定义当前Maven项目隶属组织名称（通常是域名反写，例如com.itheima）
* **artifactId：**定义当前Maven项目名称（通常是模块名称，例如 order-service）
* **version：**定义当前项目版本号，自己开发使用快照版本，需要发布的时候再用完整版

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128232945844.png" alt="image-20220128232945844" style="zoom:67%;" />

==注意：==

* 上面所说的资源可以是插件、依赖、当前项目。
* 我们的项目如果被其他的项目依赖时，也是需要坐标来引入的。我们在创建Maven项目的时候不就已经写好了我们当前项目的坐标嘛。

### 2.4 Maven的安装—MAC

**他是一个单独的工具/软件，与Java是单独分开的东西哦**

官网下载二进制压缩包、开箱即用，然后配置环境变量、配置本地仓库路径和私服仓库路径，最后IDEA绑定Maven设置即可使用了



**1、打开Maven的官网下载安装；**

[Maven – Download Apache Maven](https://maven.apache.org/download.cgi)

<img src="images/image-20230621192442540-17201610580032.png" alt="image-20230621192442540" style="zoom: 50%;" />

> Binary是可执行版本，已经编译好可以直接使用。
> Source是源代码版本，需要自己编译成可执行软件才可使用。

> tar.gz和zip两种压缩格式,其实这两个压缩文件里面包含的内容是同样的,只是压缩格式不同
> tar.gz格式的文件比zip文件小很多,用于unix操作系统。
> zip格式用于Windows操作系统,但在Windows系统使用WinRar工具一样能够解压缩tar.gz格式

安装解压完了之后会有一个maven的文件夹，其中bin为可执行文件。

<img src="images/image-20230621192601248-17201610580031.png" alt="image-20230621192601248" style="zoom:50%;" />

<img src="images/image-20240705141622221.png" alt="image-20240705141622221" style="zoom:80%;" />



**2、添加maven的bin文件目录到环境变量里面去；**

 1. 进入到当前用户的home目录

    ```shell
    cd ~
    ```

 2. 创建.bash_profile（如果已经存在就不用创建了）

    ```sh
    touch .bash_profile
    ```

 3. 编辑该文件，加上maven的bin的环境变量

    ```sh
    vim ~/.bash_profile 
    # 加入下面一行（引号内容按照自己的maven安装路径修改）
    export PATH=$PATH:"/Users/zhoudas/Desktop/Java/apache-maven-3.9.2/bin"
    ```

 4. 更新环境变量配置文件；

    ```sh
     source ~/.bash_profile
    ```

 5. 检查是否配置成功

    ```sh
    mvn -v 
    ```

    <img src="images/image-20230621193152283-17201610580033.png" alt="image-20230621193152283" style="zoom:50%;" />

**3、配置本地仓库+私服仓库**

​	其实就是修改conf里面的setting.xml配置文件内容。如果公司有的话，直接覆盖这个配置文件就行了。

​	<img src="images/image-20240705141725814.png" alt="image-20240705141725814" style="zoom:80%;" />

​	1、在E:\Tools\Maven\路径下新建maven-repository文件夹，用作maven的本地库。

<img src="images/image-20240705142318499.png" alt="image-20240705142318499" style="zoom:80%;" />

​	2、在路径E:\Tools\Maven\apache-maven-3.8.1\conf下找到settings.xml文件

<img src="images/image-20240705142255542.png" alt="image-20240705142255542" style="zoom:80%;" />

​	3、找到节点localRepository，在注释外添加 

- ```java
  <localRepository>E:\Tools\Maven\maven-repository</localRepository>
  ```

  <img src="images/image-20240705142038405.png" alt="image-20240705142038405" style="zoom:80%;" />



​	4、配置私服仓库，找到mirrors节点

<img src="images/image-20240705142148168.png" alt="image-20240705142148168" style="zoom:80%;" />



### 2.5 Win安装

也是分为五步步、除了环境变量配置不用外，其他的都一样。Win中环境变量均采用 **Path+XXX_HOME**的形式。



**补充环境变量注意点：**

Maven是用java写的，它是需要配置Java的运行环境的，这个是在bin下面的mvn.cmd里面，打开你会发现这些东西：

- 也就是说，我们前面配置的Java环境变量，一定要起名规范哦，不然Maven会无法识别。
- Maven的环境变量起码也是要规范！！！

![img](images/wps1.jpg) 

![img](images/wps2.jpg) 







### 2.5 Maven的基本使用

#### 2.5.1 Maven构建项目

> * compile ：编译
>
> * clean：清理
>
> * test：测试
>
> * package：打包
>
> * install：安装

**环境准备：**

提供了一个Maven构建的项目，项目结构如下：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726170404545.png" alt="image-20210726170404545" style="zoom: 50%;" />

而我们使用上面命令需要在磁盘上进入到项目的 `pom.xml` 目录下，打开命令提示符

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726170549907.png" alt="image-20210726170549907" style="zoom:70%;" />

**编译命令演示：**

```java
mvn compile 
```

仅仅对main目录下面的文件进行编译

执行上述命令可以看到：

* 从阿里云下载编译需要的插件的jar包，在本地仓库也能看到下载好的插件
* 在项目下会生成一个 `target` 目录

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726171047324.png" alt="image-20210726171047324" style="zoom:80%;" />

同时在项目下会出现一个 `target` 目录，编译后的字节码文件就放在该目录下。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726171346824.png" alt="image-20210726171346824" style="zoom:80%;" />

产生了三个文件。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129141808342.png" alt="image-20220129141808342" style="zoom:80%;" />

其中classes存放了，我们main写的类的字节码文件。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129142247266.png" alt="image-20220129142247266" style="zoom:67%;" />

**测试命令演示：**

```
mvn test  
```

==对test目录下的所有测试文件进行测试。==，会先进行编译，再测试，这是他的生命周期顺序。

该命令会执行所有的测试代码。执行上述命令效果如下

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726172343933.png" alt="image-20210726172343933" style="zoom:80%;" />

在编译的基础上，又产生了三个文件。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129142149342.png" alt="image-20220129142149342" style="zoom:80%;" />

其中，reports存放了测试的记录，test-classes存放test文件下的测试类的字节码文件。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129142337322.png" alt="image-20220129142337322" style="zoom:67%;" />



**清理命令演示：**

```
mvn clean
```

执行上述命令可以看到

* 从阿里云下载清理需要的插件jar包
* 删除项目下的 `target` 目录

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726171558786.png" alt="image-20210726171558786" style="zoom:80%;" />

**打包命令演示：**

```
mvn package
```

我们前面的JDBC啊，Druid啊，这两个jar包就是这样来的。我们这样打包了之后，其他人也就可以用我们的这个项目中的东西。里面存放的就是我们main目录下面的代码的字节码文件。

执行上述命令可以看到：

* 从阿里云下载打包需要的插件jar包
* 在项目的 `terget` 目录下有一个jar包（将当前项目打成的jar包）

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129142602230.png" alt="image-20220129142602230" style="zoom:67%;" />

打开这个jar包，我们发现，只打包我们的源程序哦，测试是不会打包的。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129142636371.png" alt="image-20220129142636371" style="zoom:67%;" />

**安装命令演示：**

```
mvn install
```

该命令会将当前项目打成jar包，并安装到本地仓库。执行完上述命令后到本地仓库查看结果如下：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128234536701.png" alt="image-20220128234536701" style="zoom:80%;" />

**问题解答：**

​		你会说，IDEA不也给我们编译运行了吗，那为什么还要Maven呢，

​		首先，IDEA没有打包；其次，IDEA做完编译完，只是在本地计算机上面做的，最后我们的项目程序要传到Linux服务器上面去编译什么的，这就需要Maven来做。

#### 2.5.2 Maven生命周期

Maven 构建项目生命周期，描述的是一次构建过程经历经历了多少个事件

Maven 对项目构建的生命周期划分为3套：

* clean ：清理工作。
* default ：核心工作，例如编译，测试，打包，安装等。
* site ： 产生报告，发布站点等。这套声明周期一般不会使用。

**同一套生命周期内，执行后边的命令，前面的所有命令会自动执行。**例如默认（default）生命周期如下：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726173153576.png" alt="image-20210726173153576" style="zoom:80%;" />

当我们执行 `install`（安装）命令时，它会先执行 `compile`命令，再执行 `test ` 命令，再执行 `package` 命令，最后执行 `install` 命令。

当我们执行 `package` （打包）命令时，它会先执行 `compile` 命令，再执行 `test` 命令，最后执行 `package` 命令。

默认的生命周期也有对应的很多命令，其他的一般都不会使用，我们只关注常用的：

**default构建生命周期：**

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726173619353.png" alt="image-20210726173619353" style="zoom:80%;" />





## 3. IDEA使用Maven

### 3.1 创建Maven

回顾项目结构：Java项目和Web项目区别就在于 webapp那个目录的有无。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726153815028.png" alt="image-20210726153815028" style="zoom:80%;" />

#### 3.1.1 直接创建java项目

先创建空工程，后面工程都是以模块形式出现。

* 创建模块，选择Maven，点击Next

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129131853757.png" alt="image-20220129131853757" style="zoom:80%;" />

  

* 填写模块名称，坐标信息，点击finish，创建完成

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129131909265.png" alt="image-20220129131909265" style="zoom:80%;" />

  

  创建好的项目目录结构如下：pom文件的内容较少，只有最基本的

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129131926289.png" alt="image-20220129131926289" style="zoom:80%;" />

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129144126473.png" alt="image-20220129144126473" style="zoom:80%;" />

  

#### 3.1.2 模板创建java项目

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129143926274.png" alt="image-20220129143926274" style="zoom:80%;" />

项目结构目录如下：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129144235013.png" alt="image-20220129144235013" style="zoom:67%;" />

可见与，前面的区别挺大的，首先没有自己给我们创建resources目录，其次他自己还给我们写好了一个源码和测试类。

然后我们需要自己手动去创建目录，并且标注一下颜色。

打开Project Structure，工程结构，添加文件夹，并且标注颜色类型。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129144655207.png" alt="image-20220129144655207" style="zoom: 80%;" />

或者用下面这种方式

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220129144802250.png" alt="image-20220129144802250" style="zoom:80%;" />



#### 3.1.3 模板创建web项目

Web项目的结构分为:开发中的项目和开发完可以部署的Web项目,这两种项目的结构是不一样的，我们一个个来介绍下:

* **Maven Web项目结构: 开发中的项目**

  ![1627202865978](https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/1627202865978-164406993760131.png)

* **开发完成部署的Web项目**

  ![1627202903750](https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/1627202903750-164406993760132.png)

  * 开发项目通过执行Maven打包命令==package==,可以获取到部署的Web项目目录
  * 编译后的Java字节码文件和resources的资源文件，会被放到WEB-INF下的classes目录下
  * pom.xml中依赖坐标对应的jar包，会被放入WEB-INF下的lib目录下

1. **选择使用Web项目骨架**

   <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20230621174444316.png" alt="image-20230621174444316" style="zoom:80%;" />

   

2. 输入Maven项目坐标创建项目

   <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20230621174554375.png" alt="image-20230621174554375" style="zoom:80%;" />

3. 确认Maven相关的配置信息后，完成项目创建

   <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20230621174547274.png" alt="image-20230621174547274" style="zoom:67%;" />

4. 删除pom.xml和web.xml中多余内容，只留下面的这些内容，注意打包方式 jar和war的区别

   ![image-20220213211553302](https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220213211553302.png)

   <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220213211531451.png" alt="image-20220213211531451" style="zoom:80%;" />

5. 补齐Maven Web项目缺失的目录结构，默认没有java和resources目录，需要手动完成创建补齐，最终的目录结果如下

   ![](https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/1627228673162-164406993760238.png)

### 3.2 导入Maven项目

我们可以通过以下步骤进行项目的导入：

* 选择右侧Maven面板，点击 + 号

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726182702336.png" alt="image-20210726182702336" style="zoom:70%;" />

* 选中对应项目的pom.xml文件，双击即可

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726182648891.png" alt="image-20210726182648891" style="zoom:70%;" />

* 如果没有Maven面板，选择

  View --> Appearance --> Tool Window Bars

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726182634466.png" alt="image-20210726182634466" style="zoom:80%;" />

### 3.3 Maven生命周期操作

**第一种使用IDEA自己的界面，通过下图所示进行命令的操作：**

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726182902961.png" alt="image-20210726182902961" style="zoom:80%;" />

**第二种--配置 Maven-Helper 插件** 

* 选择 IDEA中 File --> Settings

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726192212026.png" alt="image-20210726192212026" style="zoom:80%;" />

* 选择 Plugins

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726192224914.png" alt="image-20210726192224914" style="zoom:80%;" />

* 搜索 Maven，选择第一个 Maven Helper，点击Install安装，弹出面板中点击Accept

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726192244567.png" alt="image-20210726192244567" style="zoom:80%;" />

* 重启 IDEA

安装完该插件后可以通过 选中项目右键进行相关命令操作，如下图所示：

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726192430371.png" alt="image-20210726192430371" style="zoom:80%;" />

### 3.4 依赖管理

#### 3.4.1 坐标导入

**使用坐标引入jar包的步骤：**

* 在项目的 pom.xml 中编写 <dependencies> 标签

* 在 <dependencies> 标签中 使用 <dependency> 引入坐标

* 定义坐标的 groupId，artifactId，version

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193105765.png" alt="image-20210726193105765" style="zoom:70%;" />

* 点击刷新按钮，使坐标生效

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193121384.png" alt="image-20210726193121384" style="zoom:60%;" />

>  注意：
>
>  * 具体的坐标我们可以到如下网站进行搜索
>  * https://mvnrepository.com/

#### 3.4.2 IDEA快捷导入

每次需要引入jar包，都去对应的网站进行搜索是比较麻烦的，接下来给大家介绍一种快捷引入坐标的方式

* 在 pom.xml 中 按 alt + insert，选择 Dependency

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193603724.png" alt="image-20210726193603724" style="zoom:60%;" />

* 在弹出的面板中搜索对应坐标，然后双击选中对应坐标

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193625229.png" alt="image-20210726193625229" style="zoom:60%;" />

* 点击刷新按钮，使坐标生效

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193121384-16433842976881.png" alt="image-20210726193121384" style="zoom:60%;" />

**自动导入设置：**

上面每次操作都需要点击刷新按钮，让引入的坐标生效。当然我们也可以通过设置让其自动完成

* 选择 IDEA中 File --> Settings

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193854438.png" alt="image-20210726193854438" style="zoom:60%;" />

* 在弹出的面板中找到 Build Tools

  <img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20210726193909276.png" alt="image-20210726193909276" style="zoom:80%;" />

* 选择 Any changes，点击 ok 即可生效

#### 3.4.3 依赖范围设置

通过设置坐标的依赖范围(scope)，可以设置 对应jar包的作用范围：==编译环境、测试环境、运行环境==。

如下图所示给 `junit` 依赖通过 `scope` 标签指定依赖的作用范围。 那么这个依赖就只能作用在测试环境，其他环境下不能使用。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220128234032698.png" alt="image-20220128234032698" style="zoom:80%;" />

 **`scope` 的所有取值如下：默认为compile**

这里说明一下：编译环境指的是main目录，测试环境指的是test目录，运行环境指的是项目跑起来的时候。

| **依赖范围** | 编译classpath | 测试classpath | 运行classpath | 例子              |
| ------------ | ------------- | ------------- | ------------- | ----------------- |
| **compile**  | Y             | Y             | Y             | logback           |
| **test**     | -             | Y             | -             | Junit             |
| **provided** | Y             | Y             | -             | servlet-api       |
| **runtime**  | -             | Y             | Y             | jdbc驱动          |
| **system**   | Y             | Y             | -             | 存储在本地的jar包 |

* compile ：作用于编译环境、测试环境、运行环境。
* test ： 作用于测试环境。典型的就是Junit坐标，以后使用Junit时，都会将scope指定为该值
* provided ：作用于编译环境、测试环境。我们后面会学习 `servlet-api` ，在使用它时，必须将 `scope` 设置为该值，不然运行时就会报错
* runtime  ： 作用于测试环境、运行环境。jdbc驱动一般将 `scope` 设置为该值，当然不设置也没有任何问题 

#### 3.4.4 依赖传递

简单说一下情况，我们自己写了两个模块，一个是红色图标，一个是绿色图标。然后红色模块里面我们添加一个依赖，例如Junit啊，log4j啊；同样我们在绿色模块也添加一些依赖。此时，这两个模块里面的依赖就是直接依赖；

既然都是Maven项目，那我们就可以在红色模块里面导入绿色模块的依赖撒，当导入后，我们点击打开红色模块的依赖库，就会看到绿色模块，并且点击下一级可以看到绿色模块他导入的依赖，而且红色模块可以直接使用他们。类似于继承的关系。

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220325182330732.png" alt="image-20220325182330732" style="zoom:80%;" />

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220325182113324.png" alt="image-20220325182113324" style="zoom:80%;" />

依赖具有传递性

- 直接依赖: 在当前项目中通过依赖配置建立的依赖关系
- 间接依赖: 被资源的资源如果依赖其他资源，当前项目间接依赖其他资源

==**依赖传递冲突问题**==

既然存在依赖传递，那么就肯定会引发冲突。例如我project02用到junit；project03也用到了junit；两个版本不同，那到底使用哪一个版本呢？？？？

Maven提供的解决方案如下：

- 路径优先:   当依赖中出现相同的资源时，层级越浅，优先级越高。
- 声明优先:   当资源在相同层级被依赖时，配置顺序靠前的覆盖顺序靠后的

<img src="https://java-baguwen.oss-cn-chengdu.aliyuncs.com/images/image-20220325182704150.png" alt="image-20220325182704150" style="zoom:80%;" />

还有一个特别一点的，特殊优先:   当同一个pom.xml配置了相同资源的不同版本，后配置的覆盖先配置的。

**==可选依赖==**

指我project03里面使用的依赖，不想让project02看见并使用。（project02引入project03）

标签`<optional>true</optional>`

```xml
<dependency> 
  <groupId>junit</groupId> 
  <artifactId>junit</artifactId> 
  <version>4.12</version> 
  <optional>true</optional>
</dependency>
```

**==排除依赖==**

（project02引入project03）指我project02不想用你project03里面的一些依赖。与前一个可选依赖，刚好反过来了。不用写版本号，只要组织id和项目id就行了。

标签`<exclusions>`

```xml
<dependency> 
  <groupId>junit</groupId> 
  <artifactId>junit</artifactId> 
  <version>4.12</version> 
  <exclusions> 
    	<exclusion> 
     	 		<groupId>org.hamcrest</groupId> 
      		<artifactId>hamcrest-core</artifactId>
			</exclusion>
	</exclusions>
</dependency>
```



# 分模块开发



[Maven高级：分模块开发_maven分模块开发_黑马程序员官方的博客-CSDN博客](https://blog.csdn.net/itcast_cn/article/details/125188149)

所有用Maven管理的真实的项目都应该是分模块的，每个模块都对应着一个`pom.xml`。它们之间通过继承和聚合（也称作多模块，multi-module）相互关联。那么，为什么要这么做呢？我们明明在开发一个项目，划分模块后，导入Eclipse变成了N个项目，这会带来复杂度，给开发带来不便。

为了解释原因，假设有这样一个项目，很常见的Java Web应用。在这个应用中，我们分了几层：

- Dao层负责数据库交互，封装了Hibernate交互的类。
- Service层处理业务逻辑，放一些Service接口和实现相关的Bean。
- Web层负责与客户端交互，主要有一些Structs的Action类。

对应的，在一个项目中，我们会看到一些包名：

- `org.myorg.app.dao`
- `org.myorg.app.service`
- `org.myorg.app.web`
- `org.myorg.app.util`

这样整个项目的框架就清晰了，但随着项目的进行，你可能会遇到如下问题：
这个应用可能需要有一个前台和一个后台管理端（web或者swing），你发现大部分dao，一些service，和大部分util是在两个应用中可用的。这样的问题，你一周内遇到了好几次。
`pom.xml`中的依赖列表越来越长以重用的，但是，由于目前只有一个项目（WAR），你不得不新建一个项目依赖这个WAR，这变得非常的恶心，因为在Maven中配置对WAR的依赖远不如依赖JAR那样简单明了，而且你根本不需要`org.myorg.app.web`。有人修改了dao，提交到svn并且不小心导致build失败了，你在编写service的代码，发现编译不过，只能等那人把dao修复了，你才能继续进行，很多人都在修改，到后来你根本就不清楚哪个依赖是谁需要的，渐渐的，很多不必要的依赖被引入。甚至出现了一个依赖有多个版本存在。
build整个项目的时间越来越长，尽管你只是一直在web层工作，但你不得不build整个项目。
某个模块，比如util，你只想让一些经验丰富的人来维护，可是，现在这种情况，每个开发者都能修改，这导致关键模块的代码质量不能达到你的要求。
我们会发现，其实这里实际上没有遵守一个设计模式原则：“高内聚，低耦合”。虽然我们通过包名划分了层次，并且你还会说，这些包的依赖都是单向的，没有包的环依赖。这很好，但还不够，因为就构建层次来说，所有东西都被耦合在一起了。因此我们需要使用Maven划分模块。

一个简单的Maven模块结构是这样的：

```java
 1---- app-parent
 2|-- pom.xml (pom)
 3|
 4|-- app-util
 5|        |-- pom.xml (jar)
 6|
 7|-- app-dao
 8|        |-- pom.xml (jar)
 9|
10|-- app-service
11|        |-- pom.xml (jar)
12|
13|-- app-web
14|-- pom.xml (war)
```

上述简单示意图中，有一个父项目(app-parent)聚合很多子项目（app-util, app-dao, app-service, app-web）。每个项目，不管是父子，都含有一个`pom.xml`文件。而且要注意的是，小括号中标出了每个项目的打包类型。父项目是pom,也只能是pom。子项目有jar，或者war。根据它包含的内容具体考虑。

这些模块的依赖关系如下：

```java
1app-dao      --> app-util
2app-service  --> app-dao
3app-web      --> app-service
```

注意依赖的传递性（大部分情况是传递的，除非你配置了特殊的依赖scope），app-dao依赖于app-util，app-service依赖于app-dao，于是app-service也依赖于app-util。同理，app-web依赖于app-dao,app-util。

用**项目层次的划分**替**代包层次的划分**能给我们带来如下好处：

- 方便重用，如果你有一个新的swing项目需要用到app-dao和app-service，添加对它们的依赖即可，你不再需要去依赖一个WAR。而有些模块，如app-util，完全可以渐渐进化成公司的一份基础工具类库，供所有项目使用。这是模块化最重要的一个目的。
- 由于你现在划分了模块，每个模块的配置都在各自的`pom.xml`里，不用再到一个混乱的纷繁复杂的总的POM中寻找自己的配置。
- 如果你只是在app-dao上工作，你不再需要build整个项目，只要在app-dao目录运行`mvn`命令进行build即可，这样可以节省时间，尤其是当项目越来越复杂，build越来越耗时后。
- 某些模块，如app-util被所有人依赖，但你不想给所有人修改，现在你完全可以从这个项目结构出来，做成另外一个项目，svn只给特定的人访问，但仍提供jar给别人使用。
- 多模块的Maven项目结构支持一些Maven的更有趣的特性（如`DepencencyManagement`），这留作以后讨论。
- 接下来讨论一下POM配置细节，实际上非常简单，先看app-parent的`pom.xml`：

```xml
 1<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 2xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 3<modelVersion>4.0.0</modelVersion>
 4<groupId>org.myorg.myapp</groupId>
 5<artifactId>app-parent</artifactId>
 6<packaging>pom</packaging>
 7<version>1.0-SNAPSHOT</version>
 8<modules>
 9    <module>app-util</module>
10    <module>app-dao</module>
11    <module>app-service</module>
12    <module>app-web</module>
13</modules>
14</project>
```

Maven的坐标GAV（`groupId`, `artifactId`, `version`）在这里进行配置，这些都是必须的。**特殊的地方在于，这里的`packaging`为`pom`。所有带有子模块的项目的`packaging`都为`pom`。**`packaging`如果不进行配置，它的默认值是`jar`，代表Maven会将项目打成一个jar包。
该配置重要的地方在于modules，例子中包含的子模块有app-util, app-dao, app-service, app-war。在Maven build app-parent的时候，它会根据子模块的相互依赖关系整理一个build顺序，然后依次build。
这就是一个父模块大概需要的配置，接下来看一下子模块符合配置继承父模块。

```xml
 1<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 2xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 3<parent>
 4<artifactId>app-parent</artifactId>
 5<groupId>org.myorg.myapp</groupId>
 6<version>1.0-SNAPSHOT</version>
 7</parent>
 8<modelVersion>4.0.0</modelVersion>
 9<artifactId>app-util</artifactId>
10<dependencies>
11    <dependency>
12        <groupId>commons-lang</groupId>
13        <artifactId>commons-lang</artifactId>
14        <version>2.4</version>
15   </dependency>
16</dependencies>
17</project>
```

app-util模块继承了app-parent父模块，因此这个POM的一开始就声明了对app-parent的引用，该引用是通过Maven坐标GAV实现的。而关于项目app-util本身，它却没有声明完整GAV，这里我们只看到了artifactId。这个POM并没有错，groupId和version默认从父模块继承了。实际上子模块从父模块继承一切东西，包括依赖，插件配置等等。
此外app-util配置了一个对于commons-lang的简单依赖，这是最简单的依赖配置形式。大部分情况，也是通过GAV引用的。
再看一下app-dao，它也是继承于app-parent，同时依赖于app-util：

```xml
 1<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 2xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 3<parent>
 4<artifactId>app-parent</artifactId>
 5<groupId>org.myorg.myapp</groupId>
 6<version>1.0-SNAPSHOT</version>
 7</parent>
 8<modelVersion>4.0.0</modelVersion>
 9<artifactId>app-dao</artifactId>
10<dependencies>
11       <dependency>
12         <groupId>org.myorg.myapp</groupId>
13         <artifactId>app-util</artifactId>
14         <version>${project.version}</version>
15    </dependency>
16</dependencies>
17</project>
```

该配置和app-util的配置几乎没什么差别，不同的地方在于，依赖变化了，app-dao依赖于app-util。这里要注意的是version的值为`${project.version}`，这个值是一个属性引用，指向了POM的project/version的值，也就是这个POM对应的version。由于app-dao的version继承于app-parent，因此它的值就是`1.0-SNAPSHOT`。而`app-util`也继承了这个值，因此在所有这些项目中，我们做到了保持版本一致。
这里还需要注意的是，app-dao依赖于app-util，而app-util又依赖于commons-lang，根据传递性，app-dao也拥有了对于commons-lang的依赖。
app-service我们跳过不谈，它依赖于app-dao。我们最后看一下app-web：

```xml
 1<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 2xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 3<parent>
 4<artifactId>app-parent</artifactId>
 5<groupId>org.myorg.myapp</groupId>
 6<version>1.0-SNAPSHOT</version>
 7</parent>
 8<modelVersion>4.0.0</modelVersion>
 9<artifactId>app-web</artifactId>
10<packaging>war</packaging>
11<dependencies>
12    <dependency>
13        <groupId>org.myorg.myapp</groupId>
14        <artifactId>app-service</artifactId>
15        <version>${project.version}</version>
16    </dependency>
17</dependencies>
18</project>
```

app-web依赖于app-service，因此配置了对其的依赖。
由于app-web是我们最终要部署的应用，因此它的packaging是war。为此，你需要有一个目录`src/main/webapp`。并在这个目录下拥有web应用需要的文件，如`/WEB-INF/web.xml`。没有web.xml，Maven会报告build失败，此外你可能还会有这样一些子目录：/js, /img, /css … 。

看看Maven是如何build整个项目的，我们在 app-parent 根目录中运行 `mvn clean install` ，输出的末尾会有大致这样的内容：

```java
 1...
 2...
 3[INFO] [war:war]
 4[INFO] Packaging webapp
 5[INFO] Assembling webapp[app-web] in [/home/juven/workspaces/ws-others/myapp/app-web/target/app-web-1.0-SNAPSHOT]
 6[INFO] Processing war project
 7[INFO] Webapp assembled in[50 msecs]
 8[INFO] Building war: /home/juven/workspaces/ws-others/myapp/app-web/target/app-web-1.0-SNAPSHOT.war
 9[INFO] [install:install]
10[INFO] Installing /home/juven/workspaces/ws-others/myapp/app-web/target/app-web-1.0-SNAPSHOT.war to /home/juven/.m2/repository/org/myorg/myapp/app-web/1.0-SNAPSHOT/app-web-1.0-SNAPSHOT.war
11[INFO]
12[INFO]
13[INFO] ------------------------------------------------------------------------
14[INFO] Reactor Summary:
15[INFO] ------------------------------------------------------------------------
16[INFO] app-parent ............................................ SUCCESS [1.191s]
17[INFO] app-util .............................................. SUCCESS [1.274s]
18[INFO] app-dao ............................................... SUCCESS [0.583s]
19[INFO] app-service ........................................... SUCCESS [0.593s]
20[INFO] app-web ............................................... SUCCESS [0.976s]
21[INFO] ------------------------------------------------------------------------
22[INFO] ------------------------------------------------------------------------
23[INFO] BUILD SUCCESSFUL
24[INFO] ------------------------------------------------------------------------
25[INFO] Total time: 4 seconds
26[INFO] Finished at: Sat Dec 27 08:20:18 PST 2008
27[INFO] Final Memory: 3M/17M
28[INFO] ------------------------------------------------------------------------
```

注意Reactor Summary，整个项目根据我们希望的顺序进行build。Maven根据我们的依赖配置，智能的安排了顺序，app-util, app-dao, app-service, app-web。

最后，你可以在 `app-web/target` 目录下找到文件 `app-web-1.0-SNAPSHOT.war` ，打开这个war包，在 `/WEB-INF/lib` 目录看到了 commons-lang-2.4.jar，以及对应的app-util, app-dao, app-service 的jar包。Maven自动帮你处理了打包的事情，并且根据你的依赖配置帮你引入了相应的jar文件。

使用多模块的Maven配置，可以帮助项目划分模块，鼓励重用，防止POM变得过于庞大，方便某个模块的构建，而不用每次都构建整个项目，并且使得针对某个模块的特殊控制更为方便。本文同时给出了一个实际的配置样例，展示了如何使用Maven配置多模块项目。







