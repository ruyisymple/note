# Springboot入门

### 1、系统要求

- Java 8 & 兼容java14 .
- Maven 3.3+
- idea 2019.1.2

#### 1.1、maven设置

**注意更改本地仓库resposity的位置一定要在配置文件setting.xml中修改**

```xml
<mirrors>
      <mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
  </mirrors>
 
  <profiles>
         <profile>
              <id>jdk-1.8</id>
              <activation>
                <activeByDefault>true</activeByDefault>
                <jdk>1.8</jdk>
              </activation>
              <properties>
                <maven.compiler.source>1.8</maven.compiler.source>
                <maven.compiler.target>1.8</maven.compiler.target>
                <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
              </properties>
         </profile>
  </profiles>
```

### 2、HelloWorld

需求：浏览发送/hello请求，响应 Hello，Spring Boot 2 

#### 2.1、创建maven工程

#### 2.2、引入依赖

在pom.xml中添加以下

```

<parent>
﻿
        <groupId>org.springframework.boot</groupId>
﻿
        <artifactId>spring-boot-starter-parent</artifactId>
﻿
        <version>2.3.4.RELEASE</version>
﻿
    </parent>
﻿
​
﻿
​
﻿
    <dependencies>
﻿
        <dependency>
﻿
            <groupId>org.springframework.boot</groupId>
﻿
            <artifactId>spring-boot-starter-web</artifactId>
﻿
        </dependency>
﻿  </dependencies>
﻿
```

#### 2.3、创建主程序

在src-main-java中创建com.cms.boot.MainApplication

```
/**

 * 主程序类

 * @SpringBootApplication：这是一个SpringBoot应用
    */
    @SpringBootApplication
    public class MainApplication {

    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
  }
```

#### 2.4、编写业务

创建com.cms.boot.controller.HelloController

```
//@Controller和@RespondBody的结合
@RestController
public class HelloController {

//路径
    @RequestMapping("/hello")
    public String handle01(){
        return "Hello, Spring Boot 2!";
    }


}
```

#### 2.5、测试

直接运行main方法

#### 2.6、简化配置

在resources下新建 application.properties

在里面可以配置官方公布的配置如

```
server.port=8888
```

#### 2.7、简化部署

在pom.xml中添加插件

```
 <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.3.4.RELEASE</version> //对应springboot的版本号
            </plugin>
        </plugins>
    </build>
```

然后点击mvn -clean 和 mvn -package即可将项目打包成可执行jar包，直接在目标服务器执行即可。

在target中可以看到已经打包好的jar包，右键target在本地文件夹中打开

进入cmd中，使用 java -jar + 刚打包的jar包的名字（使用tab键就可显示），即可运行tomcat项目

注意点：

- 取消掉cmd的快速编辑模式

### 3、自动配置

#### 3.1、spring boot的特点

##### 3.1.1、依赖管理

- **父项目做依赖管理**

```
依赖管理    
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
</parent>

他的父项目
 <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.4.RELEASE</version>
  </parent>

几乎声明了所有开发中常用的依赖的版本号,自动版本仲裁机制
```

- **开发导入starter场景启动器**

```
1、见到很多 spring-boot-starter-* ： *就某种场景
2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
3、SpringBoot所有支持的场景
https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter
4、见到的  *-spring-boot-starter： 第三方为我们提供的简化开发的场景启动器。
5、所有场景启动器最底层的依赖
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter</artifactId>
  <version>2.3.4.RELEASE</version>
  <scope>compile</scope>
</dependency>
```

- **无需关注版本号，自动版本仲裁**

```
1、引入依赖默认都可以不写版本
2、引入非版本仲裁的jar，要写版本号。
```

- **可以修改默认版本号**

```
1、查看spring-boot-dependencies里面规定当前依赖的版本 用的 key。
2、在当前项目里面重写配置
    <properties>
        <mysql.version>5.1.43</mysql.version>
    </properties>
```

##### 3.1.2、自动配置

- 自动配好Tomcat

  引入Tomcat依赖。

  配置Tomcat


```
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
 </dependency>
```

- 自动配好SpringMVC

  引入SpringMVC全套组件

  自动配好SpringMVC常用组件（功能）

  自动配好Web常见功能，如：字符编码问题

  SpringBoot帮我们配置好了所有web开发的常见场景

- 默认的包结构

  主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来

  无需以前的包扫描配置

  想要改变扫描路径，@SpringBootApplication(scanBasePackages=**"com.atguigu"**)

  或者@ComponentScan 指定扫描路径

  ```
  @SpringBootApplication(scanBasePackages="com.atguigu")
  等同于
  @SpringBootConfiguration
  @EnableAutoConfiguration
  @ComponentScan("com.atguigu.boot")
  ```

- 各种配置拥有默认值

  默认配置最终都是映射到某个类上，如：MultipartProperties

  配置文件的值最终会绑定每个类上，这个类会在容器中创建对象

- 按需加载所有自动配置项

  非常多的starter

  引入了哪些场景这个场景的自动配置才会开启

  SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面

  

- ......

#### 3.2、容器功能

##### 3.2.1、组件添加

###### 1、@Configuration

- 基本使用
- **Full模式与Lite模式**

- - 示例
  - 最佳实战

- - - 配置 类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断
    - 配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式