# flywayForPostgres
postgresのDBマイグレーション用flywayプロジェクト

前提条件

以下のツールがインストール済みであること

- gradle（バージョンはできれば最新で）

<br>

1. ローカル環境でgradleコマンドを実行してプロジェクトを作成

2. repositoryとなるディレクトリを切る


```shell:事前準備
# mkdir flyway
# cd flyway
# grade init
```

<br>

3. これで雛形が完成したので、build.gradleを編集する

記載内容は以下のような感じ

```gradle:設定ファイル
// Apply the java plugin to add support for Java
apply plugin: 'java'
apply plugin: 'org.flywaydb.flyway'

// In this section you declare where to find the dependencies of your project
repositories {
    // Use 'jcenter' for resolving your dependencies.
    // You can declare any Maven/Ivy/file repository here.
    jcenter()
}

// In this section you declare the dependencies for your production and test code
dependencies {
    // The production code uses the SLF4J logging API at compile time
    compile 'org.slf4j:slf4j-api:1.7.21'
    // この辺は適宜変更
    compile group: 'org.postgresql', name: 'postgresql', version: '9.3-1100-jdbc4'
    
    // Declare the dependency for your favourite test framework you want to use in your tests.
    // TestNG is also supported by the Gradle Test task. Just change the
    // testCompile dependency to testCompile 'org.testng:testng:6.8.1' and add
    // 'test.useTestNG()' to your build script.
    testCompile 'junit:junit:4.12'
}

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.flywaydb:flyway-gradle-plugin:3.2.1'
    }
}

repositories {
    mavenCentral()
}

flyway {
    // for local
    url='jdbc:postgresql://localhost:5432/mydb_ps'
    user='mydb_ps'
    password='mydb_ps'
    schemas = ['mydb_ps']
}
```

