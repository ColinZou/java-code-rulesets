# Java代码规则库
## 一、目的
方便不同项目引用Java代码检测的PMD规则与findbugs排除规则。
## 二、使用方法
### 1. 添加maven仓库 
在pom.xml当中添加如下仓库地址

```xml
<repositories>
    <repository>
        <id>oss.sonatype.org</id>
        <name>Sona Type OSS</name>
        <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
        <releases>
            <enabled>false</enabled>
        </releases>
    </repository>
</repositories>
```
### 2. PMD配置
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-pmd-plugin</artifactId>
    <version>3.7</version>
    <dependencies>
        <dependency>
            <groupId>com.stableforever</groupId>
            <artifactId>java-code-rulesets</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
    </dependencies>
    <configuration>
        <linkXRef>true</linkXRef>
        <language>java</language>
        <failOnViolation>true</failOnViolation>
        <failurePriority>3</failurePriority>
        <skipEmptyReport>true</skipEmptyReport>
        <rulesets>
            <ruleset>/rulesets/java/default-ruleset.xml</ruleset>
        </rulesets>
    </configuration>
</plugin>
```
### 3. findbugs配置
```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>findbugs-maven-plugin</artifactId>
    <version>${findbugs.version}</version>
    <dependencies>
        <dependency>
            <groupId>com.stableforever</groupId>
            <artifactId>java-code-rulesets</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
    </dependencies>
    <configuration>
        <xmlOutput>true</xmlOutput>
        <findbugsXmlOutput>true</findbugsXmlOutput>
        <effort>Max</effort>
        <failOnError>true</failOnError>
        <excludeFilterFile>/findbugs/findbugs-exclude.xml</excludeFilterFile>
        <plugins>
            <plugin>
                <groupId>com.mebigfatguy.fb-contrib</groupId>
                <artifactId>fb-contrib</artifactId>
                <version>7.4.5</version>
            </plugin>
        </plugins>
    </configuration>
</plugin>
```