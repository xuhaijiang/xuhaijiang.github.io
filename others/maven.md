#### maven

##### maven属性
- 内置属性


    ${base} 项目根目录
    ${version}


- POM属性


    ${project.artifactId}对应了project>artifactId元素的值
    ${project.build.directory} 构建目录，默认为target
    ${project.build.outputDirectory} 构建过程输出目录，默认为target/classes
    ${project.build.finalName} 产出物名称，默认为${project.artifactId}-${project.version}
    ${project.packaging} 打包类型，默认为jar
    ${project.xxx} 当前pom文件的任意节点内容
    
- 自定义属性

在pom中 properties 元素下自定义的Maven属性。
例如:

    <project>  
        <properties>  
            <xhj.version>xhj.1.0</xhj.version>  
        </properties>  
    </project> 


- Settings属性


    ${settings.localRepository}


- Java系统属性


    ${user.home}
    
        
- 环境变量属性


    ${env.JAVA_HOME}
    通过命令行mvn help:system查看所有环境变量

##### 自定义的 jar 到 Maven 的本地资源库

	mvn install:install-file -Dfile=e:\kaptcha-2.3.2.jar -DgroupId=com.google.code -DartifactId=kaptcha -Dversion=2.3.2 -Dpackaging=jar

##### Maven 编译器插件

	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>2.3.2</version>
		<configuration>
			<source>1.6</source>
			<target>1.6</target>
		</configuration>
	</plugin>

##### 添加外部依赖项中，使用下列方式到Maven的pom.xml

	<dependency>
	 <groupId>ldapjdk</groupId>
	 <artifactId>ldapjdk</artifactId>
	 <scope>system</scope>
	 <version>1.0</version>
	 <systemPath>${basedir}src/lib/ldapjdk.jar</systemPath>
	</dependency>

##### Maven 打包

	mvn package

##### 本地jar，导入到maven中

	mvn install:install-file -DgroupId=org.roof -DartifactId=roof-web-org-service-api -Dversion=3.0.1 -Dpackaging=jar -Dfile=F:\SVNClient\Company\public\develop\dome\repository\org\roof\roof-web-org-service-api\3.0.1\roof-web-org-service-api-3.0.1.jar





#####	设定主仓库，按设定顺序进行查找
	<repositories>
		<!-- 如有Nexus私服，取消注释并指向正确的服务器地址。 -->
		<repository> 
			<id>nexus-repos</id>
		 	<name>Team Nexus Repository</name> 
			<url>http://192.168.11.36:8888/nexus/content/groups/public</url> 
		</repository> 

		<repository>
			<id>oschina-repos</id>
			<name>Oschina Releases</name>
			<url>http://maven.oschina.net/content/groups/public</url>
		</repository>
	</repositories>


##### 设定插件仓库 
	<pluginRepositories>
		<!-- 如有Nexus私服，取消注释并指向正确的服务器地址。 -->
		<pluginRepository>
 			<id>nexus-repos</id> 
			<name>Team Nexus Repository</name>
		 	<url>http://192.168.11.36:8888/nexus/content/groups/public</url> 
		</pluginRepository> 

		<pluginRepository>
			<id>oschina-repos</id>
			<name>Oschina Releases</name>
			<url>http://maven.oschina.net/content/groups/public</url>
		</pluginRepository>

	</pluginRepositories>

	
##### pom.xml 的配置方案：

 	<repositories>
        <repository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots><enabled>true</enabled></snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-snapshots</id>
            <url>http://repo.spring.io/snapshot</url>
        </pluginRepository>
        <pluginRepository>
            <id>spring-milestones</id>
            <url>http://repo.spring.io/milestone</url>
        </pluginRepository>
    </pluginRepositories>

##### setting

	<mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    <mirror>
        <id>central</id>
        <name>Maven Repository Switchboard</name>
        <url>http://repo1.maven.org/maven2/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    <mirror>
        <id>repo2</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://repo2.maven.org/maven2/</url>
    </mirror>
    <mirror>
        <id>ibiblio</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://mirrors.ibiblio.org/pub/mirrors/maven2/</url>
    </mirror>
    <mirror>
        <id>jboss-public-repository-group</id>
        <mirrorOf>central</mirrorOf>
        <name>JBoss Public Repository Group</name>
        <url>http://repository.jboss.org/nexus/content/groups/public</url>
    </mirror>
    <!-- 中央仓库在中国的镜像 -->
    <mirror>
        <id>maven.net.cn</id>
        <name>oneof the central mirrors in china</name>
        <url>http://maven.net.cn/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
  
  
  
  
  
  
  
  
  
  
  
  
  