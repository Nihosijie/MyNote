# Java 基础

## 常量与变量

### 标识符

#### 标识符的命名规则

- 标识符可以由字母、数字、下划线和美元符号组成，不能以数字开头
- 标识符严格区分大小写
- 标识符不能是Java关键字和保留字
- 标识符的命名最好能反映出其作用

#### 关键字

[![I3eMZR.png](https://z3.ax1x.com/2021/11/07/I3eMZR.png)](https://imgtu.com/i/I3eMZR)

保留关键字：goto

### 变量

#### 变量的三个元素：

变量类型、变量名、变量值

#### 变量名的命名规则

- 满足标识符命名规则
- 符合小驼峰法
- 尽量简单，做到见名知意
- 变量名的长度没有限制

#### 类的命名规则

- 满足大驼峰(Pascal)命名规则

### 数据类型

- 基本数据类型
  - 数值型
    - 整数型
      - byte/1
      - short/2
      - int/4
      - long/8
    - 浮点型
      - float/4
      - double/8
  - 字符型
    - char/1
  - 布尔型
    - boolean/**~**
- 引用数据类型
  - 类
  - 接口
  - 数组

### 进制表示

- 二进制：0b开头，包括0和1

- 八进制：0开头，包括0-7的数字
- 十进制，无开头，包括0-9
- 十六进制，0x开头，包括0-9和a-f

### 类型转换

- 自动类型转换（隐式类型转换）

  由数据表示范围小的类型转向数据表示范围大的方向转换

![[resources/image-20211107225128359.png]]

- 强制类型转换

  由数据表示范围大的类型想数据表示范围小的方向转换

  格式：(输出类型)数值

### 常量

使用final修饰，常量名一般使用大写，必须初始化，之后不能被修改

## java运算符

- 算数运算符

  - ```+``` : 加法

  - ```-``` : 减法

  - ```*``` : 乘法

  - ```/``` : 整除, 当被除数或除数有一个为浮点数时为除法

  - ``` % ``` : 取余

  - ``` ++ ``` : 自增

  - ``` -- ``` : 自减

    ![[resources/image-20211108153421461.png]]

- 赋值运算符

  - ```+=``` :  
  - ```-=``` : 
  - ```*=``` : 
  - ``` \=``` : 

- 关系运算符

- 逻辑运算符

- 条件运算符

- 位运算符





# 数据库开发与实战



![[resources/image-20211108193746727.png]]

![[resources/image-20211108193836980.png]]

![[resources/image-20211108193906740.png]]

![[resources/image-20211108194004541.png]]

![[resources/image-20211108194018840.png]]



##   MySQL基础

### MySQL 忘记密码

普通用户忘记密码：通过root用户修改密码

root用户忘记密码：

1. 创建一个txt文件，定义修改密码的SQL语句

   localhost是只允许本地登陆，如果改成了ip则为可以远程登陆

   123456为新设置的密码

   ```sql
   ALTER USER&#39;root&#39;@&#39;localhost&#39; IDENTIFIED BY &#39;123456&#39;;yy
   ```

2. 管理员打开powershell窗口

   ```bash
   # 先停止服务
   net stop mysql80
   
   mysqld --defaults-file="Mysql数据目录路径\my.ini" -init-file="上述命令保存的txt文件路径" --console 
   ```

3. 尝试使用新密码连接数据库

4. 将mysql服务打开

   ```bash
   net start mysql80
   ```

### MySQL配置文件

```ini
[client]
# 客户端在连接时若未指明端口，则默认指向3306端口
port=3306 

[mysql]
# 命令行界面输入命令如果出错时不发出蜂鸣器的声音
no-beep 


[mysqld]
#端口号
port=3306
# 数据目录
datadir=D:/CodeTool/MySQL/MySQL Server 8.0\Data
# 密码认证插件
default_authentication_plugin=mysql_native_password
# 默认村塾引擎
default-storage-engine=INNODB
# 数据库模式，严格模式时若存的数据和数据类型不符则无法存入数据
sql-mode="STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION"
# 日志输出：用文件记录日志
log-output=FILE
# 是否生成日志，0未开启日志
general-log=0
# 当开启记录日志时，日志名将以以下文件名命名
general_log_file="SUPERPC.log"
# 开启慢查询日志，当进行数据库优化时，需要日志记录SQL语句执行的过程
slow-query-log=1
#慢查询日志文件名称
slow_query_log_file="SUPERPC-slow.log"
# 当大于多少秒未执行完的SQL语句会被记录在慢查询日志
long_query_time=10
# 错误日志名称
log-error="SUPERPC.err"
log-bin="SUPERPC-bin"
# 数据库ID，数据库集群时会用到数据库ID
server-id=1
# 创建表时把表明转换为小写，1：打开
lower_case_table_names=1
# 导入导出数据时存放的目录地址
secure-file-priv="D:/CodeTool/MySQL/MySQL Server 8.0/Uploads"
# MySQL最大支持链接的数量
max_connections=151

table_open_cache=2000

tmp_table_size=74M
# 线程数量，影响数据库的效率
thread_cache_size=10

myisam_max_sort_file_size=100G

myisam_sort_buffer_size=138M

key_buffer_size=8M

read_buffer_size=64K

read_rnd_buffer_size=256K

innodb_flush_log_at_trx_commit=1

innodb_log_buffer_size=1M

innodb_buffer_pool_size=8M

innodb_log_file_size=48M

innodb_thread_concurrency=13

innodb_autoextend_increment=64

innodb_buffer_pool_instances=8

innodb_concurrency_tickets=5000

innodb_old_blocks_time=1000

innodb_open_files=300

innodb_stats_on_metadata=0

innodb_file_per_table=1

innodb_checksum_algorithm=0

back_log=80

flush_time=0

join_buffer_size=256K

max_allowed_packet=4M

max_connect_errors=100

open_files_limit=4161

sort_buffer_size=256K

table_definition_cache=1400

binlog_row_event_max_size=8K

sync_master_info=10000

sync_relay_log=10000

sync_relay_log_info=10000

loose_mysqlx_port=33060

```

### MySQL数据库表的相关操作

#### SQL语言分类

- DML：数据库操作语言
  - 添加
  - 修改
  - 删除
  - 查询
- DCL：数据库控制语言
  - 用户
  - 权限
  - 事务
- DDL：数据定义语言
  - 逻辑库
  - 数据表
  - 视图
  - 索引

#### SQL语句注意事项

- SQL语句不区分大小写，但是字符串区分大小写，**建议关键字大写，非关键字小写**
- SQL语句必须以分号结尾
- SQL语句中的空白和换行没有限制，但是不能破坏语法

#### SQL语句中的注释

- \# 单行注释
- /* 多行注释 */

#### SQL创建逻辑库

```SQL
# 创建逻辑库
CREATE DATABASE 逻辑库名称;
# 显示所有的逻辑库
SHOW DATABASES;
# 删除数据库
DROP DATABASE 逻辑库名称;
```

#### 数据表操作

创建数据表时命名建议：

前面加上t_ 或者tb_ 表示是真实的数据表

前面加上 v_ 或者 vw_ 表示这是一张虚拟的视图

````sql
# 创建数据表
CREATE TABLE 数据表(
列名1 数据类型 [约束] [COMMENT 注释],
列名2 数据类型 [约束] [COMMENT 注释],
    .....
)[COMMENT = 注释]

# 列出数据表
SHOW TABLES;


# 输出数据表的结构
DESC 数据表

# 输出数据表的创建语句
SHOW CREATE TABLE 数据表

# 删除数据表
DROP TABLE 数据表;

````

#### 数据类型

- 数字

  |                      类型                       |  大小  | 说明          |
  | :---------------------------------------------: | :----: | :------------ |
  |                     TINYINT                     | 1字节  | 小整数        |
  |                    SMALLINT                     | 2字节  | 普通整数      |
  |                    MEDIUMINT                    | 3字节  | 普通整数      |
  |                       INT                       | 4字节  | 较大整数      |
  |                     BIGINT                      | 8字节  | 大整数        |
  |                      FLOAT                      | 4字节  | 单精度浮点数  |
  |                     DOUBLE                      | 8字节  | 双精度浮点数  |
  |                     DECIMAL                     | ------ | DECIMAL(10,2) |
  | DECIMAL(整数加小数占的位数, 小数点后精确到几位) |        |               |

   		记录整数时，使用 INT 即可，记录小数时，如果要求精确，需要使用DECIMAL，单/双精度浮点数会因为二进制的问题而无法精确表示小数

- 字符串

  |    类型    |      大小      | 说明               |
  | :--------: | :------------: | :----------------- |
  |    CAHR    |   1-255字符    | 固定长度字符串     |
  |  VARCHAR   |  1-65535字符   | 不固定长度字符串   |
  |    TEXT    |  1-65535字符   | 不确定长度字符串   |
  | MEDIUMTEXT | 1-1千6百万字符 | 不确定长度字符串   |
  |  LONGTEXT  |   1-42亿字符   | 不确定是长度字符串 |

  一般最大使用VARCHAR足矣，如果需要保存超长数据一般使用非关系型数据库

- 日期类型

  |   类型    | 大小  | 说明                             |
  | :-------: | :---: | :------------------------------- |
  |   DATE    | 3字节 | 日期(不包含时分秒等时间)         |
  |   TIME    | 3字节 | 时间(时分秒)                     |
  |   YEAR    | 1字节 | 年份                             |
  | DATETIME  | 8字节 | 时间日期                         |
  | TIMESTAMP | 4字节 | 时间戳(只能是1970年1月1日之后的) |

  MySQL 中的日期是一种特殊的字符串，所以输入时需要加上单/双引号，年月日之间用```-```分割

#### 修改表结构

- 添加字段

  ``` sql
  ALTER TABLE 表名
  ADD 列1 数据类型 [约束] [COMMENT 注释],
  ADD 列2 数据类型 [约束] [COMMENT 注释],
  ...;
  ```

- 修改字段类型和约束

  ``` sql
  ALTER TABLE 表名称
  MODIFY 列1 数据类型 [约束] [COMMENT 注释],
  MODIFY 列2 数据类型 [约束] [COMMENT 注释],
  .....;
  ```

  

- 修改字段名称

  ``` sql
  ALTER TABLE 表名
  CHANGE 列1 新列名1 数据类型 [约束] [COMMENT 注释],
  CHANGE 列2 新列名2 数据类型 [约束] [COMMENT 注释],
  .....;
  ```

- 删除字段

  ```sql
  ALTER TABLE 表名
  DROP 列1,
  DROP 列2,
  .....;
  ```

  

- 修改表名

``` sql
ALTER TABLE 表名 RENAME 新表名;
```



#### 数据库的范式

- 构建数据库必须遵循一定的规则，这种规则就是范式
- 目前关系型数据库有6种范式，一般情况下，只需要满足第三范式即可

##### 第一范式：原子性

- 第一范式是数据库的基本要求，不满足这一点就不是关系型数据库

- 数据表中的每一列都是不可分割的基本数据项，同一列中不能有多个值，也不能存在重复的属性

  ![[resources/image-20211108225855901.png]]

##### 第二范式：唯一性

- 数据表中的每条记录必须是唯一的。为了实现区分，通常要为表加上一个列用来存储唯一标识，这个唯一属性列被称作主键列

  ![[resources/image-20211108230013540.png]]

##### 第三范式：关联性

- 每列都与主键有直接关系，不存在依赖传递

  ![[resources/image-20211108230047381.png]]

- 依照第三范式，数据可以拆分保存到不同的数据表，彼此保持关联

  ![[resources/image-20211108230135961.png]]

#### 字段约束

- MySQL中的字段约束共有4种

  | 约束名称 |   关键字    | 描述                     |
  | :------: | :---------: | :----------------------- |
  | 主键约束 | PRIMARY KEY | 字段值唯一，且不能为NULL |
  | 非空约束 |  NOT NULL   | 字段值不能为NULL         |
  | 唯一约束 |   UNIQUE    | 字段值唯一，且可以为NULL |
  | 外键约束 | FOREIGN KEY | 保持关联数据的逻辑性     |

  外键约束是唯一不推荐使用的约束

##### 主键约束

- 要求字段的值在全表中必须唯一，而且不能为NULL
- 建议主键一定要使用数字类型，因为数字的检索速度会非常快
- 如果主键为数字类型，还可以设置自动增长

```sql
CREATE TABLE t_teacher(
id INT PRIMARY KEY AUTO_INCREMENT,
...,
);
```

##### 非空约束

- 非空约束要求字段的值不能是NULL值

- NULL值是没有值，而不是 “” 空字符串

  ```sql
  CREATE TABLE t_teacher(
  	INT PRIMARY KEY AUTO_INCREMENT,
      name VARCAHR(20) NOT NULL,
      married BOOLEAN NOT NULL DEFAULT FALSE
  );
  ```

  BOOLEAN在sql中实际上是不存在的，在数据库表中会被数据库映射成 TINYINT 类型

##### 唯一约束

- 唯一约束要求字段值如果不为NULL，那么在全表中必须唯一

```sql
CREATE TABLE t_teacher(
....,
    tel VARCHAR(11) NOT NULL UNIQUE
);
```

##### 外键约束

- 外键约束用来保证关联数据的逻辑关系

  ![[resources/image-20211108231154820.png]]

- 外键约束的定义是写在子表上的

  ```sql
  # 部门表
  CREATE TABLE t_dept(
  	deptno INT UNSIGNED PRIMARY KEY,
      dname VARCHAR(20) NOT NULL UNIQUE,
      tel CHAR(4) UNIQUE
  ); 
  ```

  

  ```sql
  # 员工表
  CREATE TABLE t_emp(
  	empno INT UNSIGNED PRIMARY KEY,
      ename VARCHAR(20) NOT NULL,
      sex ENUM("男", "女") NOT NULL,
      deptno INT UNSIGNED,
      hiredate DATE NOT NULL,
      FOREIGN KEY (deptno) REFERENCES t_dept(deptno)
  );
  ```

  要删除父表中的内容必须先删除子表中的内容

##### 外键约束的闭环问题

- 如果形成外键闭环，那么我们将无法删除任何一张表的记录

  ![[resources/image-20211108231527261.png]]

#### 索引

##### 数据排序的好处

- 一旦数据排序之后，查找的速度就会翻倍，现实世界(字典)和程序世界都是如此

##### 数据表的索引

- MySQL 利用二叉树结构，对数据表的记录排序，从而加速数据的检索速度

##### 创建索引

```sql
CREATE TABLE 表名称(
...,
    INDEX [索引名称](字段),
    ....
);
```

```sql
CREATE TABLE t_msg(
id INT UNSIGNED PRIMARY KEY,
    content VARCHAR(200) NOT NULL,
    type ENUM("公告", "通报", "个人通知") NOT NULL,
    create_time TIMESTAMP NOT NULL,
    INDEX idx_type (type)
)
```





##### 添加和删除索引

```sql
CREATE INDEX 索引名称 ON 表名(字段);
ALTER TABLE 表名称 ADD INDEX [索引名](字段);
SHOW INDEX FROM 表名;
DROP INDEX 索引名称 ON 表名;
```



##### 索引的使用原则

- 数据量很大，而且经常被查询的数据表都可以设置索引
- 索引只添加在经常被用作检索条件的字段上面
- 不要在大字段上创建索引



### 数据库操作语言

#### 记录查询

最基本的查询语句是由 SELECT 和 FROM 关键字组成的

```sql
SELECT * FROM t_student;
SELECT id,name,sex FROM t_student;
```

#### 使用列别名

 	通常情况下，SELECT 子句中使用了表达式，那么这列的名字就默认为表达式，因此需要一种对列名重命名的机制

```sql
SELECT
ename,
sal * 12 AS "annual_salary"
FROM emp;
```

重命名只在显示输出时候使用，数据表列名不会真的改变



#### 查询语句的子句执行顺序

```sql
SELECT
ename,
sql * 12 AS "annual_salary"
FROM emp;
```

1. 词法分析与优化：读取SQL语句
2. FROM：选择数据来源
3. SELECT：选择输出内容

#### 数据分页

如果结果集的记录很多，则可以使用LIMIT关键字限定结果集数量

```sql
SELECT ..... FROM ..... LIMIT 起始位置，偏移量;
```

#### 数据分页的简写用法

如果LIMIT子句只有一个参数，它表示的是偏移量，其实默认值为0

```sq
SELECT empno,ename FROM t_emp LIMIT 10;
SELECT empno,ename FROM t_emp LIMIT 0,10;
```

#### 结果集排序：单个字段

如果没有设置，查询语句不会对结果集进行排序。也就是说，如果想让结果集按照某种顺序排列，就必须使用ORDER BY子句。

```sql
SELECT ...... FROM ...... ORDER BY 列名 [ASC][DESC]
```

其中ASC代表升序(默认)，DESC表示(降序)。

如果排序列是数字类型，数据库就按照数字大小排序，如果是日期类型就按照日期大小排序，如果是字符串类型就按照字符串集序号排序。

```sql
SELECT ename,sal FROM t_emp ORDER BY hiredate DESC;
```

当排序字段内容相同时，MySQL会按照主键大小来排序两条数据。

#### 结果集排序：多个排序字段

可以使用 ORDER BY 规定首要排序条件和次要排序条件。

```sql
SELECT empno,ename,sal,hiredate
FROM emp
ORDER BY sal DESC,hiredate ASC;
```



#### 排序+分页

ORDER BY子句书写的时候放在 LIMIT 子句的前面

```
FROM -> SELECT -> ORDER BY -> LIMIT
```



#### 去除重复记录

当我们要查询员工表有多少种职业，写出来的SQL语句如下：

``` sql
SELECT job FROM t_emp
```

此时结果存在重复记录，如果我们要去除重复的数据，可以使用DISTINCT关键字来实现

```sql
SELECT DISTINCT 字段 FROM .....;
```

需要注意：

-  使用DISTINCT的SELECT子句中只能查询一列数据，如果查询多列，去除重复记录就会失效。
-  DISTINCT关键字只能在SELECT子句中使用一次



#### 条件查询

当用户需要取出逻辑表中满足一条或者某几种条件的记录。这类条件要用 WHERE 子句来实现数据的筛选

``` sql
SELECT ... FROM ..... WHERE 条件 [AND][OR] 条件 ...;
```

WHERE 语句中的条件运算会用到以下四类运算符：

| 序号 |   运算符   |
| :--: | :--------: |
|  1   | 数学运算符 |
|  2   | 比较运算符 |
|  3   | 逻辑运算符 |
|  4   | 按位运算符 |

##### 算数运算符

| 序号 | 表达式 | 意义 |  例子  |
| :--: | :----: | :--: | :----: |
|  1   |   +    | 加法 | 1+2+3  |
|  2   |   -    | 减法 | 1-2-3  |
|  3   |   *    | 乘法 | 5 * 35 |
|  4   |   /    | 除法 | 231/15 |
|  5   |   %    | 求模 | 10 % 3 |

##### 比较运算符

| 序号 | 表达式 |   意义   |         例子          |
| :--: | :----: | :------: | :-------------------: |
|  1   |   >    |   大于   |       age > 18        |
|  2   |   >=   | 大于等于 |       age >= 18       |
|  3   |   <    |   小于   |      sal < 3000       |
|  4   |   <=   | 小于等于 |      sal <= 3000      |
|  5   |   =    |   等于   |      deptno = 10      |
|  6   |   !=   |  不等于  |     deptno != 30      |
|  7   |   IN   |  包含于  | deptno IN(10, 30, 40) |


##### 逻辑运算符

| 序号 | 表达式 |   意义   |            例子             |
| :--: | :----: | :------: | :-------------------------: |
|  1   |  AND   |  与关系  |   age > 18 AND sex = "男"   |
|  2   |   OR   |  或关系  | empno = 8000 OR deptno = 20 |
|  3   |  NOT   |  非关系  |       NOT deptno = 20       |
|  4   |  XOR   | 异或关系 |   age > 18 XOR sex = "男"   |


##### 按位运算符

| 序号 | 表达式 |   意义   |  例子   |
| :--: | :----: | :------: | :-----: |
|  1   |   &    |  按位与  |  3 & 7  |
|  2   |   \|   |  按位或  |    3    |
|  3   |   ~    | 按位取反 |   ~10   |
|  4   |   ^    | 按位异或 |  3 ^ 7  |
|  5   |   <<   |   左移   | 10 << 1 |
|  6   |   >>   |   右移   | 10 >> 1 |



#### WHERE子句的注意事项

WHERE 子句中，条件执行的顺序是从左到右的，所以我们应该把索引条件中苛刻的或者筛选掉记录最多的条件写在最左侧。

```sql
SELECT empno,ename FROM t_emp
WHERE ename = "FORD" AND sal >= 2000;

SELECT empno,ename FROM t_emp
WHERE depno = 10 AND sal >= 2000;
```



#### 各种子句的执行顺序

```FROM``` > ```WHERE``` > ```SELECT``` > ```ORDER BY```  > ```LIMIT```



#### 聚合函数

聚合函数在数据的查询分析中应用十分广泛。聚合函数可以对数据求和、求最大值、求最小值和求平均值等。

```sql
SELECT AVG(sal + IFNULL(comm, 0)) FROM t_emp;
```

##### SUM函数

SUM函数用于求和，只能用于数字类型，用于字符类型时统计结果为0，用于统计日期类型时则为毫秒数相加。

SUM函数求和会排除NULL值。



##### MAX函数

MAX 函数会用于获得非空值的最大值

```sql
SELECT MAX(comm) FROM t_emp;
```

例1：查询10和20部门中，月收入最高的员工

```sql
SELECT MAX(sal + IFNULL(comm, 0))
FROM empno
WHERE deptno IN (10, 20);
```

例2：查询员工名字最长为几个字符

```sql
SELECT MAX(LENGTH(ename)) FROM t_emp;
```



##### MIN函数

MIN函数用于获得非空值的最小值

```sql
SELECT MIN(empno) FROM t_emp;
SELECT MIN(hiredate) FROM t_emp;
```



##### AVG函数

AVG函数用于获取非空值的平均值，非数字数据统计结果为0

```sql
SELECT AVG(sal + IFNULL(comm, 0)) FROM t_emp;
SELECT AVG(ename) FROM t_emp;
```



##### COUNT函数

COUNT(*) 用于获得包含空值的记录数，COUNT(列名) 用于获得包含非空值的记录数。

```sql
SELECT COUNT(*) FROM t_emp;
SELECT COUNT(comm) FROM t_emp;
```

例1：查询 10和 20部门中，底薪超过 2000 元并且工龄超过15年的员工人数

```sql
SELECT COUNT(*) FROM t_emp
WHERE deptno IN (10, 20) AND sal >= 2000 AND (DATEDIFF(NOW(), hiredate) / 365) >= 15;
```

例2：查询1985年以后入职的员工，底薪超过公司平均底薪的员工数量

错误示范：因为聚合函数无法在WHERE中使用，所以下方语句会出错

```sql
SELECT COUNT(*) FROM t_emp
WHERE hiredate >= "1985-01-01" AND sal > AVG(sal);
```



#### 分组查询

默认情况下，汇总函数时对全表范围内的数据做统计

GROUP BY子句的作用是通过一定的规则将一个数据集划分成若干的小的区域，然后针对每个小区域分别进行数据汇总处理。

```sql
SELECT deptno, AVG(sal) FROM t_emp
GROUP BY deptno;
```



##### 逐级分组

数据库支持多列分组条件，执行的时候逐级分组。

例1： 查询每个部门里，每种职位的人员数量和平均底薪

```sql
SELECT deptno, job, COUNT(*), AVG(sal)
FROM t_emp GROUP BY deptno, job
ORDER BY deptno;
```

##### 对SELECT子句的要求

查询语句中如果包含GROUP BY 子句，那么SELECT子句中的内容就必须要遵守规定：SELECT子句中可以包括聚合函数，或者GROUP BY子句的分组列，其余内容均不可以出现在SELECT子句中。

```sql
SELECT deptno, COUNT(*), AVG(sal)
FROM t_emp
GROUP BY deptno;
```

错误示范(实际测试的时候可以出结果，不知道是什么原因)：

```sql
SELECT deptno, COUNT(*), AVG(sal), sal
FROM t_emp
GROUP BY deptno
ORDER BY deptno;
```

##### 对分组结果再次进行汇总计算

加上ROLLUP之后，可以对分组结果进行进一步的汇总，下图中可以看出对各部门的工资平均值进行了平均。

```sql
SELECT deptno, COUNT(*), AVG(sal), MAX(sal), MIN(sal)
FROM t_emp GROUP BY deptno WITH ROLLUP;
```

![[resources/image-20211115145725172.png]]

##### GROUP_CONCAT 函数

GROUP_CONCAT 函数可以把分组查询中的某个字段拼接成一个字符串

例1：查询每个部门内底薪超过2000的人员和员工姓名

```sql
SELECT deptno, GROUP_CONCAT(ename), COUNT(*)
FROM t_emp WHERE sal >= 2000
GROUP BY deptno;
```



##### 各种子句的执行顺序

```FROM``` > ```WHERE``` > ```GROUP BY``` > ```SELECT``` > ```ORDER BY``` > ```LIMIT```



##### HAVING 子句

由于 WHERE 子句先于 GROUP BY执行，一旦WHERE子句出现汇总函数，数据库不知道按照什么范围进行计算，所以会出现错误，此时便需要HAVING子句，**HAVING子句必须伴随着GROUP BY子句使用**

例：查询部门平均底薪超过2000元的部门编号

WHERE会出错

```sql
SELECT deptno FROM t_emp
WHERE AVG(sal) >= 2000
GROUP BY deptno;
```

使用HAVING

```sql
SELECT deptno FROM t_emp
WHERE hiredate >= "1982-01-01"
GROUP BY deptno HAVING AVG(sal) >= 2000
ORDER BY deptno;
```

##### HAVING子句的特殊用法

按照数字1分组，MySQL会根据SELECT子句中的列进行分组，HAVING子句也可以正常使用。

HAVING不能使用具体的列来和聚合函数作比较。



#### 表连接查询

从多张表中提取数据时必须指定关联的条件，如果不定义关联条件就会出现无条件连接，两张表的数据就会产生交叉连接，从而产生笛卡尔积。

未定义关联条件

```sql
SELECT empno, ename, dname
FROM t_emp JOIN t_dept;
```

定义了关联条件

```sql
SELECT e.empno, e.ename, d.dname
FROM t_emp e JOIN t_dept d
ON e.deptno = d.deptno;
```

表连接可以分为内连接和外连接

内连接是结果集中只保留符合连接条件的记录

外连接是不管符不符合连接条件，记录都要保留在结果集中



##### 内连接

内连接是最常见的一种表连接，用于查询多张关系表符合连接条件的记录。

```sql
SELECT ...... FROM 表1
[INNER] JOIN 表2 ON 条件
[INNER] JOIN 表3 ON 条件
```

```sql
SELECT ... FROm 表1 JOIN 表2 ON 连接条件;
```

```sql
SELECT ... FROm 表1 JOIN 表2 WHERE 连接条件;
```

```sql
SELECT ... FROm 表1, 表2 WHERE 连接条件;
```

例1： 查询每个员工的工号、姓名、部门名称、底薪、职位、工资等级？

```sql
SELECT empno, ename, dname, sal, job, grade
FROM t_emp e
JOIN t_dept d ON e.deptno = d.deptno
JOIN t_salgrade s ON e.sal BETWEEN s.losal AND s.hisal;
```

**内连接的数据表不一定必须要有同名字段，只要字段之间符合逻辑关系就可以。**

例2： 查询与SCOTT相同部门的员工都有谁？

```sql
SELECT e2.ename
FROM t_emp e1 JOIN t_emp e2
ON e1.deptno = e2.deptno
WHERE e1.ename = "SCOTT" AND e2.ename != "SCOTT";
```

**相同的数据表也可以做表连接**

例3： 查询月薪超过公司平均月薪的员工信息

```sql
SELECt e.ename, e.sal
FROM t_emp e
JOIN (SELECT AVG(sal) AS avg FROM t_emp) avg
ON e.sal > avg;
```

**结果集也可以作为一张表来跟其他表连接**



例4：查询RESERCH部门的人数、最高底薪、最低底薪、平均底薪、平均工龄

```sql
SELECT COUNT(*), MAX(sal), MIN(sal), AVG(sal), FLOOR(AVG(DATEDIFF(NOW(), hiredate) / 365)) 
FROM t_emp e JOIN t_dept d
ON e.deptno = d.deptno
WHERE d.dname = "RESEARCH"
GROUP BY e.deptno;
```

例5：查询每种职业的最高工资、最低工资、平均工资、最高工资等级和
最低工资等级

```sql
SELECT e.job,MAX(sal + IFNULL(comm, 0)) AS max_sal, MIN(sal + IFNULL(comm, 0)) AS min_sal, AVG(sal + IFNULL(comm, 0)) AS avg_sal,
MAX(grade) AS max_grade, MIN(grade) AS min_grade
FROM t_emp e
JOIN t_dept d ON e.deptno = d.deptno
JOIN t_salgrade s ON (e.sal + IFNULL(e.comm, 0)) BETWEEN s.losal AND s.hisal
GROUP BY e.job;
```

例5： 查询每个底薪超过部门平均底薪的员工信息

```sql
SELECT e1.ename, e1.sal
FROM t_emp e1
JOIN (SELECT e.deptno, AVG(sal) AS avg FROM t_emp e JOIN t_dept d ON e.deptno = d.deptno GROUP BY d.dname) e2
ON e1.sal >= e2.avg AND e1.deptno = e2.deptno;
```

##### 外连接

​		使用内连接时会忽略 null 值，需要引入外连接的语法才能解决这个问题

​		外连接和内连接的区别在于，除了符合条件的记录之外，结果集中还会保留不符合条件的记录

###### 左连接和右连接

​		左外连接就是保留左表中所有的记录，与右表左连接。如果右表中有符合条件的及来说就与左表连接，如果右表中没有符合条件的记录，就用NULL与左表连接。右外连接同样。

例1：查询每个部门的名称和部门的人数

```sql
SELECT d.dname, COUNT(e.empno)
FROM t_dept d
LEFT JOIN t_emp e ON d.deptno = e.deptno
GROUP BY d.dname
```

例2：查询每个部门的名称和部门的人数，如果没有部门的员工部门名称使用NULL代替
```sql
SELECT d.dname, COUNT(e.empno)
FROM t_emp e
LEFT JOIN t_dept d ON e.deptno = d.deptno
GROUP BY e.deptno
UNION
SELECT d.dname, COUNT(e.empno)
FROM t_emp e
RIGHT JOIN t_dept d ON e.deptno = d.deptno
GROUP BY d.dname
```
练习：查询每名员工的编号、姓名、部门、月薪、工龄等级、工龄、上司编号、上司姓名、上司部门
```sql
SELECT e.empno, e.ename, d.dname, e.sal + IFNULL(e.comm, 0), s.grade, FLOOR(DATEDIFF(NOW(), e.hiredate) / 365) AS work_years, b.empno AS bno, b.ename AS bname, b.dname AS bdname
FROM t_emp e
LEFT JOIN t_dept d ON e.deptno = d.deptno
LEFT JOIN t_salgrade s ON e.sal BETWEEN s.losal AND s.hisal
LEFT JOIN 
(SELECT e1.empno, e1.ename, d1.dname
FROM t_emp e1
LEFT JOIN t_dept d1 ON e1.deptno = d1.deptno) b
ON e.mgr = b.empno;
```

###### 外连接的注意事项
内连接只保留符合条件的记录，所以查询条件写在ON子句和WHERE子句中的效果是相同的。
但是在外连接里面，条件写在WHERE子句里，不符合条件的记录是会被筛选掉而不是保留下来。

例子：
```sql
# WHERE
SELECT e.empno, e.ename, d.dname
FROM t_emp e
LEFT JOIN t_dept d ON e.deptno = d.deptno
WHERE e.deptno = 10;

# AND
SELECT e.empno, e.ename, d.dname
FROM t_emp e
LEFT JOIN t_dept d ON e.deptno = d.deptno
AND e.deptno = 10;
```
##### UNION关键字
``UNION``关键字可以将多个查询结果的结果集进行合并，但是需要注意查询的字段和查询的字段数量需要相同



#### 子查询
子查询是一种查询中嵌套查询的语句

例：查询底薪超过公司平均底薪的员工的信息
```sql
SELECT e.empno, e.ename
FROM t_emp e
JOIN
(SELECT AVG(e1.sal) AS avg_sal
FROM t_emp e1) avg
ON e.sal > avg.avg_sal
```

子查询可以写在三个地方，WHERE、FROM和SELECT，但是只有**FROM子句子查询**中是最可取的

##### WHERE子查询
WHERE子查询简单，容易理解，但是是效最低的子查询
下例中，比较每条记录时都要执行子查询一次，效率太低，反复被执行的查询被叫做[[相关子查询]], 应避免出现相关子查询。
例：查询底薪超过公司平均底薪的员工信息
```sql
SELECT e.empno, e.ename, e.sal
FROM t_emp e
WHERE e.sal > (SELECT AVG(sal) FROM t_emp)
```
##### FROM子查询
FROM子查询只会执行一次，所以```查询效率很高```
例：查询底薪超过公司平均底薪的员工的信息
```sql
SELECT e.empno, e.ename
FROM t_emp e
JOIN
(SELECT AVG(e1.sal) AS avg_sal
FROM t_emp e1) avg
ON e.sal > avg.avg_sal
```
##### SELECT子查询
SELECT子查询每输出一条记录时都要执行一次，所以查询效率很低
PS: 有类似左连接的效果
例：查询每个员工的编号、姓名和部门名称
```sql
SELECT empno, ename, (SELECT dname FROM t_dept WHERE deptno = e.deptno) AS dname
FROM t_emp e
```

##### 单行子查询和多行子查询
- 单行子查询的结果只能有一条记录，多行子查询的结果集中有多个记录
- 多行子查询只能出现在FROM和WHERE子句中

例：用子查询查找FORD和MARTIN两个人的同事
```sql
# 用 WHERE 子查询做
SELECT empno, ename, deptno
FROM t_emp
WHERE deptno IN (SELECT deptno FROM t_emp WHERE ename IN ("FORD", "MARTIN"))
AND ename NOT IN ("FORD", "MARTIN")

# 用 FROM 子查询做
SELECT e1.empno, e1.ename, e1.deptno
FROM t_emp e1
JOIN t_emp e2 ON e2.ename IN ("FORD", "MARTIN") AND e1.deptno = e2.deptno AND e1.ename NOT IN ("FORD", "MARTIN")
```

##### WHERE中的多行子查询
WHERE子句中可以使用IN、ALL、ANY、EXISTS等关键字来处理多行表达式结果集中的条件判断
例：查询比FORD和MARTIN底薪都高的员工信息
```sql
SELECT empno, ename, sal
FROM t_emp
WHERE sal > ALL(SELECT sal FROM t_emp WHERE ename IN ("FORD", "MARTIN"))
```
###### EXISTS关键字
EXISTS关键字是把原来在子查询之外的条件判断，写到了子查询里面
例：查询工资等级是三级或者四级的员工信息
```sql
# 其中EXISTS子句中选择的字段无所谓，只要结果不为空就可以
SELECT ename
FROM t_emp
WHERE EXISTS
(SELECT sal 
FROM t_salgrade 
WHERE sal BETWEEN losal AND hisal
AND grade IN ("3", "4"))

```


### 对数据的基本操作
#### INSERT语句
INSERT可以向数据表写入记录，可以是一条记录，也可以是多条记录
```sql
# 插入一条
INSERT INTO 表名(字段1, 字段2, 字段3....)
VALUES(值1, 值2, 值3....);

# 插入多条
INSERT INTO 表名(字段1, 字段2, 字段3....)
VALUES(值1, 值2, 值3....),(值1, 值2, 值3....);
```
可以不把字段名写出来，但是会影响MySQL执行效率， 如果不声明字段名，MySQL在插入时就会查找表结构，所以尽量在插入时把字段声明出来 

练习：向技术部添加一条员工记录
```sql
INSERT INTO t_emp(empno, ename, job, mgr, hiredate, sal, comm, deptno)
VALUES
(8848, "狂徒张三", "MANAGER", 7901, "2021-12-21", 1000, Null, (SELECT deptno FROM t_dept WHERE dname="技术部"));
```
INSERT语句也可以插入子查询，但是必须是单行子查询，多行子查询的结果是无法插入的。

##### INSERT子句方言
SQL语句方言只支持一种数据库，MySQL方言支持MySQL数据库，但是不支持Oracal和SQL Server
```sql
INSERT INTO 表名 SET 字段1=值1, 字段2=值2,.....;
```

例:
```sql
INSERT INTO t_emp(empno, ename, job, mgr, hiredate, sal, comm, deptno)
VALUES
(8848, "狂徒张三", "MANAGER", 7901, "2021-12-21", 1000, Null, (SELECT deptno FROM t_dept WHERE dname="技术部"))
```

##### IGNORE关键字
当插入的数据和数据库中已有的数据有冲突时会导致INSERT语句中所有的数据都无法插入，此时需要使用IGNORE关键字

- IGNORE关键字会让INSERT只插入数据库中不存在的数据
```sql
INSESR [IGNORE] INTO 表名 ...;
```

例：10因为冲突会被舍弃，90未冲突，所以会被插入
```sql
INSERT IGNORE INTO t_dept(deptno, dname, loc)
VALUES
(10, "A", "天津"),
(90, "B", "上海");
```

#### UPDATE语句
UPDATE语句用于修改表的记录
```sql
UPDATE [IGNORE] 表名
SET 字段1 = 值1, 字段2 = 值2, ....
[WHERE 条件1.....]
[ORDER BY ....]
[LIMIT ....];
```
执行顺序:  ``UPDATE``>``WHERE``>``ORDER BY``>``LIMIT``>``SET``
其中：
WHERE可以控制要修改的数据范围，不加WHERE就是全表范围修改
ORDER BY：当有需要将id等主键字段变化时可能引起冲突，此时使用ORDER BY关键字来防止这种情况出现
LIMIT：在UPDATE中只可以有一个参数，也就是只可以限制分页中第一页的内容

练习1：将每个员工的编号和上司的编号+1，用ORDER BY子句完成
```sql
UPDATE t_emp
SET empno = empno+1, mgr = mgr+1
ORDER BY empno DESC;
```
练习2：把月收入前三名的员工底薪减100元，用LIMIT子句完成
```sql
UPDATE t_emp
SET sal = sal-100
ORDER BY sal + IFNULL(comm, 0) DESC
LIMIT 3;
```
练习3：把10部门中，工龄超过20年的员工，底薪增加200元
```sql
UPDATE t_emp
SET sal = sal + 200
WHERE FLOOR(DATEDIFF(NOW(),IFNULL(hiredate, "9999-01-01")) / 365) >= 20 AND deptno = 10;
```
练习4：将ALLEN调往RESERCH部门，职务调整为ANALYST
```sql
# 相关子查询(不推荐)
UPDATE t_emp
SET deptno=(SELECT deptno FROM t_dept WHERE dname="RESEARCH"), job="ANALYST"
WHERE ename="ALLEN";

# 表连接（推荐）
UPDATE t_emp e JOIN t_dept d ON 
SET e.deptno=d.deptno, e.job = "ANALYST"
WHERE e.ename = "ALLEN" AND d.dname = "RESEARCH";
```

##### UPDATE中的表连接
因为相关子查询的查询效率非常低，所以我们可以利用表连接的方式来改造UPDATE语句
表示方式1：
```sql
UPDATE 表1 JOIN ON 表2 ON 条件
SET 字段1=值1, 字段2=值2,....;
```
表示方式2：
```sql
UPDATE 表1, 表2
SET 字段1 = 值1, 字段2 = 值2
WHERE 连接条件;
```
表连接的UPDATE语句可以修改多张表的记录

表示方式3：
```sql
UPDATE 表1 [LEFT | RIGHT] JOIN 表2 ON 条件
SET 字段1 = 值1, 字段2=值2;
```

练习1：把底薪低于公司平均底薪的员工，底薪增加150元
```sql
UPDATE t_emp JOIN (SELECT AVG(sal) AS avg_sal FROM t_emp) avg ON sal < avg.avg_sal
SET sal = sal + 150;
```

练习2：把没有部门的员工，或者SALES部门低于2000元底薪的员工都调往20部门
```sql
UPDATE t_emp e
LEFT JOIN t_dept d ON e.deptno = d.deptno
SET e.deptno = 20
WHERE (d.dname = "SALES" AND e.sal < 2000)  OR e.deptno IS NULL;
```


#### DELETE语句
DELETE语句用于删除记录
执行顺序：``FROM``>``WHERE``>``ORDER BY``>``LIMIT``>``DELETE``
```sql
DELETE [IGNORE] FROM 表名
[WHERE 条件1, 条件2 ...]
[ORDER BY ...]
[LIMIT ...];
```
IGNORE关键字用于在删除操作被外键约束阻止时继续操作

练习1：删除10部门中，工龄超过40年的员工记录
```sql
DELETE FROM t_emp
WHERE deptno=10 AND FLOOR(DATEDIFF(NOW(), hiredate) / 365) >= 40;
```

练习2：删除20部门中工资最高的员工记录
```sql
DELETE FROM t_emp
WHERE deptno = 20
ORDER BY sal + IFNULL(comm, 0) DESC
LIMIT 1;
```



##### DELETE子句中的表连接
因为相关子查询效率很低，所以可以利用表连接的方式改造DELETE子句
```sql
DELETE 表1,... FROM 表1 JOIN 表2 ON 连接条件
[WHERE 条件1, 条件2 ...]
[ORDER BY ...]
[LIMIT ...];
```
练习1：删除SALES和该部门所有的员工记录
```sql
DELETE e,d
FROM t_emp e JOIN t_dept d ON e.deptno = d.deptno
WHERE d.dname = "SALES";
```

练习2：删除每个低于部门平均底薪的员工记录
```sql
DELETE e
FROM t_emp e JOIN (SELECT deptno,AVG(sal) AS sal FROM t_emp GROUP BY deptno) avg ON e.deptno = avg.deptno
WHERE e.sal < avg.sal;
```

练习3：删除员工KING和他的直接下属的员工记录，用表连接实现
```sql
DELETE e
FROM t_emp e JOIN (SELECT empno FROM t_emp WHERE ename="KING") k ON e.mgr = k.empno OR e.ename = "KING";
```

###### DELETE子句中的外连接
```sql
DELETE 表1,... FROM 表1 [LEFT | RIGHT] JOIN 表2
ON 条件...;
```

例1：删除SALES部门的员工以及没有部门的员工
```sql
DELETE e
FROM t_emp e LEFT JOIN t_dept d ON e.deptno = d.deptno
WHERE d.dname = "SALES" OR e.deptno IS NULL;
```

##### 快速删除数据表中所有数据
DELETE语句是在事务机制下删除记录，删除记录之前先要把将要删除的记录保存到日志文件中，然后再删除记录。

[[TRUNCATE]]语句是在事务机制之外删除记录，速度远远超过DELETE语句
```sql
TRUNCATE TABLE 表名;
```


### MySQL函数
函数分类：
- 数字函数
- 字符函数
- 日期函数
- 条件函数

#### 数字函数
| 函数 | 功能 | 用例 |
| :--: | :--: | :--: |
| ABS | 绝对值 | ABS(-100) |
| ROUND | 四舍五入 | ROUND(3.14) |
| FLOOR | 强制舍位到最近的整数 | FLOOR(9.9) |
| CEIL | 强制进位到最近的整数 | CEIL(3.14) |
| POWER | 幂函数 | POWER(2, 3) |
| LOG | 对数函数 | LOG(4, 2) |
| LN | 对数函数 | LN(10) |
| SQRT | 开平方 | SQRT(9) |
| PI | 圆周率 | PI() |
| SIN | 三角函数 | SIN(弧度) |
| COS | 三角函数 | COS(弧度) |
| TAN | 三角函数 | TAN(弧度) |
| COT | 三角函数 | COT(弧度) |
| RADIANS | 角度转换弧度 | RADIANS(30) |
| DEGREES | 弧度转换角度 | DEGREES(1) |

#### 时间函数
- NOW() 获取系统日期和时间，格式yyyy-MM-dd hh:mm:ss
- CURDATE() 获取当前系统日期，格式yyyy-MM-dd
- CURTIME() 函数能获得当前系统时间，格式hh:mm:ss

##### 日期格式化函数
- DATE_FORMAT()函数用于格式化日期，返回用户想要的日期格式。
	DATE_FORMAT(日期，表达式)
	例：
	```sql
	select ename, DATE_FORMAT(hiredate, "%Y") FROM t_emp;
	```
	| %Y | %m | %d | %w | %W | %j | %U | %H | %h | %i | %s | %r | %T |
	| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
	| 年份 | 月份 | 日期 | 星期(数字) | 星期(名称) | 本年第几天 | 本年第几周 | 小时(24) | 小时(12) | 分钟 | 秒 | 时间(12) | 时间(24) |
	
	##### 日期计算函数
	日期计算的注意事项：
		MYSQL数据库里面，两个日期不能直接相加减，日期也不能和数字直接相加减
	- DATE_ADD() 函数可以实现日期的偏移计算，而且时间单位很灵活
		DATE_ADD(日期, INTERVAL 偏移量 时间单位)
		例子：
		```sql
		SELECT DATE_ADD(NOW(), INTERVAL 2 DAY);
		SELECT DATE_ADD(NOW(), INTERVAL -300 MINUTE);
		
		# 向前偏移两个月零三天
		SELECT DATE_ADD(DATE_ADD(NOW(), INTERVAL -2 MONTH), INTERVAL -3 DAY);
		```
	- DATE_DIFF() 函数用来计算两个日期之间相差的天数
		DATE_DIFF(日期, 日期)
#### 字符函数
| 函数 | 功能 | 用例 |
| :--: | :--: | :--: |
| LOWER | 转换小写字符 | LOWER(HELLO) |
| UPPER | 转换大写字符 | UPPER(hello) |
| LENGTH | 字符数量 | LENGTH(hello) |
| CONCAT | 连接字符串 | CONCAT(sal, "$") |
| INSTR | 字符出现的位置 | INSTR(ename, "A") |
| INSERT | 插入/替换字符 | INSERT("你好", 1, 0(偏移量), "先生") |
| REPLACE | 替换字符 | REPLACE("你好", "先生"， ”女士“) |
| SUBSTR |  截取字符串 | SUBSTR("你好世界", 3, 4) |
| SUBSTRING | 截取字符串 | SUBSTRING("你好世界", 3, 2) |
| LPAD | 左侧填充字符 | LPAD("Hello", 10, "\*") |
| RPAD | 右侧填充字符 | RPAD("Hello, 10, "\*" |
| TRIM | 去除首尾空白字符 | TRIM(" 你好先生 ") |

#### 条件函数
- IFNULL(表达式, 值)
- IF(表达式, 值1, 值2)
	例：中秋节部门发礼品，SALES部门的人发A礼品，其余部门的人发B礼品
	```sql
	SELECT e.ename, d.dname,IF(d.dname = "SALES", "A", "B") AS gift
	FROM t_emp e JOIN t_dept d ON e.deptno = d.deptno;
	```
- 复杂条件判断：
	```sql
	CASE
		WHEN 表达式 THEN 值1
		WHEN 表达式 THEN 值2
		...
		ELSE 值N
	END
	```
	例：公司组织旅游，SALES部门去P1旅游，ACCOUNTING部门去P2，RESEARCH部门去P3，查询每名员工的旅行地点
	```sql
	SELECT 
		e.ename, d.dname,
		CASE
			WHEN d.dname = "SALES" THEN "P1"
			WHEN d.dname = "ACCOUNTING" THEN "P2"
			WHEN d.dname = "RESEARCH" THEN "P3"
		END
		AS location
	FROM t_emp e JOIN t_dept d ON e.deptno = d.deptno;
	```
	例：公司决定为员工调整基本工资，具体调整方案如下：
![[resources/Pasted image 20211229170003.png]]
```sql
	UPDATE t_emp e
	LEFT JOIN t_dept d ON e.deptno = d.deptno
	LEFT JOIN (SELECT deptno, AVG(sal) avg_sal FROM t_emp GROUP BY deptno) a ON a.deptno = e.deptno
	SET e.sal = (
		CASE
			WHEN d.dname = "SALES" AND FLOOR(DATEDIFF(NOW(), e.hiredate)/365) >= 20 THEN e.sal * 1.1
			WHEN d.dname = "SALES" AND FLOOR(DATEDIFF(NOW(), e.hiredate)/365) < 20 THEN e.sal * 1.005
			WHEN d.dname = "ACCOUNTING" THEN e.sal + 300
			WHEN d.dname = "RESEARCH" AND e.sal < a.avg_sal THEN e.sal + 200
			WHEN e.deptno IS NULL THEN e.sal + 100
			ELSE e.sal
		END
	);
```


### MySQL事务机制

事务机制可以避免直接操作数据文件
MySQL共有5中日志，其中只有 redo 和 undo 日志和事务有关
![[resources/Pasted image 20211229191619.png]]
undo日志: sql操作的记录会被拷贝到undo日志中
redo日志: sql增删改查等日志会被记录在redo日志中
当redo中的操作完成之后就会将redo日志和数据库进行同步

RDBMS = SQL语句 + 事务(ACID)
事务是一个或者多个SQL语句组成的整体，要么全部执行完成，要么全部执行失败

#### 管理事务
- 默认情况下，MySQL执行每条SQL语句都会开启自动开启和提交事务
- 为了让多条SQL语句纳入到一个事务中，可以手动管理事务
- 在开启事务和提交/回滚日志中间的操作是保存在redo日志文件中的，只要日志文件没有和数据库做同步，那么数据库中保存的数据就没有发生改变。
- 持久化的是操作后的结果而不是中间的状态
	```sql
		START TRANSACTION;
		SQL语句
		[COMMIT | ROLLBACK];
	```
例：把10部门中的MANAGER员工调往20部门，其他岗位的员工调往30部门，然后删除10部门
![[resources/Pasted image 20211229192211.png]]

```sql
	START TRANSACTION;

	UPDATE t_emp
	SET deptno = IF(job = "MANAGER", 20, 30)
	WHERE deptno = 10;

	DELETE FROM t_dept
	WHERE deptno = 10;

	COMMIT;
```

#### 事务的ACID特性
- 原子性: 一个事务中的操作要么全部完成，要么全部失败，事务执行后不允许停留在中间某个状态
- 一致性: 不管任何时间，并发事务有多少，事务必须保持运行结果的一致性
- 隔离性: 事务不受其他并发事务的影响，如同在给定的时间内，该事务是数据库唯一运行的事务
	- 默认情况下A事务只能看到日志中该事务的相关数据
- 持久性: 事务一旦提交，结果便是永久性的。即使发生宕机，仍旧可以依靠事务日志完成数据的持久化。

#### 事务的隔离级别
| 序号 | 隔离级别 | 功能 |
| :--: | :--: | :--: |
| 1 | read uncommitted | 读取未提交数据 |
| 2 | read committed | 读取已提交数据 |
| 3 | repeatable read | 重复读取 |
| 4 | serializable | 序列化 |

设置事务的隔离级别：
```sql
	SET SESSION TRANSACTION ISOLATION LEVEL 隔离级别;

```
使用何种的隔离级别需要根据业务来确定
- 业务场景1：购票
	![[resources/Pasted image 20211229195950.png]]
	由于事物之间的隔离性，A事务将1A坐席售出后，B事务看不见，B事务便可能将1A坐席再次售出，由于A事务还没有提交，当B事务提交后，A事务发现1A坐席被售出了，所以A事务会发生回滚操作。
	在这个场景中，我们应该允许事务之间读取其他事务未提交的临时数据。

- 业务场景2：转账场景
	![[resources/Pasted image 20211229200501.png]]
	在读取未提交数据的隔离级别下：
	当A事务开启事务但是还没有开始执行转账的操作，此时B事务已经开启并且执行了支出100元的操作，此时账户余额为4900元，当A执行转账操作之后，账户余额会变成5900块钱，但是
		1. 如果A和B都正常提交，账户余额会变为5900块钱，没有出错
		2. 如果B事务没有提交而是回滚了，A事务提交后账户余额变为5900块钱，而B事务回滚后账户余额仍是5900块钱，此时账户余额便会变成5900块钱，少了100块钱。
	这个业务场景应该使用READ COMMITTED。

- 场景3：购物时涨价场景
	![[resources/Pasted image 20211229201101.png]]
	当用户下单之后还未付款，但是商家将商品价格涨价了，此时用户应该按照涨价之前的商品价格去付款，此时需要让A事务的执行不受到B事务的影响，此时使用REPEATABLE READ。
	
	REPEATABLE READ 会读取undo日志中的内容，需要先执行一条能够让数据加载到undo日志中的操作才会使得查询出来的数据时正确的。
- SERIALIZEABLE
	由于事务并发执行所带来的各种问题，前三种隔离级别只适用在某些业务场景中，但是序列化的隔离性会让事务逐一执行，也就不会产生上述问题了。
	但是序列化可以避免上述问题的发生，但是序列化会让数据库的并发性急剧下降。所以不会经常使用。
	
### 数据导出和备份
- 数据导出和备份的区别
	- 数据导出：导出的纯粹是业务数据
	- 数据备份：备份的是数据文件，日志文件，索引文件等
	- 备份分为全量备份和增量备份
#### 数据导出
- SQL文档：数据不多
- 文本文档：数据很多

##### 导出SQL文件
mysqldump用来将业务文件导出成SQL文件，其中也包括了表结构
```sql
	mysqldump -uroot -p [no-data] 逻辑库>路径;
```
##### 导入SQL文件
source 命令用于导入sql文件，包括创建数据表，写入记录等
```sql
USE 数据库名;
SOURCE SQL文件存放路径.sql;
```
##### 导出为文本文档并且导入
导出：
1. 先将表结构导出为sql文件
2. 在navicat的导出向导中将数据导出为txt文件
导入：
1. 先运行导出的表结构的sql文件
2. 在navicat的导入向导中将txt的数据文件导入



## JDBC
### JDBC 开发流程
1. 加载并注册JDBC驱动
2. 创建数据库连接
3. 创建Statement对象
4. 遍历查询结果
5. 关闭连接，释放资源

### JDBC驱动
#### JDBC驱动下载
搜索对应数据库+driver，如mysql driver进入官网下载，由于就java是跨平台语言，所以windows如没有对应jar包可以下载linux的tar包解压后获取。

#### Class.forName的作用
- Class.forName 用于加载指定的JDBC驱动类
- Class.forName 的本质是通知JDBC注册这个驱动类
- 驱动由数据库厂商自行开发，连接字符串不同

| 数据库 | JDBC驱动类 | 连接字符串 |
| :--: | :--: | :--: |
| MySQL5 | com.mysql.jdbc.Driver | jdbc:mysql//主机ip:端口/数据库名 |
| MySQL8 | com.mysql.cj.jdbc.Driver | jdbc:mysql://主机ip:端口/数据库名 |
| Oracle | oracle.jdbc.driver.OracleDriver | jdbc:oracle::thin:@主机ip:端口:数据库名 |
| SQL Server | com.microsoft.sqlserver.jdbc.SQLServerDriver | jdbc:microsoft:sqlserver:主机ip:端口;databasename=数据库名 |

#### 创建数据库连接代码
```java
String dbDriver = "com.mysql.cj.jdbc.Driver"; //JDBC驱动类
String dbURL = "jdbc:mysql://localhost:3306/imooc"; //连接字符串
String dbUsername = "root"; // 数据库用户名
String dbPassword = "123456"; //数据库密码
// 1. 加载并注册jdbc驱动
Class.forName(dbDriver);
// 2. 创建数据库连接
Connection connection = DriverManager.getConnection(dbURL, dbUsername, dbPassword);
```

#### 数据库连接配置
##### DriverManager
- DriverManager 用于注册/管理JDBC驱动程序
- DriverManager.getConnection(连接字符串, 用户名, 密码)
- 返回值 Connection 对象, 对应数据库的物理网络连接

##### Connection 对象
- Connection对象用于JDBC与数据库的网络通信对象
- java.sql.Connection是一个接口, 具体由驱动厂商实现
- 所有数据库的操作都建立在Connection基础上

##### MySQL连接字符串
- 格式: jdbc:mysql://\[主机ip\]:\[端口\]/数据库名?参数列表
- 主机ip与端口是可选配置, 默认值为127.0.0.1和3306
- 参数列表采用url编码, 格式: 参数1=值1&参数2=值2&....

###### MySQL连接字符串常用参数
| 参数 | 建议参数值 | 说明 |
| :--: | :--: | :--: |
| useSSL | true(生产) false(开发) | 是否禁用SSL |
| useUnicode | true | 启用unicode编码传输数据 |
| characterEncoding | UTF-8 | 使用UTF-8编码传输数据 |
| serverTImezone | Asia/Shanghai | 使用东8区时间, UTC+8 |
| allowPublicKeyRetrieval | true | 允许从客户端获取公钥加密传输 | 

### SQL注入攻击
当输入的语句被黑客加上特殊的语句时会被套出数据库的信息
- SQL注入攻击是指利用SQL漏洞越权获取数据的黑客行为
- SQL注入攻击根源是未对原始SQL中的敏感字符做特殊处理
- 解决方法: 放弃Statement改用PreparedStatement处理SQL
如:
```sql
# 当需要输入部门名称时
SELECT * FROM employee WHERE dname='" + qdname + "'
# 原来正常输入
select \* from employee where dname = '部门名称'

# 注入攻击, 输入 ' or 1=1 or 1=' 此时会出现该表中所有数据
SELECT * FROM employee WHERE dname='' or 1=1 or 1=''
```

### PreparedStatement
- 预编译Statement，是Statement的子接口
- PreparedStatement可以对SQL进行参数化，预防SQL注入攻击
- PreparedStatement比Statement的执行效率更高
使用：
```java
// 利用PreparedStatement预防SQL注入风险
// 当dname值为' or 1=1 or 1=' 时查询不到任何结果
// SQL: SELECT * FROM employee WHERE dname='\' or 1=1 or 1=\''
String sql = "select * from employee where dname=?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setString(1, dname); // 设置SQL参数, 参数从1开始
Result rs = pstmt.executeQuery();
while(rs.next()) {
	...
}
```
PrepareStatement 对sql语句中的特殊字符进行了转义处理，从而避免了被SQL注入攻击。

### DbUtils
对于获取数据库连接和关闭连接的操作，由于每个使用jdbc的程序都要用到这段代码，我们可以将这两段代码封装为一个工具类。
```java
package com.imooc.jdbc.hrapp.common;  
  
import java.sql.*;  
  
public class DbUtils {  
    public static Connection getConnection() throws ClassNotFoundException, SQLException {  
        Class.forName("com.mysql.cj.jdbc.Driver");  
        String dbURL = "jdbc:mysql://localhost:3306/imooc?useSSL=false&useUnicode=true&characterEncoding=UTF-8" +  
                "&serverTimezone=Asia/Shanghai&allowRetrieval=true";  
        String dbUsername = "root";  
        String dbPassword = "Ms.990218";  
        Connection conn = DriverManager.getConnection(dbURL, dbUsername, dbPassword);  
        return conn;  
    }  
  
    public static void closeConnection(ResultSet rs, Statement stmt, Connection conn){  
        try {  
            if (rs != null) {  
                rs.close();  
            }  
            if (stmt != null) {  
                stmt.close();  
            }  
            if (conn != null && !conn.isClosed()) {  
                conn.close();  
            }  
        } catch (SQLException e) {  
            e.printStackTrace();  
        }  
    }  
}
```


### JDBC增删改查
- 新增职员
```java
package com.imooc.jdbc.hrapp.command;  
  
import com.imooc.jdbc.hrapp.common.DbUtils;  
  
import java.sql.Connection;  
import java.sql.PreparedStatement;  
import java.sql.SQLException;  
import java.util.Scanner;  
  
public class InsertCommand implements Command {  
    @Override  
 public void execute() {  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
        try {  
            Scanner in = new Scanner(System.in);  
            System.out.println("请输入员工编号:");  
            Integer eno = in.nextInt();  
            System.out.println("请输入员工姓名:");  
            String ename = in.next();  
            System.out.println("请输入员工薪资:");  
            Float salary = in.nextFloat();  
            System.out.println("请输入员工所属部门:");  
            String dname = in.next();  
            conn = DbUtils.getConnection();  
            String sql = "INSERT INTO employee(eno, ename, salary, dname) VALUES(?, ?, ?, ?)";  
            pstmt = conn.prepareStatement(sql);  
            pstmt.setInt(1, eno);  
            pstmt.setString(2, ename);  
            pstmt.setFloat(3, salary);  
            pstmt.setString(4, dname);  
  
            int cnt = pstmt.executeUpdate();  
            System.out.println("cnt: " + cnt);  
            if (cnt != 0) {  
                System.out.println(ename + "员工入职手续办理完成");  
            }  
        } catch (ClassNotFoundException e) {  
            e.printStackTrace();  
        } catch (SQLException e) {  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(null, pstmt, conn);  
        }  
  
    }  
}
```
- 更新职员信息
```sql
package com.imooc.jdbc.hrapp.command;  
  
import com.imooc.jdbc.hrapp.common.DbUtils;  
  
import java.sql.Connection;  
import java.sql.PreparedStatement;  
import java.sql.SQLException;  
import java.util.Scanner;  
  
public class UpdateCommand implements Command{  
  
    @Override  
 public void execute() {  
        Scanner in = new Scanner(System.in);  
        System.out.println("请输入员工的编号:");  
        Integer eno = in.nextInt();  
        System.out.println("请输入调整后的薪资:");  
        Float salary = in.nextFloat();  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
        try {  
            conn = DbUtils.getConnection();  
            String sql = "update employee set salary = ? where eno = ?";  
            pstmt = conn.prepareStatement(sql);  
            pstmt.setFloat(1, salary);  
            pstmt.setInt(2, eno);  
            int cnt = pstmt.executeUpdate();  
            System.out.println("cnt: " + cnt);  
            if (cnt != 0) {  
                System.out.println(eno + "的员工薪资已调整为" + salary + "元");  
            } else {  
                System.out.println("数据库中暂无此员工");  
            }  
        } catch (ClassNotFoundException e) {  
            e.printStackTrace();  
        } catch (SQLException e) {  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(null, pstmt, conn);  
        }  
    }  
}
```
- 删除职员
```java
package com.imooc.jdbc.hrapp.command;  
  
import com.imooc.jdbc.hrapp.common.DbUtils;  
  
import java.sql.Connection;  
import java.sql.PreparedStatement;  
import java.sql.SQLException;  
import java.util.Scanner;  
  
public class DeleteCommand implements Command{  
  
    @Override  
 public void execute() {  
        Scanner in = new Scanner(System.in);  
        System.out.println("请输入要离职的员工编号");  
        Integer eno = in.nextInt();  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
        try {  
            conn = DbUtils.getConnection();  
            String sql = "delete from employee where eno = ?";  
            pstmt = conn.prepareStatement(sql);  
            pstmt.setInt(1, eno);  
            int cnt = pstmt.executeUpdate();  
            if (cnt != 0) {  
                System.out.println(eno + "的离职手续办理完成");  
            } else {  
                System.out.println("数据库中无此员工");  
            }  
        } catch (ClassNotFoundException e) {  
            e.printStackTrace();  
        } catch (SQLException e) {  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(null, pstmt, conn);  
        }  
    }  
}
```

- 查询职员(此段代码未使用DbUtils工具类)
```java
package com.imooc.jdbc.hrapp.command;  
  
import java.sql.*;  
import java.util.Scanner;  
  
public class PstmtQueryCommand implements Command{  
    @Override  
    public void execute() {  
        System.out.println("请输入部门名称");  
        Scanner in = new Scanner(System.in);  
        String qdname = in.next();  
        String dbDriver = "com.mysql.cj.jdbc.Driver";  
        String dbURL = "jdbc:mysql://localhost:3306/imooc?useSSL=false&useUnicode=true&characterEncoding=UTF-8" +  
                "&serverTimezone=Asia/Shanghai&allowPublicKeyRetrieval=true";  
        String dbUsername = "root";  
        String dbPassword = "Ms.990218";  
        Connection conn = null;  
//        Statement stmt = null;  
 PreparedStatement pstmt = null;  
        ResultSet rs = null;  
        try {  
            Class.forName(dbDriver);  
            conn = DriverManager.getConnection(dbURL, dbUsername, dbPassword);  
            String sql = "SELECT * FROM employee WHERE dname=? and eno > ?";  
            pstmt = conn.prepareStatement(sql);  
            pstmt.setString(1, qdname);  
            pstmt.setInt(2, 3000);  
//            stmt = conn.createStatement();  
 rs = pstmt.executeQuery();  
//            System.out.println("SELECT * FROM employee WHERE dname='" + qdname + "'");  
//            rs = stmt.executeQuery("SELECT * FROM employee WHERE dname='" + qdname + "'");  
 while (rs.next()) {  
                Integer eno = rs.getInt("eno");  
                String ename = rs.getString("ename");  
                Float salary = rs.getFloat("salary");  
                String dname = rs.getString("dname");  
                Date hiredate = rs.getDate("hiredate");  
                System.out.println(eno + "-" + ename  + "-" + salary + "-" + dname + "-" + hiredate);  
            }  
        } catch (ClassNotFoundException e) {  
            e.printStackTrace();  
        } catch (SQLException e) {  
            e.printStackTrace();  
        } finally {  
            if (conn != null) {  
                try {  
                    if (rs != null) {  
                        rs.close();  
                    }  
                    if (pstmt != null) {  
                        pstmt.close();  
                    }  
                    if (conn != null && !conn.isClosed()) {  
                        conn.close();  
                    }  
                } catch (SQLException e) {  
                    e.printStackTrace();  
                }  
            }  
        }  
    }  
}
```

### JDBC事务
#### 事务
- 事务是以一种可靠的、一致的方式，访问和操作数据库的程序单元
- 要么把事情全做完，要么一件也不做，不会将事情只做一半
- 事务依赖于数据库实现，MySQL通过事务区作为数据缓冲地带
#### 事务的提交操作
![[resources/Pasted image 20220105222335.png]]
#### 事务的回滚操作
![[resources/Pasted image 20220105222424.png]]
#### JDBC两种事务模式
- JDBC允许两种事务模式
- 自动提交事务模式
- 手动提交事务模式
##### 自动提交事务模式
- 自动提交事务模式是指每执行一次SQL操作，自动提交事务
- 自动提交开启方法：conn.setAutoCommit(true)
- 自动事务是JDBC默认行为，此模式无法保证多数据一致性
##### 手动提交事务模式
- 手动提交事务模式是指显式调用commit()和rollback()方法管理事务
- 手动提交开启方法: conn.setAutoCommit(false)
- 手动提交事务可保证多数据一致性, 但必须手动调用提交/回滚方法

#### JDBC中Date日期对象的处理
sql中date和datetime在java中被处理时都被当做Date处理。
ResultSet获取sql中日期类型的对象时选择sql包下的Date，实体类中选择util包下的Date。
由于sql下的Date继承自Util包下的Date，所以可以将获取的sql包下的Date对象直接赋值给实体类中util包下的Date

##### 将字符串转换为sql下的Date
1. 将字符串转化为util下的Date
```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
java.util.Date udHiredate = sdf.parse(strHiredate);

```
2. 将util下的Date转换为sql下的Date
```java
long time = udHiredate.getTime(); //获取时间戳
java.sql.Date sdHiredate = new java.sql.Date(time);
```

#### JDBC数据批处理
单条处理数据：每次初始化一次preparestatement参数，每次执行一次sql语句
```java
private static void tc1() {  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
  
        try {  
            long startTime = new Date().getTime();  
            conn = DbUtils.getConnection();  
            conn.setAutoCommit(false);  
            for (int i = 100000; i < 200000; i++) {  
//                if (i == 1005) {  
//                    throw new RuntimeException("插入失败");  
//                }  
 Integer eno = i;  
                String ename = "员工" + i;  
                Float salary = 1000f;  
                String dname = "研发部";  
                String sql = "insert into employee(eno, ename, salary, dname) VALUES(?, ?, ?, ?)";  
                pstmt = conn.prepareStatement(sql);  
                pstmt.setInt(1, eno);  
                pstmt.setString(2, ename);  
                pstmt.setFloat(3, salary);  
                pstmt.setString(4, dname);  
                pstmt.executeUpdate();  
            }  
            conn.commit();  
            long endTime = new Date().getTime();  
            System.out.println("tc1执行时长：" + (endTime - startTime));  
        } catch (Exception e) {  
            try {  
                conn.rollback();  
            } catch (SQLException ex) {  
                ex.printStackTrace();  
            }  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(null, pstmt, conn);  
        }  
    }

```
批处理处理数据：在插入数据之前初始化preparestatement参数，然后将每一条数据插入到批处理任务中, 最后一次执行
```java
private static void tc2() {  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
  
        try {  
            long startTime = new Date().getTime();  
            conn = DbUtils.getConnection();  
            conn.setAutoCommit(false);  
  
            String sql = "insert into employee(eno, ename, salary, dname) VALUES(?, ?, ?, ?)";  
            pstmt = conn.prepareStatement(sql);  
            for (int i = 200000; i < 300000; i++) {  
//                if (i == 1005) {  
//                    throw new RuntimeException("插入失败");  
//                }  
 Integer eno = i;  
                String ename = "员工" + i;  
                Float salary = 1000f;  
                String dname = "研发部";  
                pstmt.setInt(1, eno);  
                pstmt.setString(2, ename);  
                pstmt.setFloat(3, salary);  
                pstmt.setString(4, dname);  
//                pstmt.executeUpdate();  
  
 pstmt.addBatch(); //将参数加入到批处理任务中  
 }  
            pstmt.executeBatch();  
            conn.commit();  
            long endTime = new Date().getTime();  
            System.out.println("tc2执行时长：" + (endTime - startTime));  
        } catch (Exception e) {  
            try {  
                conn.rollback();  
            } catch (SQLException ex) {  
                ex.printStackTrace();  
            }  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(null, pstmt, conn);  
        }
```

### 连接池与JDBC 进阶使用
#### 阿里巴巴Druid连接池
- Druid连接池是阿里巴巴开源连接池组件，是最好的连接池之一
- Deuid对数据库连接进行有效管理与重用，最大化程序的执行效率
- 连接池负责创建连接，程序只负责取用和归还
![[resources/Pasted image 20220124004721.png]]

使用：
1. 下载Druid的jar包并放入依赖库中加载依赖
2. 在项目的src目录下创建druid-config.properties文件
```xml
driverClassName=com.mysql.cj.jdbc.Driver  
url=jdbc:mysql://localhost:3306/imooc?useSSL=false&useUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai&allowRetriveral=true  
username=root  
password=Ms.990218
```
3. 编写程序
```java
package com.imooc.jdbc.sample;  
  
import com.alibaba.druid.pool.DruidDataSourceFactory;  
import com.imooc.jdbc.hrapp.common.DbUtils;  
  
import javax.sql.DataSource;  
import java.io.FileInputStream;  
import java.io.UnsupportedEncodingException;  
import java.net.URLDecoder;  
import java.sql.Connection;  
import java.sql.PreparedStatement;  
import java.sql.ResultSet;  
import java.util.Properties;  
  
public class DruidSample {  
    public static void main(String[] args) {  
        // 1. 加载属性文件  
 Properties properties = new Properties();  
        String propertiesFile = DruidSample.class.getResource("/druid-config.properties").getPath();  
  
        // 容错: 将路径中的中文和空格编码,防止出错  
 try {  
            propertiesFile = new URLDecoder().decode(propertiesFile, "UTF-8");  
            properties.load(new FileInputStream(propertiesFile));  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
  
  
        Connection conn = null;  
        PreparedStatement pstmt = null;  
        ResultSet rs = null;  
        try {  
            // 2. 获取DateSource数据源对象  
 DataSource dataSource =  DruidDataSourceFactory.createDataSource(properties);  
            // 3. 获取数据库连接  
 conn = dataSource.getConnection();  
            pstmt = conn.prepareStatement("select * from employee limit 0,10");  
            rs = pstmt.executeQuery();  
            while(rs.next()) {  
                System.out.println("eno: " + rs.getInt("eno"));  
                System.out.println("ename: " + rs.getString("ename"));  
                System.out.println("salary: " + rs.getFloat("salary"));  
                System.out.println("dname: " + rs.getString("dname"));  
                System.out.println("hiredate: " + rs.getDate("hiredate"));  
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }finally {  
            DbUtils.closeConnection(rs, pstmt, conn);  
        }  
  
    }  
}
```

##### Druid连接池线程数量
在druid-config.properties文件中
```xml
initialSize=10
maxActive=20
```
当程序开始运行时会创建initialSize个线程，当线程不够用时创建新线程，总线程数量不超过20个，当所有线程都被占用时，如果有程序需要使用线程，需要等待线程池内有线程被释放才能继续运行，可能会造成程序卡死。
**技巧**： 将初始化线程和最大线程数量都设置成一个数，可以防止新创建线程让用户等待，对资源管理也有好处。

#### c3p0连接池
1. 添加c3p0-0.9.5.5.jar和mchange-commons-java-0.2.19.jar包
2. 新建c3p0-config.xml配置文件
```xml
<?xml version="1.0" encoding="utf-8" ?>  
<c3p0-config>  
    <default-config>  
        <property name="driverClass">com.mysql.cj.jdbc.Driver</property>  
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/imooc?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=Asia/Shanghai&amp;allowRetriveral=true</property>  
        <property name="user">root</property>  
        <property name="password">Ms.990218</property>  
<!-- 连接池初始连接数量-->  
 <property name="initialPoolSize">10</property>  
<!-- 连接池最大连接数量-->  
 <property name="maxPoolSize">20</property>  
    </default-config>  
</c3p0-config>
```
需要注意的是在c3p0的jdbcUrl中&需要更改为&amp;
3. 编写代码
```java
package com.imooc.jdbc.sample;  
  
import com.imooc.jdbc.hrapp.common.DbUtils;  
import com.mchange.v2.c3p0.ComboPooledDataSource;  
  
import javax.sql.DataSource;  
import java.sql.Connection;  
import java.sql.PreparedStatement;  
import java.sql.ResultSet;  
import java.sql.SQLException;  
  
public class C3P0Sample {  
    public static void main(String[] args) {  
        // 1. 加载配置文件  
 // 2，创建DataSource  
 DataSource dataSource = new ComboPooledDataSource();  
        // 3. 得到数据库连接  
 Connection conn = null;  
        PreparedStatement pstmt = null;  
        ResultSet rs = null;  
        try {  
            conn = dataSource.getConnection();  
            pstmt = conn.prepareStatement("select * from employee limit 0,10");  
            rs = pstmt.executeQuery();  
            while(rs.next()){  
                System.out.println("eno: " + rs.getInt("eno"));  
                System.out.println("ename: " + rs.getString("ename"));  
                System.out.println("salary: " + rs.getFloat("salary"));  
                System.out.println("dname: " + rs.getString("dname"));  
                System.out.println("hiredate: " + rs.getDate("hiredate"));  
            }  
        } catch (SQLException e) {  
            e.printStackTrace();  
        } finally {  
            DbUtils.closeConnection(rs, pstmt, conn);  
        }  
  
  
    }  
}
```
需要注意的是：由于我们必须将c3p0配置文件命名为c3p0-config.xml，所以第一步：加载配置文件和第二部：创建数据库连接只需要一条语句就可以完成，也就是
```java
DataSource dataSource = new ComboPooledDataSource();
```

#### Apache Commons DBUtils
![[resources/Pasted image 20220307173927.png]]
1. 添加commons-dbutils-1.7.jar包
2. 编写java代码
```java
package com.imooc.jdbc.sample;  
/*  
* Apache DBUtils + Druid联合使用演示  
* */  
  
  
import com.alibaba.druid.pool.DruidDataSourceFactory;  
import com.imooc.jdbc.hrapp.entity.Employee;  
import com.mchange.v2.c3p0.ComboPooledDataSource;  
import org.apache.commons.dbutils.QueryRunner;  
import org.apache.commons.dbutils.handlers.BeanHandler;  
import org.apache.commons.dbutils.handlers.BeanListHandler;  
  
import javax.sql.DataSource;  
import java.io.FileInputStream;  
import java.io.UnsupportedEncodingException;  
import java.net.URL;  
import java.net.URLDecoder;  
import java.sql.Connection;  
import java.sql.SQLException;  
import java.util.List;  
import java.util.Properties;  
  
public class DBUtilsSample {  
    private static void query() {  
        Properties properties = new Properties();  
        String propertyFile = DBUtilsSample.class.getResource("/druid-config.properties").getPath();  
        try {  
            propertyFile = new URLDecoder().decode(propertyFile, "UTF-8");  
            properties.load(new FileInputStream(propertyFile));  
            DataSource dataSource = DruidDataSourceFactory.createDataSource(properties);  
            QueryRunner qr = new QueryRunner(dataSource);  
            List<Employee> employees =  qr.query("select * from employee limit ?,10",  
                    new BeanListHandler<>(Employee.class),  
                    new Object[]{10});  
            // 第一个参数是查询语句  
 // 第二个参数是将结果集包装成的对象  
 // 第三个数组是参数，也就是查询语句中的？  
 for (Employee employee : employees) {  
                System.out.println(employee.getEname());  
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
    private static void update() {  
        Properties properties = new Properties();  
        String propertyFile = DBUtilsSample.class.getResource("/druid-config.properties").getPath();  
        Connection conn = null;  
        try {  
            // 对路径进行编码，防止路径中有空格等情况时出错  
 propertyFile = new URLDecoder().decode(propertyFile, "UTF-8");  
            properties.load(new FileInputStream(propertyFile));  
            DataSource dataSource = DruidDataSourceFactory.createDataSource(properties);  
            // 获取数据库连接  
 conn = dataSource.getConnection();  
            // 关闭自动提交事务  
 conn.setAutoCommit(false);  
            String sql1 = "update employee set salary = salary+1000 where eno = ?";  
            String sql2 = "update employee set salary = salary+1000 where eno = ?";  
            QueryRunner qr = new QueryRunner();  
            qr.update(sql1, new Object[]{1000});  
            qr.update(sql1, new Object[]{1001});  
            conn.commit();  
        } catch (Exception e) {  
            e.printStackTrace();  
            try {  
                if (conn != null && !conn.isClosed()){  
                    conn.rollback();  
                }  
            } catch (SQLException ex) {  
                ex.printStackTrace();  
            } finally {  
                try {  
                    if (conn != null && !conn.isClosed()) {  
                        conn.close();  
                    }  
                } catch (SQLException ex) {  
                    ex.printStackTrace();  
                }  
            }  
        }  
    }  
    public static void main(String[] args) {  
        query();  
    }  
}
```
在DBUtils查询操作中，由于并没有创建连接，所以不需要我们自己创建和关闭连接，当使用语句时DBUtils自动给我们创建连接，当操作完成时自动关闭连接，我们只需要进行后续的操作而不需要关注连接。

# Maven
## Maven介绍
![[resources/Pasted image 20220308110147.png]]
![[resources/Pasted image 20220308110645.png]]

## 配置
1. 配置好JAVA环境变量
2. 下载maven
3. 将 maven解压目录/bin 加入PATH环境变量中
4. 在cmd中输入mvn -v后，有版本文件输出就可以了

## 创建第一个maven项目
1. eclipse中已经集成了maven，但是我们最好自己在preferences中选择自己下载的最新的maven
2. 在new->other->maven project中创建
3. 创建新的maven项目时的maven坐标
### maven坐标
![[resources/Pasted image 20220308153515.png]]
### maven项目标准结构
![[resources/Pasted image 20220308153729.png]]

## Maven依赖管理
![[resources/Pasted image 20220308153908.png]]
可在search.maven.org中查找依赖
Maven存在的作用是方便的管理依赖，安装一个依赖可以使这个依赖的底层依赖全部被安装
## 本地仓库和中央仓库
![[resources/Pasted image 20220308164034.png]]
## Maven镜像仓库
1. 在maven.aliyun.com中找到public的路径
2. 在 pom.xml 中加入
```xml
  <repositories>
  	<!-- 阿里云私服地址 -->
  	<repository>
  		<id>aliyun</id>
  		<name>aliyun</name>
  		<url>https://maven.aliyun.com/repository/public</url>
  	</repository>
  </repositories>
  <dependencies>
```
在保存之后，当maven要下载依赖文件时会优先从阿里云的镜像服务器中下载。


## 项目打包
![[resources/Pasted image 20220308164817.png]]
1. 在pom.xml文件中加入
```xml
  <build>
  	<plugins>
  		<plugin>
  			<groupId>org.maven.plugins</groupId>
  			<artifactId>maven-assembly-plugin</artifactId>
  			<version>2.5.5</version>
  			<!-- 配置信息 -->
  			<configuration>
  				<archive>
  					<manifest>
  						<mainClass>com.imooc.maven.PinyinTestor</mainClass>
  					</manifest>
  				</archive>
  				<!-- 打包过程中使用到的额外参数 -->
  				<descriptorRefs>
  					<!-- 在打包时会将所有的jar合并到输出的jar文件中 -->
  					<descriptorRef>jar-with-dependiences</descriptorRef>
  				</descriptorRefs>
  			</configuration>  			
  		</plugin>
  	</plugins>
  </build>

```
2. 在eclipse中run->run configurations->maven build->new configuration
![[resources/Pasted image 20220308170521.png]]
3. 运行后将会把当前项目输出到target中

## maven构建一个web工程
1. 在JRE System Library中将jre修改为jre1.8
2. 在preferences中java compiler中将compile level修改为1.8
3. 由于初始没有网页文件夹，在main中新建一个webapp文件夹
4. properties 的Project Facets中开启Dynamic Web Module, 选择版本为3.1，将运行环境设置为你自己新建的tomcat环境，在左下角Further configuration available中将Content directory 改为 /src/main/webapp, 并勾选下方Generate web.xml, 点击apply and close
5. 测试：在webapp目录下新建一个index.jsp文件，并输入一些内容
6. 将maven项目添加到tomcat中
7. 浏览器访问localhost:8080/maven/index.jsp，出现你输入的内容说明成功了
8. 在search.maven.org中搜索jstl选择javax-servlet包下的jstl，并将其添加到maven依赖中
9. 测试依赖是否添加成功
	1. 在index.jsp中加入
	```java
	<%@ taglib uri = "http://java.sun.com/jsp/jstl/fmt" prefix = "fmt" %>
		
	<fmt:formatNumber value = "123456789.54321" pattern = "0,000.00"></fmt:formatNumber>
		
	```
	2. 重启tomcat并查看修改结果
	3. 重启后会出现ClassNotFoundException，此时需要在maven项目中右键，选择Properties-->Deployment Assembly-->add-->Java build path entries，然后点击next，选择maven dependency。这样maven的jar包就发布到tomcat的lib目录下，就不会提示找不到ClassNotFoundException了。
	4. 在pom.xml中加入
	```xml
	<!-- packaging 表示输出的格式 -->
  	<packaging>war</packaging>
  	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>3.2.2</version>
			</plugin>
		</plugins>
	</build>
	```
	5. 在run configuration中加入build-war，base directory选择web项目，Goals中写package, 然后apply and run
	6. 将打包的war包放到tomcat安装目录的webapps中，然后关闭eclipse中的tomcat，打开tomcat中的startup.bat，此时webapps中会出现打包的web项目，然后访问localhost:8080/文件夹路径/index.jsp
	7. 如需自定义输出war包名字，在pom.xml的build中加入，再次编译后就可以自定义的名字访问了
	```xml
		<finalName>maven-web</finalName>
	```
	## Maven常用命令
	![[resources/Pasted image 20220309095247.png]]
	## 工厂模式
	![[resources/Pasted image 20220309102015.png]]
	![[resources/Pasted image 20220309102025.png]]
	![[resources/Pasted image 20220309102137.png]]
	![[resources/Pasted image 20220309102305.png]]
	
	# MyBatis
	![[resources/Pasted image 20220309133827.png]]
	![[resources/Pasted image 20220309133843.png]]