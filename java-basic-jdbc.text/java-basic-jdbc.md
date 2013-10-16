Title: [Java基础] JDBC简单步骤
Date: 2013-10-09
Tags: Java,数据库,SQL
Slug: java-basic-jdbc
Author: Zoey Young
Summary: 以前整理的, 翻出来复习

初始化于: 2010-08-27

1. **Load the Driver 向DriverManager注册**

    ｜`Class.forName()`|`Class.forName().newInstance()`|`new DriverName()`

    ｜实例化时自动向DriverManager注册, 不需显式调用DriverManager.registerDriver方法

2. **Connect to the DataBase**

    ｜`DriverManager.getConnection()` -> Connection对象 `conn`

3. **Execute the SQL 执行SQL语句并返回结果集resultSet**

    ｜`conn.CreateStatement()` -> Statement对象 `stmt`

    ｜`stmt.executeQuery()` -> ResultSet对象

    ｜`stmt.executeUpdate()` -> ResultSet对象

4. **Retrieve the result data 对结果集进行遍**

    ｜循环取得结果`while(rs.next())`

5. **Show the result data**

    ｜将数据库中的各种类型转换为Java中的类型(getXXX)方法

6. **Close 关闭连接**

    ｜close the ResultSet/close the Statement/close the Connection

要连上数据库, 首先第一步就要找到相应的JDBC的数据库的类库, 第二步找相应的驱动Driver.

Java提供了一个大管家DriverManager, 要跟哪一个数据库连接, 就要先跟大管家注册一下. 然后透过大管家去和各种数据库连接.

执行SQL语句的第一步就是要创建一个语句对象Statement, 通过连接来创建

要处理的异常:

1. ClassNotFoundException
2. SQLException

写一个简单的JDBC程序, 随便连接到一个数据库.

注意点:

1. 所有抛出的异常全部处理
2. 应该关闭的要在finally里关闭,最好是关闭前判断一下其是否为空,然后再把它关闭
3. 最后并设其为null

-----

    :::java
    import java.sql.*;

    public class TestJDBC {
        public static void main(String[] args) {
            Connection conn = null;
            Statement stmt = null;
            ResultSet rs = null;
            try {
                // 加载JDBC驱动
                Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
                // 等价于 new com.microsoft.sqlserver.jdbc.SQLServerDriver();
                conn = DriverManager.getConnection(
                        "jdbc:sqlserver://localhost:1433;DatabaseName=sample",
                        "sa", "sa");
                stmt = conn.createStatement();
                rs = stmt.executeQuery("select * from table");
                while (rs.next()) {
                    System.out.println(rs.getString("colName"));
                }
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } catch (SQLException e) {
                e.printStackTrace();
            } finally {
                try {
                    if (rs != null) {
                        rs.close();
                        rs = null;
                    }
                    if (stat != null) {
                        stat.close();
                        stat = null;
                    }
                    if (con != null) {
                        con.close();
                        con = null;
                    }
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
