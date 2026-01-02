---
title: JavaWeb简要总结--Mysql,JDBC
date: 2020-08-31 23:23:30
tags:
  - Website
cover: https://user-images.githubusercontent.com/60562661/91742455-e1b69200-ebe8-11ea-8c49-1efdfc6166b6.jpg
---

**Summarize** 	总结给自己看，泛泛学过去很多东西记不住，这里记录一下最常用的东西，最核心的。

## Mysql 极简操作

> Mysql 首次安装登录出现问题，
>
> ERROR 1045 (28000): Access denied for user 'ODBC'@'localhost' (using password: YES)
>
> 解决问题见：https://blog.csdn.net/tiankongbubian/article/details/77119751
>
> 适用于 **windows** 环境

---

### **常用SQL命令**

**分类：DML,DQL,DCL,DDL**

- **Data Definition Language** (DDL数据定义语言) 如：建库，建表
- **Data Manipulation Language**(DML数据操纵语言)，如：对表中的记录操作增删改
- **Data Query Language**(DQL 数据查询语言)，如：对表中的查询操作
- **Data Control Language**(DCL 数据控制语言)，如：对用户权限的设置

```shell
mysql -uroot -proot //登录mysql
```

```mysql
show databases; -- 显示数据库

use test;

show tables; -- 显示表

create database 库名; -- 建库

drop database 库名; -- 删库

drop table if exists `create`;
```

```mysql
/*
创建表实例
*/
CREATE TABLE student3 ( 
    id INT, 
	NAME VARCHAR(20), 
	age INT, 
	sex VARCHAR(5), 
	address VARCHAR(100), 
	math INT,  
	english INT
);  

-- 修改表相关
alter table 表名 rename to 新的表名; -- 1. 修改表名
		
alter table 表名 character set 字符集名称; -- 2. 修改表的字符集
		
alter table 表名 add 列名 数据类型; -- 3. 添加一列
		
alter table 表名 change 列名 新列别 新数据类型; -- 4. 修改列名称 类型
alter table 表名 modify 列名 新数据类型;
	
alter table 表名 drop 列名; -- 5. 删除列

```

增删改表数据：

```mysql
-- 添加记录
insert into 表名(列名1,列名2,...列名n) values(值1,值2,...值n); -- 指定列
insert into 表名 values(值1,值2,...值n); -- 所有列
-- 删除记录
delete from 表名 [where 条件]
 TRUNCATE TABLE 表名; -- 删除表建议操作
 -- 修改记录
 update 表名 set 列名1 = 值1, 列名2 = 值2,... [where 条件];
 --查询记录
 select * from 表名;
 select 字段名1，字段名2... from 表名；
 
-- '_'表示一个占位符，'%'表示不确定占位符
 -- 查询姓马的有哪些？ like
SELECT * FROM student WHERE NAME LIKE '马%';
-- 查询姓名第二个字是化的人			
SELECT * FROM student WHERE NAME LIKE "_化%";
-- 查询姓名是3个字的人
SELECT * FROM student WHERE NAME LIKE '___';
```



以上就是最常写的sql命令了。**Mysql极简入门，可以查询基本语法。其他高级部分用到再面向百度编程。**

---

![](https://user-images.githubusercontent.com/60562661/91742293-a2884100-ebe8-11ea-9fe3-fb7627f853a8.jpg)



## JDBC--Java连接数据库

记录一下`JDBC`最常用的 一套流程，其他冗余的就不多做记录了。

- **原生 JDBC 连接操作流程**

```java
public class DemoJDBC {
    public static void main(String[] args) throws Exception {

        //  注册驱动 ，内部自动执行静态代码块
        Class.forName("com.mysql.jdbc.Driver");

        // 获取数据库连接对象
        //本机可以简写  jdbc:mysql:///test_multi
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test_multi", "root", "123");

        // 定义 sql 语句
        String sql = "update user set password = 'lol'";
        String sql2 = "select * from user";

        // 1. 获取sql执行对象
        // 2. 事务管理
        Statement statement = conn.createStatement();

        // 执行sql对象
        // executeUpdate (执行DML语句, DDL语句
       int count = statement.executeUpdate(sql);
        ResultSet results = statement.executeQuery(sql2);
		
        //遍历结果
        while (results.next()){
            int id = results.getInt("uid");
            String userName = results.getString("username");
            String passWord = results.getString("password");
            Date birth = results.getDate("birthday");

            System.out.println("id: " + id +
                               "userName: " + userName +
                               "passWord: " + passWord +
                               "birthDay: " + birth);
        }
		
        // 释放资源
        statement.close();
        conn.close();
    }

}

```



- **JDBCTemplate 流程 -- 最常用**

  > Spring框架对JDBC的简单封装。提供了一个JDBCTemplate对象简化JDBC的开发

```java
// 定义工具类，采用阿里的Druid连接池
public class JDBCPoolUtils {

    private static DataSource ds;

    // 初始化数据源
    static {
        try {
            Properties pro = new Properties();
            pro.load(JDBCPoolUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
            ds = DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
	
    // 获取连接对象
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }
	
    //释放资源
    public static void close(PreparedStatement statement, Connection con) {
        if (statement != null) {
            try {
                statement.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }

        }
        if (con != null) {
            try {
                statement.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

    }
	
    //释放资源重载
    public static void close(ResultSet res, PreparedStatement statement, Connection con) {
        if(res!=null){
            try {
                res.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }

        }
        if (statement != null) {
            try {
                statement.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }

        }
        if (con != null) {
            try {
                statement.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

    }

    public static DataSource getDataSource(){
        return ds;
    }


}

```

```java
//JDBCTemplate流程
public class DemoJDBCTemplate {
    public static void main(String[] args) {
        //创建JdbcTemplate对象
        JdbcTemplate template = new JdbcTemplate(JDBCPoolUtils.getDataSource());
        // 定义sql语句
        String sql = "select * from user";
        String sql2 = "select count(id) from user";        
        // 执行查询返回javabean对象装载到列表
        //User 对象 与 数据库列一一对应
        List<User> zyl = template.query(sql, new BeanPropertyRowMapper<User>(User.class)); // 返回 JavaBean
        Long count = template.queryForObject(sql2,Long.class); // 执行聚合函数
        System.out.println(count);
        for(User map : zyl){
            System.out.println(map);
        }
    }
}

```

---

**2020-9-1日夜更新。**