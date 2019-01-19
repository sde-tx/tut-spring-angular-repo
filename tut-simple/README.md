* https://spring.io/guides/tutorials/spring-security-and-angular-js/

# Section: A Secure Single Page Application <br>

```
Root
 戌式式 simple
       戌式式 ui
```
- Create folder structure like above <br>
- Generate Spring project using Spring Boot Initializr with Web and Security <br>
- Extract it under simple <br>

- Add parent pom.xml under simple <br>
<details>
  <summary>pom.xml under simple</summary>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>org.test</groupId>
	<artifactId>simple</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>pom</packaging>
	<name>simple</name>
	<description>Demo project for Spring Boot</description>

	<modules>
		<module>ui</module>
	</modules>
</project>
```
</details>


- Edit pom.xml in ui to <br>
  ```
	look at parent pom.xml
	change packaging into jar
	add build command
	(update nodeVersion to v8.12.0)
  ```
<details>
  <summary>pom.xml under ui</summary>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>org.test</groupId>
	<artifactId>ui</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>ui</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.2.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>1.8</java.version>
    </properties>

    <build>
        <resources>
            <resource>
                <directory>${project.basedir}/src/main/resources</directory>
            </resource>
            <resource>
                <directory>${project.build.directory}/generated-resources</directory>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>com.github.eirslett</groupId>
                <artifactId>frontend-maven-plugin</artifactId>
                <version>1.6</version>
                <configuration>
                    <nodeVersion>v8.12.0</nodeVersion>
                </configuration>
                <executions>
                    <execution>
                        <id>install-npm</id>
                        <goals>
                            <goal>install-node-and-npm</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>npm-install</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>npm-build</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>run-script build</arguments>
                        </configuration>
                    </execution>
                    <execution>
                        <id>npm-test</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>run-script e2e</arguments>
                        </configuration>
                        <phase>test</phase>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>
```
</details>

- Create two files under ui <br>
```
ng:
#!/bin/sh
cd $(dirname $0)
PATH="$PWD/node/":$PATH
./node_modules/@angular/cli/bin/ng "$@"

npm:
#!/bin/sh
cd $(dirname $0)
PATH="$PWD/node/":$PATH
node "node/node_modules/npm/bin/npm-cli.js" "$@"
```

- Install angular-cli (if not installed) <br>
npm install @angular/cli <br>

- Check Node version used by Angular Cli and update nodeVersion above if above version is lower than this <br>
- Create Angular App under ui <br>
ng new client # add <br>

- Execute jobs below under ui: <br>
```
remove client/node*, client/src/favicon.ico, client/.gitignore, client/.git
open angular.js and replace "outputPath": "dist/client" into "outputPath": "target/classes/static"
copy all remainings in client to ui
remove client
```

- Execute maven commands below for multi module project under simple <br>
```
mvn -N io.takari:maven:wrapper
mvnw clean install
mvnw spring-boot:run
```