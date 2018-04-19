CheckStyle配置及使用
===
[CheckStyle](http://checkstyle.sourceforge.net/ "CheckStyle")是SourceForge下的一个项目，提供了一个帮助JAVA开发人员遵守某些编码规范的工具。它能够自动化代码规范检查过程，从 而使得开发人员从这项重要，但是枯燥的任务中解脱出来。


与IDEA集成
---
### 安装插件
1. 在线安装
![idea install checkstyle plugin](/talywy/codestyle/blob/master/checkstyle/images/idea-install-checkstyle.png?raw=true "idea install checksytle plugin")

2. 离线安装
到[CheckStyle-IDEA插件官网](https://plugins.jetbrains.com/plugin/1065 "CheckStyle-IDEA")或[这里](/talywy/codestyle/blob/master/checkstyle/plugins/checkstyle-idea-4.21.2.zip?raw=true "checkstyle-idea-4.21.2.zip")下载插件插件包，然后在安装插件是选择从本地磁盘安装。
![install from local disk](/talywy/codestyle/blob/master/checkstyle/images/idea-install-checkstyle-local.png?raw=true)


### 增加checkstyle检查规则
![idea add checkstyle rules](/talywy/codestyle/blob/master/checkstyle/images/idea-checkstyle-rules.png?raw=true "idea add checkstyle rules")

### 使用

1. 手动触发代码检查
![check source code](/talywy/codestyle/blob/master/checkstyle/images/idea-check.png?raw=true "check source code")
在源码文件中`单击右键`，选择`Check Current File`即可进行代码检查分析。同时可以在`CheckStyle Scan`窗口中选择`Rules`来使用不同的检查规则。

2. 实时自动检查
![check real-time](/talywy/codestyle/blob/master/checkstyle/images/checkstyle-realtime-scan.png?raw=true "check real-time")
Settings->Editor->Inspections->Checkstyle , 选中`Checkstyle real-time scane`(默认是选中的)，即可打开实时检查功能。同时可以在此处设置检查报错的等级。

3. 配置IDEA自动调整import包顺序
![import setting](/talywy/codestyle/blob/master/checkstyle/images/checkstyle-import.png?raw=true "import setting")
可以按照上图在IDEA中设置包导入的顺序，配置好之后可在代码中使用optimize-import命令实现包引入顺序的自动调整，如下图：
![optimize import](/talywy/codestyle/blob/master/checkstyle/images/optimize-import.png?raw=true "optimize import")

为了便于集成，提供了配置好的IDEA设置，可以在[此处下载](/talywy/codestyle/blob/master/checkstyle/configs/settings-idea-codestyle.jar?raw=true), 下载完之后File->Import Settings来进行导入。

与Maven集成
---
在项目的pom.xml中配置以下内容

```
<reporting>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>2.17</version>
            <configuration>
                <configLocation>../../edu_java_checks_cn.xml</configLocation>
            </configuration>
            <reportSets>
                <reportSet>
                    <reports>
                        <report>checkstyle</report>
                    </reports>
                </reportSet>
            </reportSets>
        </plugin>
    </plugins>
</reporting>
```
使用`mvn site`命令生成项目文档网站，成成的报告位置为：target/site/checkstyle.html，报告样式如下:


建议可在项目的DailyBuild中增加报告自动邮件发送，以帮助持续改进代码规范，提高代码质量
![check-report-1](/talywy/codestyle/blob/master/checkstyle/images/check-report-1.png?raw=true)
![check-report-2](/talywy/codestyle/blob/master/checkstyle/images/check-report-2.png?raw=true)

更多插件使用说明，请参考：[Maven Checkstyl官方使用说明](http://maven.apache.org/plugins/maven-checkstyle-plugin/usage.html)

与Eclipse集成
---

为了统一教育事业部Java编码规范，基于[Google Java Style](https://google.github.io/styleguide/javaguide.html) 编写了两个检查配置文件供日常研发使用:

* [java_checks_cn.xml](/talywy/codestyle/blob/master/checkstyle/configs/java_checks_cn.xml) 中文提示配置检查
* [java_checks_en.xml](/tlaywy/codestyle/blob/master/checkstyle/configs/java_checks_en.xml) 英文提示配置检查
* [settings-idea-codestyle.jar](http://tech.edu.iflytek.com/talywy/codestyle/blob/master/checkstyle/configs/settings-idea-codestyle.jar?raw=true) IDEA包导入规则配置
