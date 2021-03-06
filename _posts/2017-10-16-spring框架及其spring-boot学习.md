---
layout:   post
title:    "spring框架及其spring boot学习"
subtitle: “spring”
date:     2017-10-13
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - spring boot
---

### [spring boot](http://blog.csdn.net/adeyi/article/details/17259479)

1. Pom.xml

   > 1. Project Object Model，项目对象模型。通过xml格式保存的pom.xml文件。作用类似ant的build.xml文件，功能更强大。该文件用于管理：源代码、配置文件、开发者的信息和角色、问题追踪系统、组织信息、项目授权、项目的url、项目的依赖关系等等。一个完整的pom.xml文件，放置在项目的根目录下。
   >
   > 2. ```xml
   >    <span style="padding:0px; margin:0px"><project xmlns="http://maven.apache.org/POM/4.0.0"   
   >        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
   >    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0http://maven.apache.org/maven-v4_0_0.xsd">   
   >        <!--父项目的坐标。如果项目中没有规定某个元素的值，那么父项目中的对应值即为项目的默认值。 坐标包括group ID，artifact ID和 version。-->  
   >        <parent>  
   >         <!--被继承的父项目的构件标识符-->  
   >         <artifactId/>  
   >         <!--被继承的父项目的全球唯一标识符-->  
   >         <groupId/>  
   >         <!--被继承的父项目的版本-->  
   >         <version/>  
   >         <!-- 父项目的pom.xml文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项 目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom。-->  
   >         <relativePath/>  
   >     </parent>  
   >     <!--声明项目描述符遵循哪一个POM模型版本。模型本身的版本很少改变，虽然如此，但它仍然是必不可少的，这是为了当Maven引入了新的特性或者其他模型变更的时候，确保稳定性。-->     
   >        <modelVersion>4.0.0</modelVersion>   
   >        <!--项目的全球唯一标识符，通常使用全限定的包名区分该项目和其他项目。并且构建时生成的路径也是由此生成， 如com.mycompany.app生成的相对路径为：/com/mycompany/app-->   
   >        <groupId>asia.banseon</groupId>   
   >        <!-- 构件的标识符，它和group ID一起唯一标识一个构件。换句话说，你不能有两个不同的项目拥有同样的artifact ID和groupID；在某个 特定的group ID下，artifact ID也必须是唯一的。构件是项目产生的或使用的一个东西，Maven为项目产生的构件包括：JARs，源 码，二进制发布和WARs等。-->   
   >        <artifactId>banseon-maven2</artifactId>   
   >        <!--项目产生的构件类型，例如jar、war、ear、pom。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型-->   
   >        <packaging>jar</packaging>   
   >        <!--项目当前版本，格式为:主版本.次版本.增量版本-限定版本号-->   
   >        <version>1.0-SNAPSHOT</version>   
   >        <!--项目的名称, Maven产生的文档用-->   
   >        <name>banseon-maven</name>   
   >        <!--项目主页的URL, Maven产生的文档用-->   
   >        <url>http://www.baidu.com/banseon</url>   
   >        <!-- 项目的详细描述, Maven 产生的文档用。  当这个元素能够用HTML格式描述时（例如，CDATA中的文本会被解析器忽略，就可以包含HTML标 签）， 不鼓励使用纯文本描述。如果你需要修改产生的web站点的索引页面，你应该修改你自己的索引页文件，而不是调整这里的文档。-->   
   >        <description>A maven project to study maven.</description>   
   >        <!--描述了这个项目构建环境中的前提条件。-->  
   >     <prerequisites>  
   >      <!--构建该项目或使用该插件所需要的Maven的最低版本-->  
   >        <maven/>  
   >     </prerequisites>  
   >     <!--项目的问题管理系统(Bugzilla, Jira, Scarab,或任何你喜欢的问题管理系统)的名称和URL，本例为 jira-->   
   >        <issueManagement>  
   >         <!--问题管理系统（例如jira）的名字，-->   
   >            <system>jira</system>   
   >            <!--该项目使用的问题管理系统的URL-->  
   >            <url>http://jira.baidu.com/banseon</url>   
   >        </issueManagement>   
   >        <!--项目持续集成信息-->  
   >     <ciManagement>  
   >      <!--持续集成系统的名字，例如continuum-->  
   >      <system/>  
   >      <!--该项目使用的持续集成系统的URL（如果持续集成系统有web接口的话）。-->  
   >      <url/>  
   >      <!--构建完成时，需要通知的开发者/用户的配置项。包括被通知者信息和通知条件（错误，失败，成功，警告）-->  
   >      <notifiers>  
   >       <!--配置一种方式，当构建中断时，以该方式通知用户/开发者-->  
   >       <notifier>  
   >        <!--传送通知的途径-->  
   >        <type/>  
   >        <!--发生错误时是否通知-->  
   >        <sendOnError/>  
   >        <!--构建失败时是否通知-->  
   >        <sendOnFailure/>  
   >        <!--构建成功时是否通知-->  
   >        <sendOnSuccess/>  
   >        <!--发生警告时是否通知-->  
   >        <sendOnWarning/>  
   >        <!--不赞成使用。通知发送到哪里-->  
   >        <address/>  
   >        <!--扩展配置项-->  
   >        <configuration/>  
   >       </notifier>  
   >      </notifiers>  
   >     </ciManagement>  
   >     <!--项目创建年份，4位数字。当产生版权信息时需要使用这个值。-->  
   >        <inceptionYear/>  
   >        <!--项目相关邮件列表信息-->   
   >        <mailingLists>  
   >         <!--该元素描述了项目相关的所有邮件列表。自动产生的网站引用这些信息。-->   
   >            <mailingList>   
   >             <!--邮件的名称-->  
   >                <name>Demo</name>   
   >                <!--发送邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
   >                <post>banseon@126.com</post>   
   >                <!--订阅邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
   >                <subscribe>banseon@126.com</subscribe>   
   >                <!--取消订阅邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
   >                <unsubscribe>banseon@126.com</unsubscribe>   
   >                <!--你可以浏览邮件信息的URL-->  
   >                <archive>http:/hi.baidu.com/banseon/demo/dev/</archive>   
   >            </mailingList>   
   >        </mailingLists>   
   >        <!--项目开发者列表-->   
   >        <developers>   
   >         <!--某个项目开发者的信息-->  
   >            <developer>   
   >             <!--SCM里项目开发者的唯一标识符-->  
   >                <id>HELLO WORLD</id>   
   >                <!--项目开发者的全名-->  
   >                <name>banseon</name>   
   >                <!--项目开发者的email-->  
   >                <email>banseon@126.com</email>   
   >                <!--项目开发者的主页的URL-->  
   >                <url/>  
   >                <!--项目开发者在项目中扮演的角色，角色元素描述了各种角色-->  
   >                <roles>   
   >                    <role>Project Manager</role>   
   >                    <role>Architect</role>   
   >                </roles>  
   >                <!--项目开发者所属组织-->  
   >                <organization>demo</organization>   
   >                <!--项目开发者所属组织的URL-->  
   >                <organizationUrl>http://hi.baidu.com/banseon</organizationUrl>   
   >                <!--项目开发者属性，如即时消息如何处理等-->  
   >                <properties>   
   >                    <dept>No</dept>   
   >                </properties>  
   >                <!--项目开发者所在时区， -11到12范围内的整数。-->  
   >                <timezone>-5</timezone>   
   >            </developer>   
   >        </developers>   
   >        <!--项目的其他贡献者列表-->   
   >        <contributors>  
   >         <!--项目的其他贡献者。参见developers/developer元素-->  
   >         <contributor>  
   >       <name/><email/><url/><organization/><organizationUrl/><roles/><timezone/><properties/>  
   >         </contributor>       
   >        </contributors>     
   >        <!--该元素描述了项目所有License列表。 应该只列出该项目的license列表，不要列出依赖项目的 license列表。如果列出多个license，用户可以选择它们中的一个而不是接受所有license。-->   
   >        <licenses>  
   >         <!--描述了项目的license，用于生成项目的web站点的license页面，其他一些报表和validation也会用到该元素。-->   
   >            <license>  
   >             <!--license用于法律上的名称-->  
   >                <name>Apache 2</name>   
   >                <!--官方的license正文页面的URL-->  
   >                <url>http://www.baidu.com/banseon/LICENSE-2.0.txt</url>   
   >                <!--项目分发的主要方式：  
   >                  repo，可以从Maven库下载  
   >                  manual， 用户必须手动下载和安装依赖-->  
   >                <distribution>repo</distribution>   
   >                <!--关于license的补充信息-->  
   >                <comments>A business-friendly OSS license</comments>   
   >            </license>   
   >        </licenses>   
   >        <!--SCM(Source Control Management)标签允许你配置你的代码库，供Maven web站点和其它插件使用。-->   
   >        <scm>   
   >            <!--SCM的URL,该URL描述了版本库和如何连接到版本库。欲知详情，请看SCMs提供的URL格式和列表。该连接只读。-->   
   >            <connection>   
   >                scm:svn:http://svn.baidu.com/banseon/maven/banseon/banseon-maven2-trunk(dao-trunk)    
   >            </connection>   
   >            <!--给开发者使用的，类似connection元素。即该连接不仅仅只读-->  
   >            <developerConnection>   
   >                scm:svn:http://svn.baidu.com/banseon/maven/banseon/dao-trunk    
   >            </developerConnection>  
   >            <!--当前代码的标签，在开发阶段默认为HEAD-->  
   >            <tag/>         
   >            <!--指向项目的可浏览SCM库（例如ViewVC或者Fisheye）的URL。-->   
   >            <url>http://svn.baidu.com/banseon</url>   
   >        </scm>   
   >        <!--描述项目所属组织的各种属性。Maven产生的文档用-->   
   >        <organization>   
   >         <!--组织的全名-->  
   >            <name>demo</name>   
   >            <!--组织主页的URL-->  
   >            <url>http://www.baidu.com/banseon</url>   
   >        </organization>  
   >        <!--构建项目需要的信息-->  
   >        <build>  
   >         <!--该元素设置了项目源码目录，当构建项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->  
   >      <sourceDirectory/>  
   >      <!--该元素设置了项目脚本源码目录，该目录和源码目录不同：绝大多数情况下，该目录下的内容 会被拷贝到输出目录(因为脚本是被解释的，而不是被编译的)。-->  
   >      <scriptSourceDirectory/>  
   >      <!--该元素设置了项目单元测试使用的源码目录，当测试项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->  
   >      <testSourceDirectory/>  
   >      <!--被编译过的应用程序class文件存放的目录。-->  
   >      <outputDirectory/>  
   >      <!--被编译过的测试class文件存放的目录。-->  
   >      <testOutputDirectory/>  
   >      <!--使用来自该项目的一系列构建扩展-->  
   >      <extensions>  
   >       <!--描述使用到的构建扩展。-->  
   >       <extension>  
   >        <!--构建扩展的groupId-->  
   >        <groupId/>  
   >        <!--构建扩展的artifactId-->  
   >        <artifactId/>  
   >        <!--构建扩展的版本-->  
   >        <version/>  
   >       </extension>  
   >      </extensions>  
   >      <!--当项目没有规定目标（Maven2 叫做阶段）时的默认值-->  
   >      <defaultGoal/>  
   >      <!--这个元素描述了项目相关的所有资源路径列表，例如和项目相关的属性文件，这些资源被包含在最终的打包文件里。-->  
   >      <resources>  
   >       <!--这个元素描述了项目相关或测试相关的所有资源路径-->  
   >       <resource>  
   >        <!-- 描述了资源的目标路径。该路径相对target/classes目录（例如${project.build.outputDirectory}）。举个例 子，如果你想资源在特定的包里(org.apache.maven.messages)，你就必须该元素设置为org/apache/maven /messages。然而，如果你只是想把资源放到源码目录结构里，就不需要该配置。-->  
   >        <targetPath/>  
   >        <!--是否使用参数值代替参数名。参数值取自properties元素或者文件里配置的属性，文件在filters元素里列出。-->  
   >        <filtering/>  
   >        <!--描述存放资源的目录，该路径相对POM路径-->  
   >        <directory/>  
   >        <!--包含的模式列表，例如**/*.xml.-->  
   >        <includes/>  
   >        <!--排除的模式列表，例如**/*.xml-->  
   >        <excludes/>  
   >       </resource>  
   >      </resources>  
   >      <!--这个元素描述了单元测试相关的所有资源路径，例如和单元测试相关的属性文件。-->  
   >      <testResources>  
   >       <!--这个元素描述了测试相关的所有资源路径，参见build/resources/resource元素的说明-->  
   >       <testResource>  
   >        <targetPath/><filtering/><directory/><includes/><excludes/>  
   >       </testResource>  
   >      </testResources>  
   >      <!--构建产生的所有文件存放的目录-->  
   >      <directory/>  
   >      <!--产生的构件的文件名，默认值是${artifactId}-${version}。-->  
   >      <finalName/>  
   >      <!--当filtering开关打开时，使用到的过滤器属性文件列表-->  
   >      <filters/>  
   >      <!--子项目可以引用的默认插件信息。该插件配置项直到被引用时才会被解析或绑定到生命周期。给定插件的任何本地配置都会覆盖这里的配置-->  
   >      <pluginManagement>  
   >       <!--使用的插件列表 。-->  
   >       <plugins>  
   >        <!--plugin元素包含描述插件所需要的信息。-->  
   >        <plugin>  
   >         <!--插件在仓库里的group ID-->  
   >         <groupId/>  
   >         <!--插件在仓库里的artifact ID-->  
   >         <artifactId/>  
   >         <!--被使用的插件的版本（或版本范围）-->  
   >         <version/>  
   >         <!--是否从该插件下载Maven扩展（例如打包和类型处理器），由于性能原因，只有在真需要下载时，该元素才被设置成enabled。-->  
   >         <extensions/>  
   >         <!--在构建生命周期中执行一组目标的配置。每个目标可能有不同的配置。-->  
   >         <executions>  
   >          <!--execution元素包含了插件执行需要的信息-->  
   >          <execution>  
   >           <!--执行目标的标识符，用于标识构建过程中的目标，或者匹配继承过程中需要合并的执行目标-->  
   >           <id/>  
   >           <!--绑定了目标的构建生命周期阶段，如果省略，目标会被绑定到源数据里配置的默认阶段-->  
   >           <phase/>  
   >           <!--配置的执行目标-->  
   >           <goals/>  
   >           <!--配置是否被传播到子POM-->  
   >           <inherited/>  
   >           <!--作为DOM对象的配置-->  
   >           <configuration/>  
   >          </execution>  
   >         </executions>  
   >         <!--项目引入插件所需要的额外依赖-->  
   >         <dependencies>  
   >          <!--参见dependencies/dependency元素-->  
   >          <dependency>  
   >           ......  
   >          </dependency>  
   >         </dependencies>       
   >         <!--任何配置是否被传播到子项目-->  
   >         <inherited/>  
   >         <!--作为DOM对象的配置-->  
   >         <configuration/>  
   >        </plugin>  
   >       </plugins>  
   >      </pluginManagement>  
   >      <!--使用的插件列表-->  
   >      <plugins>  
   >       <!--参见build/pluginManagement/plugins/plugin元素-->  
   >       <plugin>  
   >        <groupId/><artifactId/><version/><extensions/>  
   >        <executions>  
   >         <execution>  
   >          <id/><phase/><goals/><inherited/><configuration/>  
   >         </execution>  
   >        </executions>  
   >        <dependencies>  
   >         <!--参见dependencies/dependency元素-->  
   >         <dependency>  
   >          ......  
   >         </dependency>  
   >        </dependencies>  
   >        <goals/><inherited/><configuration/>  
   >       </plugin>  
   >      </plugins>  
   >     </build>  
   >     <!--在列的项目构建profile，如果被激活，会修改构建处理-->  
   >     <profiles>  
   >      <!--根据环境参数或命令行参数激活某个构建处理-->  
   >      <profile>  
   >       <!--构建配置的唯一标识符。即用于命令行激活，也用于在继承时合并具有相同标识符的profile。-->  
   >       <id/>  
   >       <!--自动触发profile的条件逻辑。Activation是profile的开启钥匙。profile的力量来自于它  
   >       能够在某些特定的环境中自动使用某些特定的值；这些环境通过activation元素指定。activation元素并不是激活profile的唯一方式。-->  
   >       <activation>  
   >        <!--profile默认是否激活的标志-->  
   >        <activeByDefault/>  
   >        <!--当匹配的jdk被检测到，profile被激活。例如，1.4激活JDK1.4，1.4.0_2，而!1.4激活所有版本不是以1.4开头的JDK。-->  
   >        <jdk/>  
   >        <!--当匹配的操作系统属性被检测到，profile被激活。os元素可以定义一些操作系统相关的属性。-->  
   >        <os>  
   >         <!--激活profile的操作系统的名字-->  
   >         <name>Windows XP</name>  
   >         <!--激活profile的操作系统所属家族(如 'windows')-->  
   >         <family>Windows</family>  
   >         <!--激活profile的操作系统体系结构 -->  
   >         <arch>x86</arch>  
   >         <!--激活profile的操作系统版本-->  
   >         <version>5.1.2600</version>  
   >        </os>  
   >        <!--如果Maven检测到某一个属性（其值可以在POM中通过${名称}引用），其拥有对应的名称和值，Profile就会被激活。如果值  
   >        字段是空的，那么存在属性名称字段就会激活profile，否则按区分大小写方式匹配属性值字段-->  
   >        <property>  
   >         <!--激活profile的属性的名称-->  
   >         <name>mavenVersion</name>  
   >         <!--激活profile的属性的值-->  
   >         <value>2.0.3</value>  
   >        </property>  
   >        <!--提供一个文件名，通过检测该文件的存在或不存在来激活profile。missing检查文件是否存在，如果不存在则激活  
   >        profile。另一方面，exists则会检查文件是否存在，如果存在则激活profile。-->  
   >        <file>  
   >         <!--如果指定的文件存在，则激活profile。-->  
   >         <exists>/usr/local/hudson/hudson-home/jobs/maven-guide-zh-to-production/workspace/</exists>  
   >         <!--如果指定的文件不存在，则激活profile。-->  
   >         <missing>/usr/local/hudson/hudson-home/jobs/maven-guide-zh-to-production/workspace/</missing>  
   >        </file>  
   >       </activation>  
   >       <!--构建项目所需要的信息。参见build元素-->  
   >       <build>  
   >        <defaultGoal/>  
   >        <resources>  
   >         <resource>  
   >          <targetPath/><filtering/><directory/><includes/><excludes/>  
   >         </resource>  
   >        </resources>  
   >        <testResources>  
   >         <testResource>  
   >          <targetPath/><filtering/><directory/><includes/><excludes/>  
   >         </testResource>  
   >        </testResources>  
   >        <directory/><finalName/><filters/>  
   >        <pluginManagement>  
   >         <plugins>  
   >          <!--参见build/pluginManagement/plugins/plugin元素-->  
   >          <plugin>  
   >           <groupId/><artifactId/><version/><extensions/>  
   >           <executions>  
   >            <execution>  
   >             <id/><phase/><goals/><inherited/><configuration/>  
   >            </execution>  
   >           </executions>  
   >           <dependencies>  
   >            <!--参见dependencies/dependency元素-->  
   >            <dependency>  
   >             ......  
   >            </dependency>  
   >           </dependencies>  
   >           <goals/><inherited/><configuration/>  
   >          </plugin>  
   >         </plugins>  
   >        </pluginManagement>  
   >        <plugins>  
   >         <!--参见build/pluginManagement/plugins/plugin元素-->  
   >         <plugin>  
   >          <groupId/><artifactId/><version/><extensions/>  
   >          <executions>  
   >           <execution>  
   >            <id/><phase/><goals/><inherited/><configuration/>  
   >           </execution>  
   >          </executions>  
   >          <dependencies>  
   >           <!--参见dependencies/dependency元素-->  
   >           <dependency>  
   >            ......  
   >           </dependency>  
   >          </dependencies>  
   >          <goals/><inherited/><configuration/>  
   >         </plugin>  
   >        </plugins>  
   >       </build>  
   >       <!--模块（有时称作子项目） 被构建成项目的一部分。列出的每个模块元素是指向该模块的目录的相对路径-->  
   >       <modules/>  
   >       <!--发现依赖和扩展的远程仓库列表。-->  
   >       <repositories>  
   >        <!--参见repositories/repository元素-->  
   >        <repository>  
   >         <releases>  
   >          <enabled/><updatePolicy/><checksumPolicy/>  
   >         </releases>  
   >         <snapshots>  
   >          <enabled/><updatePolicy/><checksumPolicy/>  
   >         </snapshots>  
   >         <id/><name/><url/><layout/>  
   >        </repository>  
   >       </repositories>  
   >       <!--发现插件的远程仓库列表，这些插件用于构建和报表-->  
   >       <pluginRepositories>  
   >        <!--包含需要连接到远程插件仓库的信息.参见repositories/repository元素-->      
   >        <pluginRepository>  
   >         <releases>  
   >          <enabled/><updatePolicy/><checksumPolicy/>  
   >         </releases>  
   >         <snapshots>  
   >          <enabled/><updatePolicy/><checksumPolicy/>  
   >         </snapshots>  
   >         <id/><name/><url/><layout/>  
   >        </pluginRepository>  
   >       </pluginRepositories>  
   >       <!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。要获取更多信息，请看项目依赖机制。-->  
   >       <dependencies>  
   >        <!--参见dependencies/dependency元素-->  
   >        <dependency>  
   >         ......  
   >        </dependency>  
   >       </dependencies>  
   >       <!--不赞成使用. 现在Maven忽略该元素.-->  
   >       <reports/>     
   >       <!--该元素包括使用报表插件产生报表的规范。当用户执行“mvn site”，这些报表就会运行。 在页面导航栏能看到所有报表的链接。参见reporting元素-->  
   >       <reporting>  
   >        ......  
   >       </reporting>  
   >       <!--参见dependencyManagement元素-->  
   >       <dependencyManagement>  
   >        <dependencies>  
   >         <!--参见dependencies/dependency元素-->  
   >         <dependency>  
   >          ......  
   >         </dependency>  
   >        </dependencies>  
   >       </dependencyManagement>  
   >       <!--参见distributionManagement元素-->  
   >       <distributionManagement>  
   >        ......  
   >       </distributionManagement>  
   >       <!--参见properties元素-->  
   >       <properties/>  
   >      </profile>  
   >     </profiles>  
   >     <!--模块（有时称作子项目） 被构建成项目的一部分。列出的每个模块元素是指向该模块的目录的相对路径-->  
   >     <modules/>  
   >        <!--发现依赖和扩展的远程仓库列表。-->   
   >        <repositories>   
   >         <!--包含需要连接到远程仓库的信息-->  
   >            <repository>  
   >             <!--如何处理远程仓库里发布版本的下载-->  
   >             <releases>  
   >              <!--true或者false表示该仓库是否为下载某种类型构件（发布版，快照版）开启。 -->  
   >        <enabled/>  
   >        <!--该元素指定更新发生的频率。Maven会比较本地POM和远程POM的时间戳。这里的选项是：always（一直），daily（默认，每日），interval：X（这里X是以分钟为单位的时间间隔），或者never（从不）。-->  
   >        <updatePolicy/>  
   >        <!--当Maven验证构件校验文件失败时该怎么做：ignore（忽略），fail（失败），或者warn（警告）。-->  
   >        <checksumPolicy/>  
   >       </releases>  
   >       <!-- 如何处理远程仓库里快照版本的下载。有了releases和snapshots这两组配置，POM就可以在每个单独的仓库中，为每种类型的构件采取不同的 策略。例如，可能有人会决定只为开发目的开启对快照版本下载的支持。参见repositories/repository/releases元素 -->  
   >       <snapshots>  
   >        <enabled/><updatePolicy/><checksumPolicy/>  
   >       </snapshots>  
   >       <!--远程仓库唯一标识符。可以用来匹配在settings.xml文件里配置的远程仓库-->  
   >       <id>banseon-repository-proxy</id>   
   >       <!--远程仓库名称-->  
   >                <name>banseon-repository-proxy</name>   
   >                <!--远程仓库URL，按protocol://hostname/path形式-->  
   >                <url>http://192.168.1.169:9999/repository/</url>   
   >                <!-- 用于定位和排序构件的仓库布局类型-可以是default（默认）或者legacy（遗留）。Maven 2为其仓库提供了一个默认的布局；然 而，Maven 1.x有一种不同的布局。我们可以使用该元素指定布局是default（默认）还是legacy（遗留）。-->  
   >                <layout>default</layout>             
   >            </repository>   
   >        </repositories>  
   >        <!--发现插件的远程仓库列表，这些插件用于构建和报表-->  
   >        <pluginRepositories>  
   >         <!--包含需要连接到远程插件仓库的信息.参见repositories/repository元素-->  
   >      <pluginRepository>  
   >       ......  
   >      </pluginRepository>  
   >     </pluginRepositories>  
   >         
   >        <!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。要获取更多信息，请看项目依赖机制。-->   
   >        <dependencies>   
   >            <dependency>  
   >       <!--依赖的group ID-->  
   >                <groupId>org.apache.maven</groupId>   
   >                <!--依赖的artifact ID-->  
   >                <artifactId>maven-artifact</artifactId>   
   >                <!--依赖的版本号。 在Maven 2里, 也可以配置成版本号的范围。-->  
   >                <version>3.8.1</version>   
   >                <!-- 依赖类型，默认类型是jar。它通常表示依赖的文件的扩展名，但也有例外。一个类型可以被映射成另外一个扩展名或分类器。类型经常和使用的打包方式对应， 尽管这也有例外。一些类型的例子：jar，war，ejb-client和test-jar。如果设置extensions为 true，就可以在 plugin里定义新的类型。所以前面的类型的例子不完整。-->  
   >                <type>jar</type>  
   >                <!-- 依赖的分类器。分类器可以区分属于同一个POM，但不同构建方式的构件。分类器名被附加到文件名的版本号后面。例如，如果你想要构建两个单独的构件成 JAR，一个使用Java 1.4编译器，另一个使用Java 6编译器，你就可以使用分类器来生成两个单独的JAR构件。-->  
   >                <classifier></classifier>  
   >                <!--依赖范围。在项目发布过程中，帮助决定哪些构件被包括进来。欲知详情请参考依赖机制。  
   >                    - compile ：默认范围，用于编译    
   >                    - provided：类似于编译，但支持你期待jdk或者容器提供，类似于classpath    
   >                    - runtime: 在执行时需要使用    
   >                    - test:    用于test任务时使用    
   >                    - system: 需要外在提供相应的元素。通过systemPath来取得    
   >                    - systemPath: 仅用于范围为system。提供相应的路径    
   >                    - optional:   当项目自身被依赖时，标注依赖是否传递。用于连续依赖时使用-->   
   >                <scope>test</scope>     
   >                <!--仅供system范围使用。注意，不鼓励使用这个元素，并且在新的版本中该元素可能被覆盖掉。该元素为依赖规定了文件系统上的路径。需要绝对路径而不是相对路径。推荐使用属性匹配绝对路径，例如${java.home}。-->  
   >                <systemPath></systemPath>   
   >                <!--当计算传递依赖时， 从依赖构件列表里，列出被排除的依赖构件集。即告诉maven你只依赖指定的项目，不依赖项目的依赖。此元素主要用于解决版本冲突问题-->  
   >                <exclusions>  
   >                 <exclusion>   
   >                        <artifactId>spring-core</artifactId>   
   >                        <groupId>org.springframework</groupId>   
   >                    </exclusion>   
   >                </exclusions>     
   >                <!--可选依赖，如果你在项目B中把C依赖声明为可选，你就需要在依赖于B的项目（例如项目A）中显式的引用对C的依赖。可选依赖阻断依赖的传递性。-->   
   >                <optional>true</optional>  
   >            </dependency>  
   >        </dependencies>  
   >        <!--不赞成使用. 现在Maven忽略该元素.-->  
   >        <reports></reports>  
   >        <!--该元素描述使用报表插件产生报表的规范。当用户执行“mvn site”，这些报表就会运行。 在页面导航栏能看到所有报表的链接。-->  
   >     <reporting>  
   >      <!--true，则，网站不包括默认的报表。这包括“项目信息”菜单中的报表。-->  
   >      <excludeDefaults/>  
   >      <!--所有产生的报表存放到哪里。默认值是${project.build.directory}/site。-->  
   >      <outputDirectory/>  
   >      <!--使用的报表插件和他们的配置。-->  
   >      <plugins>  
   >       <!--plugin元素包含描述报表插件需要的信息-->  
   >       <plugin>  
   >        <!--报表插件在仓库里的group ID-->  
   >        <groupId/>  
   >        <!--报表插件在仓库里的artifact ID-->  
   >        <artifactId/>  
   >        <!--被使用的报表插件的版本（或版本范围）-->  
   >        <version/>  
   >        <!--任何配置是否被传播到子项目-->  
   >        <inherited/>  
   >        <!--报表插件的配置-->  
   >        <configuration/>  
   >        <!--一组报表的多重规范，每个规范可能有不同的配置。一个规范（报表集）对应一个执行目标 。例如，有1，2，3，4，5，6，7，8，9个报表。1，2，5构成A报表集，对应一个执行目标。2，5，8构成B报表集，对应另一个执行目标-->  
   >        <reportSets>  
   >         <!--表示报表的一个集合，以及产生该集合的配置-->  
   >         <reportSet>  
   >          <!--报表集合的唯一标识符，POM继承时用到-->  
   >          <id/>  
   >          <!--产生报表集合时，被使用的报表的配置-->  
   >          <configuration/>  
   >          <!--配置是否被继承到子POMs-->  
   >          <inherited/>  
   >          <!--这个集合里使用到哪些报表-->  
   >          <reports/>  
   >         </reportSet>  
   >        </reportSets>  
   >       </plugin>  
   >      </plugins>  
   >     </reporting>  
   >     <!-- 继承自该项目的所有子项目的默认依赖信息。这部分的依赖信息不会被立即解析,而是当子项目声明一个依赖（必须描述group ID和 artifact ID信息），如果group ID和artifact ID以外的一些信息没有描述，则通过group ID和artifact ID 匹配到这里的依赖，并使用这里的依赖信息。-->  
   >     <dependencyManagement>  
   >      <dependencies>  
   >       <!--参见dependencies/dependency元素-->  
   >       <dependency>  
   >        ......  
   >       </dependency>  
   >      </dependencies>  
   >     </dependencyManagement>     
   >        <!--项目分发信息，在执行mvn deploy后表示要发布的位置。有了这些信息就可以把网站部署到远程服务器或者把构件部署到远程仓库。-->   
   >        <distributionManagement>  
   >            <!--部署项目产生的构件到远程仓库需要的信息-->  
   >            <repository>  
   >             <!--是分配给快照一个唯一的版本号（由时间戳和构建流水号）？还是每次都使用相同的版本号？参见repositories/repository元素-->  
   >       <uniqueVersion/>  
   >       <id>banseon-maven2</id>   
   >       <name>banseon maven2</name>   
   >                <url>file://${basedir}/target/deploy</url>   
   >                <layout/>  
   >      </repository>  
   >      <!--构件的快照部署到哪里？如果没有配置该元素，默认部署到repository元素配置的仓库，参见distributionManagement/repository元素-->   
   >      <snapshotRepository>  
   >       <uniqueVersion/>  
   >       <id>banseon-maven2</id>  
   >                <name>Banseon-maven2 Snapshot Repository</name>  
   >                <url>scp://svn.baidu.com/banseon:/usr/local/maven-snapshot</url>   
   >       <layout/>  
   >      </snapshotRepository>  
   >      <!--部署项目的网站需要的信息-->   
   >            <site>  
   >             <!--部署位置的唯一标识符，用来匹配站点和settings.xml文件里的配置-->   
   >                <id>banseon-site</id>   
   >                <!--部署位置的名称-->  
   >                <name>business api website</name>   
   >                <!--部署位置的URL，按protocol://hostname/path形式-->  
   >                <url>   
   >                    scp://svn.baidu.com/banseon:/var/www/localhost/banseon-web    
   >                </url>   
   >            </site>  
   >      <!--项目下载页面的URL。如果没有该元素，用户应该参考主页。使用该元素的原因是：帮助定位那些不在仓库里的构件（由于license限制）。-->  
   >      <downloadUrl/>  
   >      <!--如果构件有了新的group ID和artifact ID（构件移到了新的位置），这里列出构件的重定位信息。-->  
   >      <relocation>  
   >       <!--构件新的group ID-->  
   >       <groupId/>  
   >       <!--构件新的artifact ID-->  
   >       <artifactId/>  
   >       <!--构件新的版本号-->  
   >       <version/>  
   >       <!--显示给用户的，关于移动的额外信息，例如原因。-->  
   >       <message/>  
   >      </relocation>  
   >      <!-- 给出该构件在远程仓库的状态。不得在本地项目中设置该元素，因为这是工具自动更新的。有效的值有：none（默认），converted（仓库管理员从 Maven 1 POM转换过来），partner（直接从伙伴Maven 2仓库同步过来），deployed（从Maven 2实例部 署），verified（被核实时正确的和最终的）。-->  
   >      <status/>         
   >        </distributionManagement>  
   >        <!--以值替代名称，Properties可以在整个POM中使用，也可以作为触发条件（见settings.xml配置文件里activation元素的说明）。格式是<name>value</name>。-->  
   >        <poperties/>  
   >    </project>  </span>
   >    ```

2. [Spring Boot的启动器Starter详解](http://blog.csdn.net/chszs/article/details/50610474).

3. 新建一个spring boot项目:[link](http://blog.csdn.net/zaq12346zaqwsx/article/details/63337519).

4. [Spring boot入门](http://blog.csdn.net/lxhjh/article/details/51769968).

5. [Maven命令解析](http://blog.csdn.net/lxhjh/article/details/8935436)，

6. [Maven中setting的配置](http://blog.csdn.net/yiluoak_47/article/details/12068855/)

7. [spring的注解](http://blog.csdn.net/xyh820/article/details/7303330/).

   > 1. 数据类：@Component、@ConfigurationProperties(prefix = "gril")；使用时：@Autowired
   > 2. 配置内容的注入：@Value, @Component, @ConfigurationProperties

8. Spring.proprerties

   > 1. Spring.profiles.active使用不同的配置

9. Controller控制器的使用

   > 1. 注解
   >    1. @Controller：处理http请求
   >    2. @RestController：Spring4新加的注解，原来返回json需要@ResponseBody配合@Controller
   >    3. @RequestMapping：配置url映射
   >    4. @PathVariable：获取url的数据
   >    5. @RequestParam：获取请求参数的值：设置默认值：@RequestParam("id", required=false, defaultValue="0");
   >    6. @GetMapping：组合注解；相当于@RequestMapping(value = "", method=RequestMethod.GET);

10. [Mybatis使用](http://www.igouyu.com/html/fwdbc/MyBatis/3708.html).

11. [Lombok](http://blog.csdn.net/hack8/article/details/23790579)

12. [MyBatis Generator generatorConfig.xml配置详解](http://blog.csdn.net/pk490525/article/details/16819307).

13.  [@Repository、@Service、@Controller 和 @Component](http://www.iitshare.com/role-of-component-repository.html)

    > 1. @repository:通常用于注解DAO类，持久层
    >
    > 2. @Service:通常用于注解Service类，服务层
    >
    > 3. @controller:通常用于Controler类，控制层
    >
    > 4. @Component:通用注解：可用于任何Bean
    >
    > 5. @Scope:作用域：Singleton：容器单一、Propority：重新载入
    >
    > 6. @Autowired:“传统”的setter方法、可用于构造器或成员变量。
    >
    > 7. @Qualifier：选择指定的bean
    >
    > 8. @Bean标识一个用于配置和初始化一个由SpringIoc容器管理的新对象的方法。
    >
    >    ```java
    >    @Configuration
    >    public class Apponfig{
    >        @Bean
    >      	public MyService myservice() {
    >            return new MyServiceImpl();
    >        }
    >    }
    >    //相当于
    >    <beans>
    >    	<bean id="MyService" class="com.acam.services.MyService">
    >    </beans>
    >    ```
    >
    > 9. @Value注解:读取数据文件的数据
    >
    >    ```java
    >    @Configuration
    >    @ImportResource("classath:/com/acme/propities-config.xml")
    >    public class AppConfig{
    >        @Value("${jbbc.url}")
    >      	private String url;
    >    }
    >    ```
    >
    > 10. @PostConstruct、@PreDestory，初始化和销毁注解
    >
    > 11. @EnableAspectJAutoProxy:AspectJ的注解
    >
    > 12. @EnableAutoConfiguration表示让Spring Boot根据类路径中的jar包依赖为当前项目进行自动配置。
    >
    > 13. @RequestMapping:提供路由信息，他告诉spring任何来自“/”路径的HTTP请求都应该被映射到home方法
    >
    > 14. @RestController：告诉spring以字符串的形式渲染结果，并直接返回给调用者。
    >
    > 15. @Aspect:注解需要配合@Component注解使用，表示一个切面
    >
    > 16. @Pointcut:注解的方法返回值必须是void

14. service层处理业务逻辑，Dao数据库有关

15. AOP：面向切面编程。日志处理、事务处理、安全验证

    > 1. 实现方式：预编译：AspectJ、运行期动态代理：SpringAOP
    > 2. 切面，切点，根据切点来执行方法

16. spring事务管理

    > 1. 事务的特性：
    >    1. 原子性：事务中的操作要么全发生，要么全不发生
    >    2. 一致性：事务前后的数据完整性必须保持一致
    >    3. 隔离性：多个用户并发访问数据库时，一个用户的事务不能被其它用户的事务干扰，多个并发事务之间数据要相互隔离
    >    4. 持久性：一旦一个事务被提交，他对数据库中数据的改变时永久性的。
    > 2. 事务接口
    >    1. 事务管理器：PlatformTransactionManager
    >    2. 事务定义信息：TransactionDefinition
    >    3. 事务具体运行状态：TransactionStatus



Spring MVC的核心思想：业务数据抽取同业务数据呈现相分离。



### Spring MVC 拦截器：

1. 通过统一拦截从浏览器发往服务器的请求来完成功能的增强
2. 使用场景：解决请求的共性问题
3. 方法：
   1. preHandle是否拦截
   2. postHandle改变视图，或者发往视图的方法
   3. afterHandle响应之后的操作

拦截器与过滤器的区别

**①拦截器是基于java的反射机制的，而过滤器是基于函数回调。　　**

**②拦截器不依赖与servlet容器，过滤器依赖与servlet容器。　　**

**③拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用。　　**

**④拦截器可以访问action上下文、值栈里的对象，而过滤器不能访问。　　**

**⑤在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次。**

**⑥拦截器可以获取IOC容器中的各个bean，而过滤器就不行，这点很重要，在拦截器里注入一个service，可以调用业务逻辑。**



### 过滤器 Filter

1. 定义：是一个服务器端的组件，他可以截取用户端的请求与响应信息，并对这些信息过滤。
2. 工作原理：启动web容器时，过滤器就开始运作，用户端的请求先通过过滤器进行判断是否合理，之后交给服务器的web资源进行处理；资源响应发送至过滤器，过滤器在判断，过滤器将web资源额响应发送给用户
3. 生命周期：实例化（web.xml）、初始化（init（））、过滤（doFilter（））、销毁（destroy（））。
4. 配置实现。




### JavaEE个人理解

1. servlet配置，servlet中页面的跳转
2. tomcat将jsp转换为servlet，加入servlet容器中。




### Mybatis

1. 获得sqlSession:
   1. 通过配置文件获取数据库连接相关信息
   2. 通过配置信息构建SqlSessionFactory
   3. 通过SqlSessionFactory打开数据会话sqlSession





