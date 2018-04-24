---
layout: post
title:  "在Jenkins中用SonarQube获取Java项目的代码覆盖率"
date:   2017-07-07
tags: Jenkins SonarQube Java coverage
---
**前提条件**
1. 在Jenkins中配置好了SonarQube Server和SonarQube Scanner
1. 代码中已经按照Maven的目录结构要求放好了JUnit单元测试代码
1. 通常这一步可选：在pom文件中设定了JaCoCo相关的内容，参照JaCoCo官方文档中的例子。

**操作步骤**
1. 新建一个自由风格(free style)的Jenkins任务
1. 指定运行的机器(Restrict where this project can be run)
1. 在“源码管理”设置中设置相关的仓库(Repositories)和分支
1. 在“构建”步骤中，选择“增加构建步骤”->“Execute shell"
1. 在Execute shell这一步的Command文本框中，添加以下代码
```shell
M2_HOME=/opt/maven
PATH=$PATH:$M2_HOME/bin
mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=true
```
注意，不同的机器上，可能Maven的目录有所变化。这一步是用JaCoCo插件，在target目录下生成jacoco.exec这一覆盖率文件。如果是多模块的Maven项目，则在各个模块的target下生成jacoco.exec。
1. 继续“增加构建步骤”，选择“Execute SonarQube Scanner”，在Anaysis properties中添加以下设置
```shell
sonar.projectKey=${JOB_NAME}
sonar.sources=./src/main
sonar.language=java
sonar.jacoco.reportPaths=target/jacoco.exec
sonar.java.binaries=target/classes
```
其中，多模块Maven项目的sonar.sources, sonar.jacoco.reportPaths和sonar.java.binaries设置需要按照子模块的路径添加，并用逗号隔开。
1. 保存任务并构建，之后查看当次结果的SonarQube分析链接。

**示例任务**
1. 非流水线，build部分，Execute shell一栏填入
    ```shell
    M2_HOME=/opt/maven
    PATH=$PATH:$M2_HOME/bin
    mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=true 
    ```
Execute SonarQube Scanner的Analysis properties一栏填入
    ```ini
    sonar.projectKey=${JOB_NAME}
    sonar.sources=./src/main/java/com/example/project/service
    sonar.language=java
    sonar.jacoco.reportPaths=target/jacoco.exec
    sonar.java.binaries=target/classes
    ```
1. 流水线
```groovy
node('node_name') {
   stage('Preparation') { // for display purposes
      // clean workspace
      cleanWs()
      // check out code
      git credentialsId: 'xxxx', url: 'http://xxxx.yyy/zzz.git'
   }
   stage('Generate coverage report') {
      // Run the maven build
      // ignore failed unit test by Maven
      sh "/opt/maven/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=true"
   }
   stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool '209_docker_sonarqb_scanner';
    withSonarQubeEnv('SonarQB') {
      sh "${scannerHome}/bin/sonar-scanner -Dsonar.language=java -Dsonar.projectKey=${JOB_NAME} -Dsonar.jacoco.reportPaths=target/jacoco.exec -Dsonar.tests=./src/test -Dsonar.java.coveragePlugin=jacoco -Dsonar.java.binaries=target/classes -Dsonar.sources=./src/main"
    }
  }
   stage('Results') {
       junit '**/target/surefire-reports/TEST-*.xml'
       // skip archiving to save disk space
       // archive 'target/*.war'
   }
   stage('Notification') {
       emailext body: '${JELLY_SCRIPT,template="html"}', recipientProviders: [[$class: 'RequesterRecipientProvider']], subject: '$DEFAULT_SUBJECT', to: '$DEFAULT_RECIPIENTS'
   }
}
```