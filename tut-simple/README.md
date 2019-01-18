* https://spring.io/guides/tutorials/spring-security-and-angular-js/

# Section: 

- Create root folder

- Create folder for simple project
Root

戌式式 simple

- Generate Spring project using  Spring Boot Initializr with Web and Security

- Extract it under simple
Root
 戌式式 simple
		戌式式 ui

- Add parent pom.xml under simple
<details>
  <summary>pom.xml under simple</summary>

<dl>
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
</dl>
</details>


- Edit pom.xml in ui to
	look at parent pom.xml
	change packaging into jar
	add build command
	(update nodeVersion to v8.12.0)

- Create two files under ui
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

- Install angular-cli (if not installed)
npm install @angular/cli

- Check Node version used by Angular Cli and update nodeVersion above if above version is lower than this

- Create Angular App under ui
ng new client # add

- Execute jobs below under ui:
remove client/node*, client/src/favicon.ico, client/.gitignore, client/.git
open angular.js and replace "outputPath": "dist/client" into "outputPath": "target/classes/static"
copy all remainings in client to ui
remove client

- Execute maven commands below for multi module project under simple
mvn -N io.takari:maven:wrapper
mvnw clean install
mvnw spring-boot:run
