## 运维后台框架

全新打造的运维平台。框架命名：**`yw-framework`**。 所有模块的包名开头均为**`com.winway`**。 第三级别为模块名。

###技术路线
* shiro
* spring boot
* spring 
* mybatis

### 系统模块 
 
 包名  | 描述
  ------------- | -------------
 winway-core & winway-core-*  | 核心包
 winway-cache & winway-cache-*  | 缓存包
 winway-config  | 公共配置模块
 winway-util  | 工具包
 winway-system  | 系统包（集成登录、用户管理、权限管理、菜单管理）

### 重要使用技术点
![Image text]( http://localhost:81/jsjg.png)
1. 所有实体类继承BaseEntity、所有form继承BaseForm
2. 所有要建表的实体使用@YwTable(comment = "comment")注解；所有主键用@YwId()注解；所有字段用@YwColumn();
3. 只允许 service 与 service 之间进行调用
4. 不建议使用自定义sql进行写代码，所有代码均使用
### 独立使用
1、 创建pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.winway</groupId>
        <artifactId>yw-framework</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </parent>
    <artifactId>winway-system</artifactId>
    <packaging>war</packaging>

    
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>demo</name>

    <parent>
        <groupId>com.winway</groupId>
        <artifactId>yw-framework</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-core</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-core-mysql</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-core-h2</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-cache</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>
        
        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-cache-for-shiro</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-config</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>com.winway</groupId>
            <artifactId>winway-util</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <scope>provided</scope>
        </dependency>
    </dependencies>
</project>
```

2、创建模块名 com.winway.demo

3、创建实体类 Student.java
```
package com.winway.demo.entity;

import com.winway.base.entity.BaseEntity;
import com.winway.base.persistence.annotate.YwColumn;
import com.winway.base.persistence.annotate.YwId;
import com.winway.base.persistence.annotate.YwTable;
import com.winway.cache.anno.EntityCache;

import java.io.Serializable;

/**
 * 学生
 */
@EntityCache
@YwTable(comment = "学生")
public class Student extends BaseEntity implements Serializable {

    @YwId
    @YwColumn(comment = "主键")
    private String id;

    @YwColumn(typePrecis = 32, comment = "姓名")
    private String name;

    @YwColumn(typePrecis = 10, comment = "编码")
    private String code;

    @YwColumn(comment = "年龄")
    private Integer age;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }
}

```

4、生成对应的其他文件

  Mapper、Service、Entity、Form、SearchForm、Controller
  
### 集成System使用
 待补充
