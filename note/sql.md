# 一、数据库概要
数据库（Database）是存储与管理数据的软件系统，就像一个存入数据的物流仓库。

## 1. 数据库分类
最常见的数据库模型主要是两种，即**关系型数据库**和**非关系型数据库**。

+ 1.1 **关系型数据库:** 当前在成熟应用且服务与各种系统的主力数据库还是关系型数据库。代表:</br>
**Oracle**、**SQL Server**、**MySQL**
* 1.2 **非关系型数据库:** NoSQL数据库在存储速度与灵活性方面有优势，也常用于缓存。常见有:</br>
**Redis**、**Mongodb**

## 2. 数据库的设计
设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库,这些不同的规范要求被称为不同的范式.范式可以指导我们更好地设计数据库的表结构，减少冗余的数据，借此可以提高数据库的存储效率，数据完整性和可扩展性。</br>

* ### 三大范式:
    * 2.1 第一范式（1NF）</br>
        > 所谓第一范式（1NF）是指在关系模型中，对列添加的一个规范要求，所有的列都应该是原子性的，即数据库表的每一列都是不可分割的原子数据项，而不能是集合，数组，记录等非原子数据项
    * 2.2 第二范式（2NF）</br>
        > 第二范式（2NF）要求实体的属性完全依赖于主关键字。所谓完全依赖是指不能存在仅依赖主关键字一部分的属性，如果存在，那么这个属性和主关键字的这一部分应该分离出来形成一个新的实体，新实体与原实体之间是一对多的关系。为实现区分通常需要为表加上一个列，以存储各个实例的唯一标识。简而言之，第二范式就是在第一范式的基础上属性完全依赖于主键。
    * 2.3 第三范式（3NF）</br>
        > 第三范式是在第二范式基础上，更进一层，第三范式的目标就是确保表中各列与主键列直接相关，而不是间接相关。即各列与主键列都是一种直接依赖关系，则满足第三范式。

## 3.sql语句
参考文章

[sql语句大全](https://www.cnblogs.com/yubinfeng/archive/2010/11/02/1867386.html)
*  **3.1基础篇**
    * 1.创建数据库:</br>
        `CREATE DATABASE database-name`
    * 2.说明：删除数据库</br>
        `drop database dbname`
    * 3.创建新表
    ```
    CREATE TABLE `heartbeat` (
    `ts` varchar(26) NOT NULL,
     PRIMARY KEY (`server_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
    ```
    或者根据已有的表创建同数据结构的新表:</br>
    `create table tab_new like tab_old`
    * 4.基本语句
    ```
        选择：select * from table1 where 范围
        插入：insert into table1(field1,field2) values(value1,value2)
        删除：delete from table1 where 范围
        更新：update table1 set field1=value1 where 范围
        查找：select * from table1 where field1 like ’%value1%’ ---like的语法很精妙，查资料!
        排序：select * from table1 order by field1,field2 [desc]
        总数：select count as totalcount from table1
        求和：select sum(field1) as sumvalue from table1
        平均：select avg(field1) as avgvalue from table1
        最大：select max(field1) as maxvalue from table1
        最小：select min(field1) as minvalue from table1
        CONCAT( u.name ,',', u.sex ,',', o.teacher  )AS name_birthday  （将一些字符组合在一起）
        分组:Group by
    ```
    * 5.使用外连接
    ```
        左（右）外联查语法结构：（没有要求两张表要有外键关联）
        select u.name , u.sex , o.teacher 
        from `student` as u  
        left join    （以它为中线，在前面的为左表，后面的为右表）
        `information` as o  
        on u.id = o.id（这两个这段不一定要外键，这两个字段的集合取决于where 条件下的集合，没有where 则为全部）
        where  u.id=7
        group by u.age; 
    ```
    说明:</br>
    首先明确两个概念：
    LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。
    数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。
    在left join下，两者的区别：
    on是在生成临时表的时候使用的条件，不管on的条件是否起到作用，都会返回左表 (table_name1) 的行。
    where则是在生成临时表之后使用的条件，此时已经不管是否使用了left join了，只要条件不为真的行，全部过滤掉。
    在多表查询时，on比where更早起作用。系统首先根据各个表之间的联接条件，把多个表合成一个临时表后，再由where进行过滤，然后再计算，计算完后再由having进行过滤。由此可见，要想过滤条件起到正确的作用，首先要明白这个条件应该在什么时候起作用，然后再决定放在那里。


