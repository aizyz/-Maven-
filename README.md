一..Maven简介

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

--------------------------------------------------------------------------------------------------------------------------------------->

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
-------------------------------------------------------------------------------------------------------------------------------------->

三．Maven常用命令

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
 




            
                
									
						阅读更多
