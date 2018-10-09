1.何为Maven 
Maven是基于项目对象模型(POM)，可以通过一小段描述信息来管理项目的构建、依赖管理和项目信息管理。 
Maven是优秀的构建工具
自动化构建过程，从清理、编译、测试到生成报告，再到打包和部署。
是跨平台的，无论是Windows上，还是Linux或Mac上，都使用相同命令。
Maven是帮助我们管理工具 构建过程
2.Maven不仅仅是构建工具
依赖管理工具：提供中央仓库，自动下载构件。
3．Maven仓库
Maven仓库就是放置所有JAR文件（WAR，ZIP，POM等等）的地方，所有Maven项目可以从同一个Maven仓库中获取自己所需要的依赖JAR。


二..Maven使用

1.项目基本信息
modelVersion:当前POM模型版本，对于Maven3必须为4.0.0
groupId:定义当前项目隶属的实际项目。
artifact:定义实际项目中的一个Maven项目（模块）。
version:定义Maven项目当前所处版本。
packaging:定义Maven项目打包方式。默认为jar。
classifier:定义构建输出的一些附属构件。生成javadoc等。由插件自动生成，不能直接定义。
2.依赖范围
1.compile：默认的scope。任何定义在compile scope下的依赖将会在所有的class paths下可用。maven工程会将其打包到最终的arifact中。如果你构建一个WAR类型的artefact，那么在compile scope下引用的JAR文件将会被集成到WAR文件内。  
2.provided：这个scope假定对应的依赖会由运行这个应用的JDK或者容器来提供。最好的例子就是servlet API。任何在provided scope下定义的依赖在构建时的类路径里是可用的，但是不会被打包到最终的artifact中。如果是一个WAR的文件，servlet API在构建时的类路径里是可用的，但是并不会被打包到WAR文件中。
  
3.runtime：在runtime scope下定义的依赖只会在运行期可用，而在构建期的类路径下不可用。这些依赖将会被打包到最终的artifact中。比如你有一个基于web的应用需要在运行时访问MySQL数据库。你的代码没有任何MySQL数据库驱动的硬依赖。你的代码仅仅是基于JDBC API来编写，在构建期并不需要MySQL数据库驱动。然而，在运行期，就需要相应的驱动来操作MySQL数据库了。因此，这个驱动应该被打包到最终的artifact中。
   
4.test：只用于测试变异的依赖（比如JUnit），execution必须定义在test scope下。这些依赖不会被打包到最终的artefact中。   
5.system：于provided scope很像。唯一的区别在于，在system scope中，你需要告诉Mave如何去找到这个依赖。如果你要引用的依赖在Maven仓库中不存在时，就可以用这个scope。不推荐使用system依赖。  
6.import：从其它的pom文件中导入依赖设置。
<!--------简介摘要
1.compile（编译范围） compile是默认的范围，会被打包。 
2.provided（已提供范围） provided依赖只有在当JDK或者一个容器已提供该依赖之后才使用。它们不是传递性的，也不会被打包。

3.runtime（运行时范围） runtime依赖在运行和测试系统的时候需要，但在编译的时候不需要。
4.test（测试范围）只有在测试编译和测试运行阶段可用。
5.system（系统范围）必须显式的提供一个对于本地系统中JAR文件的路径。注意该范围是不推荐使用。
-------->


三．1.配置地址

<!-------------本地配置---------->
<localRepository>E:\Maven\MAVEN\apache-maven-3.0.4_localtest\resp</localRepository>
2.私服地址
<mirror>
      <id>ali+maven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>        
</mirror>
3.java项目配置
<dependency>
  <groupId>公司名（cn.easytop）</groupId>
  <artifactId>项目名</artifactId>
  <version>版本号</version>
</dependency>
groupld 因为项目是由不同的公司开发的，项目是区别哪个公司的
artifactld 在同一个公司有多个项目，项目名是区分项目哪个项目组开发的
SNAPSHOT( 开发阶段是不稳定)
RELEASE（发布阶段稳定）
4.Maven是帮助我们管理工具 构建过程
5.<!------用java记事本编译
pushd F:\JspSrv\demo\src
javac cn\et\test\Test.java
java cn.et.test.Test
pause
----------->
1创建项目
项目类型 javase项目  javaee项目
2.编码阶段
编码+jar包+tomcat配置
3.编译项目
jdk的javac
javac cn\et\test\Test.java
4.运行项目
java cn.et.test.Test
5.打包发布
java -jar Test.jar
四.maven原理


五．Maven常用命令

mvn archetype:generate 
：创建 Maven 项目

mvn compile ：编译源代码

mvn test-compile 
：编译测试代码 
mvn test ： 运行应用程序中的单元测试

mvn site ： 生成项目相关信息的网站

mvn clean ：清除目标目录中的生成结果

mvn package ： 依据项目生成
jar 文件

mvn install ：在本地
Repository 中安装
jar 
mvn deploy：将jar包发布到远程仓库

mvn eclipse:eclipse 
：生成 Eclipse 项目文件
 



六.pom.xml 插件配置

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<!-- 表示maven的pom类型版本
 -->
  <modelVersion>4.0.0</modelVersion>
  <!-- 公司名  -->
  <groupId>cn.easytop</groupId>
  <!-- 项目名 -->
  <artifactId>testwar</artifactId>
  <!-- 项目版本号  -->
  <version>0.0.1-SNAPSHOT</version>
  <!-- 项目类型jar
javase项目(main方法)  javaee(要发布到tomcat)-->
  <packaging>war</packaging>
  
  <!-- 依赖 当前的项目依赖哪些jar -->
  <dependencies>
   <!-- 从仓库下载jar包 -->
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>5.1.16</version>
   <scope>runtime</scope>
</dependency>
<!-- 从本地文件系统中寻找jar(不开眼的) -->
<dependency>
   <groupId>oracle</groupId>
   <artifactId>oracle</artifactId>
   <version>oracle11g</version>
   <!-- 作用域 -->
   <scope>system</scope>
   <systemPath>E:\4.JDBC\教学软件\ojdbc6.jar</systemPath>
</dependency>
<dependency>
   <groupId>springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
   <version>1.2.6</version>
</dependency>
<dependency>
   <groupId>net.paoding</groupId>
   <artifactId>paoding-rose</artifactId>
   <version>2.0.u08</version>
</dependency>
<dependency>
   <groupId>org.apache.tomcat.maven</groupId>
   <artifactId>tomcat6-maven-plugin</artifactId>
   <version>2.1</version>
</dependency>
  </dependencies>
   <!-- 
maven插件
表示maven构建构成中执行的jar名称 插件名-maven-plugin命名
  可以通过 jar包中plugins.xml中找到所有的配置定义 --->
<build>
<plugins>
<!-- mvn tomcat6:run -->
<plugin>
<groupId>org.codehaus.mojo</groupId>
   <artifactId>tomcat-maven-plugin</artifactId>
   <version>1.1</version>
   <configuration>
   <port>8089</port>
   <uriEncoding>UTF-8</uriEncoding>
   </configuration>
</plugin>
</plugins>
</build>
</project>
七.1．继承(可以管理jar包版本)
一个项目继承了另一个项目是，那么子项目中就没必要在定义版本，因为将来如果同一个公司开发其它项目，而这些项目之间使用的文件上传库都应该是相同的版本,所以父项目中已经定义了版本号，不需要子项目中再定义，如果一个项目中没有父项目，那么就要定
2.．dependency和dependencyManagement区别
<!--子项目直接就加载-->
dependency：一般用于开发项目中,在这里定义的子项目中一定有
<dependencies>
<dependency>
   <groupId>commons-beanutils</groupId>
   <artifactId>commons-beanutils</artifactId>
   <version>1.9.0</version>
</dependency>
</dependencies>
  <!-- 只是定义所有的版本信息 ，子项目可以选择性加载-->
dependencyManagement：适合用于框架中,在这里定义的子项目中没有
  <dependencyManagement>
   <dependencies>
   <dependency>
   <groupId>commons-fileupload</groupId>
   <artifactId>commons-fileupload</artifactId>
    <version>${fileuqload-version}</version>
</dependency>
<!-- 从仓库下载jar包 -->
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>${mysql-version}</version>
</dependency>
   </dependencies>
  </dependencyManagement>

3.(1).父项目(例如upload_common)
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>cn.easytop</groupId>
  <artifactId>upload-common</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>pom</packaging>
  <!-- 自定义属性，定义所有jar包版本库 -->
  <properties>
   <fileuqload-version>1.3.2</fileuqload-version>
   <mysql-version>5.1.16</mysql-version>
  </properties>
  <!-- 子项目直接加载 -->
<dependencies>
<dependency>
   <groupId>commons-beanutils</groupId>
   <artifactId>commons-beanutils</artifactId>
   <version>1.9.0</version>
</dependency>
</dependencies>
  <!-- 只是定义所有的版本信息 ，子项目可以选择性加载-->
  <dependencyManagement>
   <dependencies>
   <dependency>
   <groupId>commons-fileupload</groupId>
   <artifactId>commons-fileupload</artifactId>
    <version>${fileuqload-version}</version>
</dependency>
<!-- 从仓库下载jar包 -->
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>${mysql-version}</version>
</dependency>
   </dependencies>
  </dependencyManagement>
</project>
 
(2).子项目(baidupan
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>cn.easytop</groupId>
  <artifactId>baidupan</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>war</packaging>
  <!-- 继承版本 -->
  <parent>
   <groupId>cn.easytop</groupId>
            
                
									
						阅读更多
