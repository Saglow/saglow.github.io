---
title: SQL
description: SQL（Structured Query Language，结构化查询语言）是一种用于管理关系型数据库系统的特定领域语言。它用于定义、操作和查询数据库中的数据。SQL是许多关系型数据库管理系统（RDBMS）的标准查询语言，包括MySQL、SQLite、Oracle、SQL Server和PostgreSQL等。
date: 2022-1-1
tags:	[知识积累]
toc: true
finished: true
comments: true
---

SQL（Structured Query Language，结构化查询语言）是一种用于管理关系型数据库系统的特定领域语言。它用于定义、操作和查询数据库中的数据。SQL是许多关系型数据库管理系统（RDBMS）的标准查询语言，包括MySQL、SQLite、Oracle、SQL Server和PostgreSQL等。

以下是常用的SQL语句类型及其功能：

1. **查询数据（SELECT）**：
   - `SELECT column1, column2 FROM table_name`: 从表中选取指定列的数据。
   - `SELECT * FROM table_name`: 从表中选取所有列的数据。
   - `SELECT DISTINCT column_name FROM table_name`: 从表中选取唯一不重复的列值。
   - `SELECT column1, column2 FROM table_name WHERE condition`: 使用条件筛选行。

2. **插入数据（INSERT）**：
   - `INSERT INTO table_name (column1, column2) VALUES (value1, value2)`: 向表中插入新数据。

3. **更新数据（UPDATE）**：
   - `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition`: 更新表中符合条件的数据。

4. **删除数据（DELETE）**：
   - `DELETE FROM table_name WHERE condition`: 删除表中符合条件的数据。

5. **创建表（CREATE TABLE）**：
   - `CREATE TABLE table_name (column1 datatype, column2 datatype, ...)`: 创建新表。

6. **删除表（DROP TABLE）**：
   - `DROP TABLE table_name`: 删除表及其数据。

7. **修改表结构（ALTER TABLE）**：
   - `ALTER TABLE table_name ADD column_name datatype`: 添加新列。
   - `ALTER TABLE table_name MODIFY column_name datatype`: 修改列的数据类型。
   - `ALTER TABLE table_name DROP column_name`: 删除列。

8. **聚合函数（Aggregate Functions）**：
   - `SELECT COUNT(column_name) FROM table_name`: 统计行数。
   - `SELECT SUM(column_name) FROM table_name`: 计算列的总和。
   - `SELECT AVG(column_name) FROM table_name`: 计算列的平均值。
   - `SELECT MAX(column_name) FROM table_name`: 找出列的最大值。
   - `SELECT MIN(column_name) FROM table_name`: 找出列的最小值。

9. **GROUP BY 子句**：
   - `SELECT column1, COUNT(column2) FROM table_name GROUP BY column1`: 对数据进行分组聚合。

10. **ORDER BY 子句**：
    - `SELECT column1, column2 FROM table_name ORDER BY column1 ASC/DESC`: 对结果集进行排序。

11. **LIMIT 子句**：
    - `SELECT column1, column2 FROM table_name LIMIT number`: 限制返回的行数。

12. **连接表（JOIN）**：
    - `SELECT column1, column2 FROM table1 INNER JOIN table2 ON table1.column = table2.column`: 将多个表连接在一起。

这些SQL语句是SQL编程中最常用的一些基本操作，用于管理数据库中的数据和表结构。根据具体的需求，可以结合这些语句来完成复杂的数据库操作。