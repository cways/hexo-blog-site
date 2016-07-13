---
title: 使用MyBatis Generator自动创建代码
date: 2016-07-13 23:03:10
categories:
- Mybatis
tags: 
- JAVA
- MyBatis
---

生成代码需要的文件和jar包

```

generatorConfig.xml
mybatis-*.jar
mybatis-generator-core-*.jar
mysql-connector-java-*.jar

```

其中有mybatis框架的jar包，数据库驱动程序jar包和mybatis生成器jar包。其中的generatorConfig.xml是需要配置的文件，配置如下：

```

<?xml version="1.0" encoding="UTF-8"?/> 
<!DOCTYPE generatorConfiguration  
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"  
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd"/> 
<generatorConfiguration/> 
<!-- 数据库驱动--/> 
    <classPathEntry  location="mysql-connector-java-5.1.25-bin.jar"/> 
    <context id="DB2Tables"  targetRuntime="MyBatis3"/> 
        <commentGenerator/> 
            <property name="suppressDate" value="true"/> 
            <!-- 是否去除自动生成的注释 true：是 ： false:否 --/> 
            <property name="suppressAllComments" value="true"/> 
        </commentGenerator/> 
        <!--数据库链接URL，用户名、密码 --/> 
        <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://125.221.1.1/db_124" userId="dem" password="dem"/> 
        </jdbcConnection/> 
        <javaTypeResolver/> 
            <property name="forceBigDecimals" value="false"/> 
        </javaTypeResolver/> 
        <!-- 生成模型的包名和位置--/> 
        <javaModelGenerator targetPackage="test.domain" targetProject="src"/> 
            <property name="enableSubPackages" value="true"/> 
            <property name="trimStrings" value="true"/> 
        </javaModelGenerator/> 
        <!-- 生成映射文件的包名和位置--/> 
        <sqlMapGenerator targetPackage="test.mapping" targetProject="src"/> 
            <property name="enableSubPackages" value="true"/> 
        </sqlMapGenerator/> 
        <!-- 生成DAO的包名和位置--/> 
        <javaClientGenerator type="XMLMAPPER" targetPackage="test.IDao" targetProject="src"/> 
            <property name="enableSubPackages" value="true"/> 
        </javaClientGenerator/> 
        <!-- 要生成的表 tableName是数据库中的表名或视图名 domainObjectName是实体类名--/> 
        <table tableName="user_info_t" domainObjectName="User" enableCountByExample="false" 
            enableUpdateByExample="false" enableDeleteByExample="false" 
            enableSelectByExample="false" selectByExampleQueryId="false">
        </table>
    </context/> 
</generatorConfiguration/> 

```

当以上操作完成，只需要打开控制台，执行脚本：

```
java -jar mybatis-generator-core-*.jar -configfile generatorConfig.xml -overwrite
```

这样生成后，就可以在src目录下找到相应的文件夹，每个表都对应三个文件（实体类、接口、配置文件）。
