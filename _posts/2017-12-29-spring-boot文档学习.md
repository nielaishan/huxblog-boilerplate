---
layout:   post
title:    "spring boot文档学习 一"
subtitle: "mybatis和配置文件properties"
date:     2017-12-29
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - spring boot
---

###Application属性文件

SpringApplication将从以下位置加载，application.properties文件，并将他们添加到Environment。

1. 当前目录下的一个/config目录下
2. 当前目录
3. 一个classpath下的config目录下
4. classpath根目录下

这个是按优先级排列的，优先级高的覆盖位置低的。

当然如果不喜欢application.properties作为配置文件名，可以通过spring.config.name环境属性来切换其他的名称。

bootstrap.properties由父Spring ApplicationContext加载。父ApplicationContext被加载到使用application.properties的之前。所以该文件中可以通过spring.config.name，说明配置文件名，可以包含路径。

```xml
spring.config.location=classpath:/application-common.properties,/data/conf/rrxfas/server.properties
```

**注：yaml文件不能通过@PropertySource注解加载，所以在此情况下，不能使用yaml文件，而用property文件**



#### 类型安全的配置属性

使用@Value({"property"})注解注入配置有时比较笨重，特别是需要使用多个property或你的数据比较有层次结构。为了控制和校验你的应用配置，Spring boot提供一个允许强类型beans的替代方法来使用property。

```Java
@Component
@ConfigurationProperties(prefix="connecttion")
public class ConnectConfig {
    private String username;
  	private InetAddress remoteAddress;
}

# application.yml
connection:
    username: admin
    remoteAddress: 192.168.1.1
# additional configuration as required”

@Service
public class MyService {
    @Autowired
    private ConnectionSettings connection;
     //... 
    @PostConstruct
    public void openConnection() {
        Server server = new Server();
        this.connection.configure(server);
    }
}


//你可以通过在@EnableConfigurationProperties注解中直接简单的列出属性类来快捷的注册@ConfigurationProperties bean的定义。
@Configuration
@EnableConfigurationProperties(ConnectionSettings.class)
public class MyConfiguration {
}
  
```

为了使用@ConfigurationProperties beans，你可以使用与其他任何bean相同的方式注入它们

#### Profile

Spring Profiles提供了一种隔离应用程序配置的方式，并让这些配置只能在特定的环境下生效。任何@Component或@Configuration都能被@Profile标记，从而限制加载它的时机。

```Java
@Configuration
@Profile("production")
public class ProductionConfiguration {
    // ...
}
```

**注：tomcat只支持war的打包方式，不支持可执行的jar。**



### Mybatis

1. dependency mybatis依赖配置在pom.xml

   ```Xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   	<modelVersion>4.0.0</modelVersion>
   	<!--项目的全球唯一标识符，通常使用全限定的包名区分该项目和其他项目。并且构建时生成的路径也是由此生成， 如com.mycompany.app生成的相对路径为：/com/mycompany/app-->  
   	<groupId>com.example</groupId>
     	<!-- 构件的标识符，它和group ID一起唯一标识一个构件。换句话说，你不能有两个不同的项目拥有同样的artifact ID和groupID；在某个 特定的group ID下，artifact ID也必须是唯一的。构件是项目产生的或使用的一个东西，Maven为项目产生的构件包括：JARs，源 码，二进制发布和WARs等。-->
   	<artifactId>demo</artifactId>
   	<version>0.0.1-SNAPSHOT</version>
     	<!--项目产生的构件类型，例如jar、war、ear、pom。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型--> 
   	<packaging>jar</packaging>
   	 <!--项目的名称, Maven产生的文档用--> 
   	<name>demo</name>
   	<description>Demo project for Spring Boot</description>
     
   	<!--父项目的坐标。如果项目中没有规定某个元素的值，那么父项目中的对应值即为项目的默认值。 坐标包括group ID，artifact ID和 version。-->
   	<parent>
   		<groupId>org.springframework.boot</groupId>
   		<artifactId>spring-boot-starter-parent</artifactId>
   		<version>1.5.9.RELEASE</version>
         	<!-- 父项目的pom.xml文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项 目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom。-->
   		<relativePath/> <!-- lookup parent from repository -->
   	</parent>
   	<!-- 项目属性 -->
   	<properties>
   		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
   		<java.version>1.7</java.version>
   		<lombok.version>1.16.18</lombok.version>
   	</properties>
   	<!-- 项目依赖 -->
   	<dependencies>
         <!-- Spring Boot的启动器Starter详解：http://blog.csdn.net/chszs/article/details/50610474 -->
         	<!--添加spring-web包 -->
   		<dependency>
   			<groupId>org.springframework.boot</groupId>
             	<!--支持全栈式Web开发，包括Tomcat和spring-webmvc。-->
   			<artifactId>spring-boot-starter-web</artifactId>
   		</dependency>
   		<!--支持常规的测试依赖，包括JUnit、Hamcrest、Mockito以及spring-test模块-->
   		<dependency>
   			<groupId>org.springframework.boot</groupId>
   			<artifactId>spring-boot-starter-test</artifactId>
   			<scope>test</scope>
   		</dependency>

   		<dependency>
   			<groupId>org.springframework.boot</groupId>
             	<!--帮助监控和管理应用-->
   			<artifactId>spring-boot-starter-actuator</artifactId>
   		</dependency>
         <dependency>
        <!-- mybatis-spring-boot-starter依赖的作用：只需要定义一个DataSource即可，它会自动创建使用该DataSource的SqlSessionFactoryBean以及SqlSessionTemplate。会自动扫描你的Mappers，连接到SqlSessionTemplate，并注册到Spring上下文中。 -->
        <groupId>org.mybatis.spring.boot</groupId>
      			<artifactId>mybatis-spring-boot-starter</artifactId>
      			<version>1.1.1</version>
      		</dependency>
            
      		<!-- 添加mybatis的核心包 -->
      		<dependency>
      			<groupId>org.mybatis</groupId>
      			<artifactId>mybatis</artifactId>
      			<version>3.4.1</version>
      		</dependency>
      		<!-- 添加mybatis与Spring整合的核心包 -->
      		<dependency>
      			<groupId>org.mybatis</groupId>
      			<artifactId>mybatis-spring</artifactId>
      			<version>1.3.0</version>
      		</dependency>
      		<!--lombok插件依赖，@Data，设置seter，geter函数-->
      		<dependency>
      			<groupId>org.projectlombok</groupId>
      			<artifactId>lombok</artifactId>
      			<version>${lombok.version}</version>
      		</dependency>
      		<!-- 添加mysql驱动包 -->
      		<dependency>
      			<groupId>mysql</groupId>
      			<artifactId>mysql-connector-java</artifactId>
      		</dependency>
      		<!-- 添加druid连接池包，主要是为了提高数据库操作性能 -->
      		<dependency>
      			<groupId>com.alibaba</groupId>
      			<artifactId>druid</artifactId>
      			<version>1.0.18</version>
      		</dependency>
      		<!-- 添加servlet3.0核心包 -->
      		<dependency>
      			<groupId>javax.servlet</groupId>
      			<artifactId>javax.servlet-api</artifactId>
      			<scope>provided</scope>
      		</dependency>
      	</dependencies>

      	<!--构建项目需要的信息-->
      	<build>
         <plugins>
      			<plugin>
      				<groupId>org.springframework.boot</groupId>
      				<artifactId>spring-boot-maven-plugin</artifactId>
      			</plugin>
      		</plugins>
      	</build>
      </project>

   <!--2. application.properties文件配置 -->

      //主要是druid连接池的配置
      jdbc.driver=com.mysql.jdbc.Driver
      jdbc.url=jdbc:mysql://localhost:3306/newsreport?useUnicode=true&amp;characterEncoding=UTF-8
      jdbc.username=root
      jdbc.password=12345678
      jdbc.pool.minIdle=0
      jdbc.pool.maxIdle=10
      jdbc.pool.maxActive=50
   ```


3. Domain层

   ```Java
   package com.example.demo.dao.domain;

   import lombok.Data;

   @Data
   public class Admin {
       private Integer id;
       private String username;
       private String password;
   }
   ```

4. dao层

   ```Java
   package com.example.demo.dao.dao;

   import com.example.demo.dao.domain.Admin;
   import org.apache.ibatis.annotations.Param;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface AdminDao {
       Admin selectById(@Param("id") Integer Id);
   }
   ```

5. 现在设置Mapper文件，在resourse目录下创建mybatis文件夹，在这下面主要是存储mapper

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

   <!-- namespace必须指向Dao接口 -->
   <mapper namespace="com.example.demo.dao.dao.AdminDao">
       <resultMap id="BaseResultMap" type="com.example.demo.dao.domain.Admin">
           <id column="id" property="id"/>
           <result column="username" property="username" />
           <result column="password" property="password"/>
       </resultMap>

       <select id="selectById" resultMap="BaseResultMap">
           select id, username, password
           from admin
           where id = #{id}
       </select>
   </mapper>
   ```

6. 在resource文件下创建applicationContext.xml文件，applicationContext.xml的作用主要就是配置连接池，以及数据源的bean、adminSqlSessionFactory

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

       <bean id="adminDataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init"
             destroy-method="close" primary="true">
           <property name="url" value="${jdbc.url}" />
           <property name="username" value="${jdbc.username}" />
           <property name="password" value="${jdbc.password}" />

           <property name="maxActive" value="10" />
           <property name="minIdle" value="0" />
           <property name="defaultAutoCommit" value="false" />
       </bean>

       <bean id="adminSqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="mapperLocations" value="classpath*:mybatis/*.xml"/>
           <property name="dataSource" ref="adminDataSource"/>
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
       </bean>

       <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
           <property name="basePackage" value="com.example.demo.dao.dao"/>
           <property name="sqlSessionFactoryBeanName" value="adminSqlSessionFactory"/>
       </bean>
   </beans>
   ```

7. 还有一个mybatis-config.xml文件，主要是配置mybatis中Mapper，JavaBean实体类属性命的自动驼峰命名转换

   ```Xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">

   <configuration>
       <settings>
           <setting name="mapUnderscoreToCamelCase" value="true"/>
       </settings>
   </configuration>
   ```

   ​