
# 连接数据库
##### 启动服务：
```
service mysql start
```
**PS：** 服务命令的4个参数：
1. start：启动服务
2. stop：停止服务
3. restart：重启服务
4. starus：查看服务状态
##### 登录数据库：
```
mysql -u用户名 -p密码
```
# 基本操作
## 一、数据库的基本操作
#### 1.创建数据库
```
create database 数据库名称;
```
#### 2.查询数据库
###### 查看所有数据库：
```
show databases;
```
###### 查看指定数据库：
```
show create database 数据库名称;
```
#### 3.修改数据库
```
alter database 数据库名称 default character set 编码方式 collate 编码方式_bin;
```
#### 4.删除数据库
```
drop database 数据库名称;
```
## 二、数据表的基本操作
#### 1.创建数据表
**命令：**
```
create table 表名(
字段名 1,数据类型[完整性约束条件],
...
字段名 n,数据类型[完整性约束条件]
);
```
**例：**
```
create table test
(
id int(11),
name varchar(20),
grade float
);
```
#### 2.查询数据表
###### 查询所有数据表：
```
show tables;
```
###### 查看指定数据表：
```
show create table 表名;
或 
show create table 表名\G;
```
```
describe 表名;
简写 
desc 表名;
```
#### 3.修改数据表
##### 修改表名
**命令：**
```
alter table 旧表名 rename [to] 新表名;
```
**例：**
```
alter table test rename to grade;
```
##### 修改字段名
**命令：**
```
alter table 表名 change 旧字段名 新字段名 新数据类型;
```
**例：**
```
alter table grade change name username varchar(20);
```
##### 修改字段数据类型
**命令：**
```
alter table 表名 modify 字段名 数据类型;
```
**例：**
```
alter table grade modify id int(20);
```
##### 添加字段
**命令：**
```
alter table 表名 add 新字段名 数据类型 [约束条件] [first|after 已存在字段名]
```
 **PS：**
 1."first"为可选参数，将添加的字段设置为表的第一个。
 2."after"为可选参数，将添加的字段放到"已存在的字段名"后面。
**例:**
```
alter table grade add age int(10);
```
##### 删除字段
**命令：**
```
alter table 表名 drop 字段名;
```
**例：**
```
alter table grade drop age;
```
##### 修改字段的排列位置
**命令：**
```
alter table 表名 modify 字段名1 数据类型 first|after 字段名2;
```
**PS：** “字段名1”指被修改的字段，'first'是改为表的第一个字段，'after'是将“字段1”插入到“字段2”后面。
**例：**
```
alter table grade modify username varchar(20) first;
```
#### 4.删除数据表
**命令：**
```
drop table 表名;
```
**例：**
```
drop table grade;
```
## 三、数据的基本操作
### 添加数据
#### 为表中所有字段添加数据 
##### 指定字段添加数据
**命令：**
```
insert into 表名(字段名1,字段名2,... )
values(值1,值2,...);
或
insert into 表名
set 字段名1=值1[,字段名2=值2,...];
```
**PS:** “字段名”为指定数据表中字段名；“值”为每个字段的值（顺序，类型必须相对应）
**例：**
```
insert into grade(id,username,grade )
values(1,'zhangsan',7);
```
##### 不指定字段名添加数据
**命令：**
```
insert into 表名 values(值1,值2,...);
```
**PS:** 由于没有指定字段名，添加的值必须和字段在表中的顺序一样
**例：**
`insert into grade values(1,'zhangsan');`
##### 同时添加多条记录
**命令：**
```
insert into 表名(字段名1,字段名2,...)
values(值1,值2,...),
...
(值1,值2,...);
或
insert into 表名 
values(值1,值2,...),
...
(值1,值2,...);
```
**PS:** 也可以不指定字段名。添加的值必须和字段在表中的顺序一样
**例：**
```
insert into grade(id,username,grade) values(1,'zhangsan',7),(2,'lisi',7);
或
insert into grade values(1,'zhangsan',7),(2,'lisi',7);
```
### 更新/修改数据
**命令：**
```
update 表名 
set 字段名1=值1[,字段名2=值2,...] 
[where 条件表达式];
```
**PS：** “字段名”为指定要更新的字段，“值”为更新的新数据。“where 条件表达式”为可选参数，用于指定更新数据需要满足的条件。
##### 更新指定数据
**命令：**
```
update 表名 
set 字段名1=值1[,字段名2=值2,...] 
where 条件表达式;
```
**例：**
```
update grade 
set username='zhangsan' 
where id=1;
```
##### 更新全部数据
**命令：**
```
update 表名 
set 字段名1=值1[,字段名2=值2,...];
```
**例：**
```
update grade 
set grade=80;
```
### 删除数据
**命令：**
```
delete from 表名 [where 条件表达系统];
```
**PS：** “表名”指定要执行删除操作的表，[where 条件表达式]为可选参数，用于删除满足条件的数据。
##### 删除指定数据数据
**命令：**
```
delete from 表名 where 条件表达系统;
```
**例：**
```
delete from grade where id=2;
```
##### 删除全部数据数据数据
**命令：**
```
delete from 表名;
或
truncate [table] 表名;
```
**PS：** 不同点：
1.truncate语句后不能接where条件句，只能删除全部数据
2.delete语句删除数据后，新增数据时自增字段从已删除记录的最大值开始计算，而使用truncate语句时，新增数据自增字段从1开始计算
**例：**
```
delete from grade;
或
truncate table grade;
```
# 数据查询
## 一、单表查询
**命令：**
```
select [distinct] * | 字段名1,字段名2,字段名3,...
from 表名
[where 条件表达式1]
[group by 字段名 [having 条件表达式2]]
[order by 字段名 [asc|desc]]
[limit [offset] 记录数]
```
**PS：**
1. “select [distinct] * |字段名1,字段名2,字段名3,...”：表示从表中查询指定字段，星号（*）通配符表示表中所有字段，二者任选其一。“distinct”是可选参数用于去除查询结果中的重复数据。
2. “from 表名”：表示从指定的表中查询数据。
3. “where表达式1”：用于指定查询条件
4. “group by 字段名 [having 条件表达式2]”：“group by”用于将查询结果按照指定字段进行分组，“having”用于对分组后的结果进行过滤。
5. “order by 字段名 [asc|desc]”：“order by”用于将查询结果按照指定字段进行排序，“[asc|desc]”参数“asc”升序，“desc”降序。
6. “limit [offset] 记录数”：“limit”用于限制查询结果数量，后面可以接两个参数，“[offset]”表示偏移量，默认为0，查询结果从偏移量+1条数据开始，“记录数”表示返回查询记录的条数
#### 1.简单查询
##### 查询指定字段
**命令：**
```
select 字段名1,字段名2,字段名3,... from 表名;
```
**例：**
```
select id,name,grade,gender from grade;
```
##### 查询所有字段
**命令：**
` select * from 表名;`
**例：**
` select * from grade;`
#### 1.按条件查询
##### 带关系运算符的查询
**命令：**
```
select 字段名1,字段名2,字段名3,... 
from 表名 
where 条件表达式;
```
**例：**
```
select id,name,grade,gender 
from grade 
where id=4;
```
##### 带in关键字的查询
**命令：**
```
select * |字段名1,字段名2,字段名3,... 
from 表名 
where 字段名 [not] in (元素1,元素2,...);
```
**PS：** “元素1,元素2”表示集合中的元素，即指定的条件范围。“[not]”可选参数，使用后表示查询不在in关键字指定集合范围的记录；
**例：**
```
select id,name,grade,gender  
from grade  
where id in (1,2,3);
```
##### 带between and关键字的查询
**命令：**
```
select * |字段名1,字段名2,字段名3,... 
from 表名 
where 字段名 [not] between 值1 and 值2;
```
**PS：** “值1”表示范围条件的起始值，“值2”表示范围条件的结束值。“[not]”是可选参数，使用后表示查询指定范围之外的记录。（值1小于值2，否则查询不到结果）
**例：**
```
select id,name,grade,gender 
from grade 
where id between 1 and 5;
```
##### 空值查询
**命令：**
```
select * |字段名1,字段名2,... 
from 表名 
where 字段名 is [not] null;
```
**PS：**“[not]”是可选参数，使用后表示查询不是空值的记录。
**例：**
```
select id,name,grade,gender 
from grade 
where gender is null;
```
##### 过滤重复查询
**命令：**
```
select distinct 字段名 from 表名; 
或
select distinct 字段名1,字段名2 from 表名; 
```
**PS：** “字段名”表示要过滤重复记录的字段。“字段名1,字段名2”多个字段值需要相同才会被认作是重复记录；
**例：**
```
select distinct gender from grade; 
或
select distinct gender,name from grade; 
```
##### 模糊查询
**命令：**
```
select * |字段名1,字段名2,... 
from 表名 
where 字段名 [not] like '匹配字符串';
```
**PS：**“字段名”表示要查询的字段。“[not]”是可选参数，使用后表示与查询不匹配的记录。“匹配字符串”指定用来匹配的字符串，其值可以是一个普通字符串也可以是一个通配符。
**通配符：**

1. "%"：符号相当于任意数量的字符，“c%”指c开头任意字符数量的字符串，“%c%”表示c之前有任意字符数量，之后有任意字符数量的字符串都相匹配。
2. “_”：只匹配单个字符。
3. “[charlist]”：匹配字符中任何单一字符。
4. “[^|!charlist]”：匹配不在字符列中的任何单一字符。
5. 若是匹配字符串中包含有“%”、“_”时，需要在匹配字符前加“\”进行转义。
**例：**
```
select id,name,grade,gender 
from grade 
where name like "s%";
```
##### and关键字多条件查询
**命令：**
```
select * |字段名1,字段名2,... 
from 表名
where 条件表达式1 and 条件表达式2 [...and 条件表达式n];
```
**例：**
```
select id,name,gender 
from grade 
where id<=5 and gender="女";
```
##### or关键字多条件查询
**命令：**
```
select * |字段名1,字段名2,... 
from 表名 
where 条件表达式1 or 条件表达式2 [...or 条件表达式n];
```
**例：**
```
select id,name,gender 
from grade  
where id<3 or gender="女";
```
##### and与or联合查询
**命令：**
```
select * |字段名1,字段名2,... 
from 表名 
where 条件表达式1 or|and 条件表达式2 [...or|and 条件表达式n];
```
**PS：**  and的优先级高于or，一起使用时，先运算and两边条件表达式，再运算or两边表达式。
**例：**

```
select id,name,gender,grade 
from grade  
where grade=100 and  gender="男" or gender="女";
```

  
