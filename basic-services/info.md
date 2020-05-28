<![endif]-->

CREATE TABLE `sale_plan` (

`id` int(2) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键id',

`title` varchar(30) NOT NULL DEFAULT '' COMMENT '页面标题',

`content` text NOT NULL COMMENT '推广内容',

`linkUrl` varchar(60) NOT NULL DEFAULT '' COMMENT '推广链接地址',

`isOpen` tinyint(1) NOT NULL DEFAULT '0' COMMENT '是否开启销售员推广计划',

`createdUser` int(10) NOT NULL DEFAULT '0' COMMENT '创建人',

`createdTime` int(11) NOT NULL DEFAULT '0' COMMENT '创建时间',

`updatedTime` int(11) NOT NULL DEFAULT '0' COMMENT '更新时间',

PRIMARY KEY (`id`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT '销售员推广计划表'

　用如下语法：

alter table table_name rename table_new_name;

修改表的字符集：

当前数据库的编码集：  show variables like 'character%';

与服务器端相关：database、server、system（永远无法修改，就是utf-8）

与客户端相关：connection、client、results

client

为客户端使用的字符集。

connection

为连接数据库的字符集设置类型，如果程序没有指明连接数据库使用的字符集类型则按照服务器端默认的字符集设置。

database

为数据库服务器中某个库使用的字符集设定，如果建库时没有指明，将使用服务器安装时指定的字符集设置。

results

为数据库给客户端返回时使用的字符集设定，如果没有指明，使用服务器默认的字符集。

server

为服务器安装时指定的默认字符集设定。

system

为数据库系统使用的字符集设定。

远程访问

Mysql8

<![if !supportLists]>1. <![endif]># 特定用户的host 修改

<![if !supportLists]>2. <![endif]>mysql > update user set host='%'  where user='root';

<![if !supportLists]>3. <![endif]># 指定用户的授权

<![if !supportLists]>4. <![endif]>mysql > grant all privileges on test.* to root@'%'

# mysql逻辑架构图

# 索引

## 索引是什么？

索引是帮助MySQL高效获取数据的数据结构。

## 优缺点

**优点：**

<![if !supportLists]>· <![endif]>减少查询需要扫描的数据量(加快了查询速度)

<![if !supportLists]>· <![endif]>减少服务器的排序操作和创建临时表的操作(加快了groupby和orderby等操作)

<![if !supportLists]>· <![endif]>将服务器的随机IO变为顺序IO(加快查询速度).

**缺点：**

首先索引也是数据,也需要存储,因此会带来额外的存储空间占用.

其次,在插入,更新和删除操作的同时,需要维护索引,因此会带来额外的时间开销.

## 索引分类

**从存储结构上来划分：****BTree****索引（****B-Tree****或****B+Tree****索引），****Hash****索引，****full-index****全文索引，****R-Tree****索引。**

从应用层次来分：

主键索引：设定为主键后数据库会自动建立索引，innodb为聚簇索引

单值索引：即一个索引只包含单个列，一个表可以有多个单列索引

唯一索引：索引列的值必须唯一，但允许有空值

复合索引：即一个索引包含多个列，在数据库操作期间，复合索引比单值索引所需要的开销更小(对于相同的多个列建索引)，当表的行数远大于索引列的数目时可以使用复合索引

**主键索引语法：**

#随表一起建索引：

**CREATE**  **TABLE** customer **(**id **INT****(**10**)** UNSIGNED  AUTO_INCREMENT **,**customer_no **VARCHAR****(**200**),**customer_name **VARCHAR****(**200**),**

**PRIMARY**  **KEY****(**id**)**

**);**

#使**用**AUTO_INCREMENT关**键**字的列必**须**有索引**(**只要有索引就行**)**。

**CREATE**  **TABLE** customer2 **(**id **INT****(**10**)** UNSIGNED**,**customer_no **VARCHAR****(**200**),**customer_name **VARCHAR****(**200**),**

**PRIMARY**  **KEY****(**id**)**

**);**

#单独建**主键**索引：

**ALTER**  **TABLE** customer **add**  **PRIMARY**  **KEY** customer**(**customer_no**);**

#删除建**主键**索引：

**ALTER**  **TABLE** customer **drop**  **PRIMARY**  **KEY**  **;**

#修改建**主键**索引：

#必**须**先删除掉**(****drop****)**原索引，再新建**(****add****)**索引

**单值索引语法：**

#随表一起建索引：

**CREATE**  **TABLE** customer **(**id **INT****(**10**)** UNSIGNED  AUTO_INCREMENT **,**customer_no **VARCHAR****(**200**),**customer_name **VARCHAR****(**200**),**

**PRIMARY**  **KEY****(**id**),**

**KEY**  **(**customer_name**)**

**);**

#随表一起建立的索引  索引名同  列名**(**customer_name**)**

#单独建单**值**索引：

**CREATE**  **INDEX** idx_customer_name **ON** customer**(**customer_name**);**

#删除索引：

**DROP**  **INDEX** idx_customer_name **;**

**唯一索引语法：**

#随表一起建索引：

**CREATE**  **TABLE** customer **(**id **INT****(**10**)** UNSIGNED  AUTO_INCREMENT **,**customer_no **VARCHAR****(**200**),**customer_name **VARCHAR****(**200**),**

**PRIMARY**  **KEY****(**id**),**

**KEY**  **(**customer_name**),**

**UNIQUE**  **(**customer_name**),**

**KEY**  **(**customer_no**,**customer_name**)**

**);**

#单独建索引：

**CREATE**  **INDEX** idx_no_name **ON** customer**(**customer_no**,**customer_name**);**

#删除索引：

**DROP**  **INDEX** idx_no_name **on** customer **;**

**复合索引语法：**

#随表一起建索引：

**CREATE**  **TABLE** customer **(**id **INT****(**10**)** UNSIGNED  AUTO_INCREMENT **,**customer_no **VARCHAR****(**200**),**customer_name **VARCHAR****(**200**),**

**PRIMARY**  **KEY****(**id**),**

**KEY**  **(**customer_name**),**

**UNIQUE**  **(**customer_name**),**

**KEY**  **(**customer_no**,**customer_name**)**

**);**

#单独建索引：

**CREATE**  **INDEX** idx_no_name **ON** customer**(**customer_no**,**customer_name**);**

#删除索引：

**DROP**  **INDEX** idx_no_name **on** customer **;**

根据中数据的物理顺序与键值的逻辑（索引）顺序关系：聚集索引，非聚集索引。

# 数据库服务器性能影响因素

## <![if !supportLists]>1. <![endif]>服务器硬件

### cpu和内存

**cpu****选择：**

选多核：不支持多cpu对同一个sql并发处理（只能用一个cpu处理）

mysql版本：最新版支持多核cpu

32位64位cpu：64位cpu

**内存选择：**

MyISAM: 内存缓存索引，操作系统缓存数据

Innodb：索引和数据，都缓存在内存

添加内存；

写入操作进入延缓

比如浏览量的计数（多次io操作变成一次）

### 磁盘IO

**磁盘选择：**

传统机械硬盘：使用RAID添加传统机器硬盘的性能

SSD（固态存储）：优点：更好的随机读写性能；更好的支持并发；缺点：更容易损坏

Fasion io卡（PCI-E）

固态存储使用场景：

<![if !supportLists]>1） <![endif]>适用于存在大量随机I/O的场景

<![if !supportLists]>2） <![endif]>适用于解决单线程负载的I/O瓶颈

### 网卡流量

建议：

<![if !supportLists]>1） <![endif]>采用高性能和高带宽的网络接口设备和交换机

<![if !supportLists]>2） <![endif]>对多个网卡进行绑定，增强可用性和带宽

<![if !supportLists]>3） <![endif]>尽可能的进行网络隔离

## <![if !supportLists]>2. <![endif]>服务器系统

可参考：Linux性能优化

## <![if !supportLists]>3. <![endif]>数据库存储引擎选择

Mysql体系结构：

### MyISAM

<![if !supportLists]>1） <![endif]>mysql5.5之前版本默认存储引擎

<![if !supportLists]>2） <![endif]>myisam存储引擎表有MYD和MYI组成；.mfr: 表结果

#### 特性

<![if !supportLists]>1） <![endif]>并发性和锁级别（表级锁）

<![if !supportLists]>2） <![endif]>表损坏修复：repair table +表名；命令行工具也可以（必须停止mysql服务）

<![if !supportLists]>3） <![endif]>MyISAM支持全文索引（5.7之前）

<![if !supportLists]>4） <![endif]>MyISAM表支持数据压缩：

**限制**

<![if !supportLists]>1） <![endif]>版本<mysql5.0默认表大小为4G，版本mysql>5.0默认表大小256TB

#### 使用场景

<![if !supportLists]>1） <![endif]>非事物型应用

<![if !supportLists]>2） <![endif]>只读类应用

<![if !supportLists]>3） <![endif]>空间类应用

### Innodb

MySQL5.5.5之后，版本默认存储引擎为Innodb

1）

系统表空间和独立表空间

给innodb添加表级锁

Lock table +表名 write

解锁：unlock tables；

#### 特性

#### Redo Log

**工作原理：**

**InnoDB****是一个事务性的存储引擎，而InnoDB的事务实现是基于事务日志redo log和undo log实现的。**

**redo log****是重做日志，提供再写入操作，实现事务的持久性；undo log是回滚日志，提供回滚操作，保证事务的一致性。**

redo log又包括了内存中的日志缓冲（redo log buffer）以及保存在磁盘的重做日志文件（redo log file），前者存储在内存中，容易丢失，后者持久化在磁盘中，不会丢失。

InnoDB的更新操作采用的是Write Ahead Log策略，即先写日志，再写入磁盘。当一条记录更新时，InnoDB会先把记录写入到redo log buffer中，并更新内存数据。可以通过参数innodb_flush_log_at_trx_commit自定义commit时，如何将redo log buffer中的日志刷新到redo log file中。

在这里，需要注意的是InnoDB的redo log的大小是固定的，分别有多个日志文件采用循环方式组成一个循环闭环，当写到结尾时，会回到开头循环写日志。可以通过参数innodb_log_files_in_group和innodb_log_file_size配置日志文件数量和每个日志文件的大小。

**Buffer Pool****中更新的数据未刷新到磁盘中，该内存页称之为脏页。**最终脏页的数据会刷新到磁盘中，将磁盘中的数据覆盖，这个过程与redo log不一定有关系。

只有当redo log日志满了的情况下，才会主动触发脏页刷新到磁盘，而脏页不仅只有redo log日志满了的情况才会刷新到磁盘，以下几种情况同样会触发脏页的刷新：

<![if !supportLists]>· <![endif]>系统内存不足时，需要将一部分数据页淘汰掉，如果淘汰的是脏页，需要先将脏页同步到磁盘；

<![if !supportLists]>· <![endif]>MySQL认为空闲的时间，这种情况没有性能问题；

<![if !supportLists]>· <![endif]>MySQL正常关闭之前，会把所有的脏页刷入到磁盘，这种情况也没有性能问题。

在生产环境中，如果开启了慢SQL监控，会发现偶尔会出现一些用时稍长的SQL。这是因为脏页在刷新到磁盘时可能会给数据库带来性能开销，导致数据库操作抖动。

**crash-safe:**

可以保证即使数据库发生异常重启，之前提交的记录都不会丢失，这个能力称为**crash-safe**

#### Binlog

Redo log和binlog的区别：

1.  redo log是InnoDB引擎特有的；binlog是MySQL的Server层实现的，所有引擎都可以使用。
2.  redo log是物理日志，记录的是“在某个数据页上做了什么修改”；binlog是逻辑日志，记录的是这个语句的原始逻辑，比如“给ID=2这一行的c字段加1 ”。
3.  redo log是循环写的，空间固定会用完；binlog是可以追加写入的。“追加写”是指binlog文件写到一定大小后会切换到下一个，并不会覆盖以前的日志。

## <![if !supportLists]>4. <![endif]>数据库参数配置

**参数配置路径：**

**参数配置：**

### 内存配置相关参数

innodb_flush_log_at_trx_commit =1;

表示每次事务的redo log都直接持久化到磁盘，这样可以保证MySQL异常重启之后数据不丢失。

sync_binlog = 1；

表示每次事务的binlog都持久化到磁盘，这样可以保证MySQL异常重启之后binlog不丢失。

### IO相关配置参数

### 安全相关配置

### 其它参数

## <![if !supportLists]>5. <![endif]>数据库结构设计和SQL语句

### sql查询速度

通过分析慢查询解决

### 大表

大表：记录超过1000行，数据量超过10G

1）慢查询：很难在一定的时间内过滤出所需要的数据

<![if !supportLists]>2） <![endif]>建立索引需要很长时间

<![if !supportLists]>3） <![endif]>修改表结构需要长时间锁表

如何处理数据库中的大表

<![if !supportLists]>1） <![endif]>大表的数据修改最好分批处理

比如：1000万行记录的表中删除/更新100万行记录一次只删除/更新5000行记录，然后暂停几秒，再继续

<![if !supportLists]>2） <![endif]>大表结构修改

两种方法：

<![if !supportLists]>1. <![endif]>先改变从数据库，然后进行主从切换，再去主服务器修改

<![if !supportLists]>2. <![endif]>现在主服务器上，建立新表，

使用工具：pt-online-schema-change

### //TODO pt-online-schema-change 演示

分库分表：分表主键的选择，分表后跨分区数据的查询和统计

大表历史数据归档：减少对前后端业务的影响

### 大事物

定义：运行时间比较长，操作的数据比较多的事物

风险：

<![if !supportLists]>3） <![endif]>锁定太多的数据，造成大量的阻塞和锁超时

<![if !supportLists]>4） <![endif]>回滚时所需时间比较长

<![if !supportLists]>5） <![endif]>执行时间长，容易造成主从延时

解决：

<![if !supportLists]>1） <![endif]>避免一次处理太多数据

<![if !supportLists]>2） <![endif]>移除不必要在事物中的select操作

### 索引

### SQL

#### 获取有性能问题的sql

1）通过用户反馈获取存在性能问题的SQL（比较被动）

2）通过慢查日志获取存在性能问题的SQL

3）实时获取存在性能问题的SQL

#### 慢查询

##### 主要开销

1）磁盘IO：顺序写入的，对大部分情况来说可以忽略不计

2）磁盘空间：主要要考虑存储日志所需要的大量的磁盘空间

##### 参数设置

**slow_query_log**  启动/停止记录慢查日志（ON开启）

**slow_query_log_file**  制定慢查日志的存储路径及文件

（默认情况下保存在MySQL的数据目录中）

**long_query_time**  制定记录慢查日志SQL执行时间的伐值

默认值为10秒，最低到微秒，如果是100微秒 则要表达为 0.0001

一般设置为0.001秒 ，一毫秒比较合适

**log_queries_not_using_indexes**  是否记录未使用索引的SQL

### 慢查询分析工具

Mysqldumpslow

Pt-query-digest

查询计划各阶段消耗时间

Mysql profile

使用performance_schema

SQL优化的一些方案

<![if !supportLists]>1） <![endif]>not in改为left json

<![if !supportLists]>2） <![endif]>汇总统计数据查询慢，可以改为将数据统计出来，放在一张表中

## 6. 性能优化命令

### show processlist

**show processlist****命令的输出结果显示了有哪些线程在运行**

**showprocesslist**如果不使用该FULL关键字，则只显示每个语句的前100个字符在Info字段中。

**还有一种查看方式：**

查询 mysql 占用的链接

netstat -naplt|grep 3306  
统计数量  
netstat -naplt|grep 3306|wc –l

或者

show global status like 'max_used_connections';

**show processlist** **详细说明**

①.id列，用户登录mysql时，系统分配的"connection_id"，可以使用函数connection_id()查看

②.user列，显示当前用户。如果不是root，这个命令就只显示用户权限范围的sql语句

③.host列，显示这个语句是从哪个ip的哪个端口上发的，可以用来跟踪出现问题语句的用户

④.db列，显示这个进程目前连接的是哪个数据库

⑤.command列，显示当前连接的执行的命令，一般取值为休眠（sleep），查询（query），连接（connect）等

⑥.time列，显示这个状态持续的时间，单位是秒

⑦.state列，显示使用当前连接的sql语句的状态，很重要的列。state描述的是语句执行中的某一个状态。一个sql语句，以查询为例，可能需要经过copying to tmp table、sorting result、sending data等状态才可以完成

⑧.info列，显示这个sql语句，是判断问题语句的一个重要依据

**Command**

**Binlog Dump**: 主节点正在将二进制日志  ，同步到从节点

**Binlog Dump****：**这是主服务器上的线程，用于将二进制日志内容发送到从服务器。

**Table Dump****：**线程将表内容发送到从服务器。

**Change user****：**线程正在执行改变用户操作。

**Close stmt****：**线程正在关闭准备好的语句。

**Connect****：**复制中，从服务器连接到其主服务器。

**Connect Out****：**复制中，从服务器正在连接到其主服务器。

**Create DB****：**线程正在执行create-database操作。

**Daemon****：**此线程在服务器内部，而不是服务客户端连接的线程。

**Debug****：**线程正在生成调试信息。

**Delayed insert****：**线程是一个延迟插入处理程序。

**Drop DB****：**线程正在执行drop-database操作。

**Execute****：**线程正在执行一个准备好的语句（prepare statement类型就是预编译的语句，JDBC支持次类型执行SQL）。

**Fetch****：**线程正在执行一个准备语句的结果。

**Field List****：**线程正在检索表列的信息。

**Init DB****：**线程正在选择默认数据库。

**Kill****：**线程正在杀死另一个线程。

**Long Data****：**该线程在执行一个准备语句的结果中检索长数据。

**Ping****：**线程正在处理服务器ping请求。

**Prepare****：**线程正在为语句生成执行计划。

**Processlist****：**线程正在生成有关服务器线程的信息。

**Query****：**该线程正在执行一个语句。

**Quit****：**线程正在终止。

**Refresh****：**线程是刷新表，日志或缓存，或重置状态变量或复制服务器信息。

**Register Slave****：**线程正在注册从服务器。

**Reset stmt****：**线程正在重置一个准备好的语句。

**Set option****：**线程正在设置或重置客户端语句执行选项。

**Shutdown****：**线程正在关闭服务器。

**Sleep****：**线程正在等待客户端向其发送新的语句。

**Statistics****：**线程正在生成服务器状态信息。

**Time****：**没用过。

**State**

Finished reading one binlog; switching to next binlog 线程已经读完二进制日志文件并打开下一个发送给从属的文件。

<![if !supportLists]>· <![endif]>**一般线程状态（****State****）值**

以下列表描述State 了与常规查询处理关联的线程值，而不是更复杂的活动，例如复制。其中许多仅用于在服务器中查找错误。

After create：当线程创建表（包括内部临时表）时，会在创建表的函数的末尾创建。即使由于某些错误而无法创建表，也会使用此状态。

Analyzing：线程正在计算MyISAM表密钥分布（例如:for ANALYZE TABLE）。

checking permissions：线程正在检查服务器是否具有执行语句所需的权限。

Checking table：线程正在执行表检查操作。

cleaning up：线程已经处理了一个命令，正在准备释放内存并重置某些状态变量。

closing tables：线程将更改的表数据刷新到磁盘并关闭已用表。这应该是一个快速的操作。如果没有，请验证您是否没有完整的磁盘，并且磁盘没有被非常大的使用。

copy to tmp table：线程正在处理ALTER TABLE语句。此状态发生在已创建新结构的表之后，但是将行复制到该表之前。对于此状态的线程，可以使用性能模式来获取有关复制操作的进度。

Copying to group table：如果语句具有不同ORDER BY和GROUP BY标准，各行按组排列和复制到一个临时表。

Creating index：线程正在处理ALTER TABLE … ENABLE KEYS一个MyISAM表。

Creating sort index：线程正在处理一个SELECT使用内部临时表解析的线程  。

creating table：线程正在创建一个表，这包括创建临时表。

committing alter table to storage engine：服务器已经完成就位ALTER TABLE并提交结果。

deleting from main table：服务器正在执行多表删除的第一部分，它仅从第一个表中删除，并从其他（引用）表中保存要用于删除的列和偏移量。

deleting from reference tables：服务器正在执行多表删除的第二部分，并从其他表中删除匹配的行。

discard_or_import_tablespace：线程正在处理ALTER TABLE … DISCARD TABLESPACE或ALTER TABLE … IMPORT TABLESPACE声明。

end：这发生在结束，但的清理之前ALTER TABLE， CREATE VIEW， DELETE， INSERT， SELECT，或UPDATE语句。

executing：该线程已经开始执行一个语句。

Execution of init_command：线程正在init_command系统变量的值中执行语句  。

freeing items：线程已经执行了一个命令，在这种状态下完成的项目的一些释放涉及查询缓存，这个状态通常在后面cleaning up。

FULLTEXT initialization：服务器正在准备执行自然语言全文搜索。

init：此操作在初始化ALTER TABLE, DELETE, INSERT, SELECT, or UPDATE之前发生，服务器在该状态中采取的操作包括刷新二进制日志、Innodb日志和一些查询缓存清理操作。对于最终状态, 可能会发生以下操作：更改表中的数据后删除查询缓存项、将事件写入二进制日志、释放内存缓冲区, 包括blob。

Killed：执行KILL语句，向线程发送了一个声明，下次检查kill标志时应该中断。在MySQL的每个主循环中检查该标志，但在某些情况下，线程可能需要很短时间才能死掉。如果线程被某个其他线程锁定，则一旦其他线程释放锁定，该kill就会生效。

Locking system tables：线程正在尝试锁定系统表（例如，时区或日志表）。

login：连接线程的初始状态，直到客户端成功认证为止。

manage keys：服务器启用或禁用表索引。

NULL：该状态用于SHOW PROCESSLIST状态。

Opening system tables：线程尝试打开系统表（例如，时区或日志表）。

Opening tables：线程正在尝试打开一个表，这应该是非常快的程序，除非有事情阻止打开。例如，一个ALTER TABLE或一个LOCK TABLE语句可以阻止打开一个表，直到语句完成。还可能需要关注table_open_cache参数的值是否足够大。对于系统表，使用Opening system tables状态。

optimizing：服务器正在执行查询的初始优化。

preparing：此状态发生在查询优化期间。

Purging old relay logs：线程正在删除不需要的中继日志文件。

query end：处理查询之后，freeing items状态之前会发生这种状态。

Removing duplicates：该查询的使用SELECT DISTINCT方式使得MySQL不能在早期阶段优化不同的操作。因此，MySQL需要一个额外的阶段来删除所有重复的行，然后将结果发送给客户端。

removing tmp table：处理语句后，该线程正在删除一个内部临时表SELECT 。如果没有创建临时表，则不使用该状态。

rename：线程正在重命名一个表。

rename result table：线程正在处理一个ALTER TABLE语句，已经创建了新表，并重新命名它来替换原始表。

Reopen tables：线程获得了表的锁，但在获得基础表结构更改的锁之后注意到。它释放了锁，关闭了table，并试图重新打开它。

Repair by sorting：修复代码正在使用排序来创建索引。

preparing for alter table：服务器正在准备就地执行ALTER TABLE。

Repair done：线程已经完成了一个MyISAM表的多线程修复  。

Repair with keycache：修复代码通过密钥缓存逐个使用创建密钥，这比慢得多Repair by sorting。

Rolling back：线程正在回滚事务。

Saving state：对于MyISAM表操作（如修复或分析），线程将新的表状态保存到.MYI文件头。状态包括行数， AUTO_INCREMENT计数器和键分布等信息。

Searching rows for update：线程正在进行第一阶段，以便在更新之前查找所有匹配的行。如果UPDATE要更改用于查找涉及的行的索引，则必须执行此操作  。

setup：线程正在开始一个ALTER TABLE操作。

Sorting for group：线程正在做一个满足一个GROUP BY。

Sorting for order：线程正在做一个满足一个ORDER BY。

Sorting index：线程是排序索引页，以便在MyISAM表优化操作期间更有效地访问。

Sorting result：对于一个SELECT语句，这类似于Creating sort index，但是对于非临时表。

statistics：服务器正在计算统计信息以开发查询执行计划。如果一个线程长时间处于这种状态，服务器可能是磁盘绑定的，执行其他工作。

update：线程正在准备开始更新表。

Updating：线程正在搜索要更新的行并正在更新它们。

updating main table：服务器正在执行多表更新的第一部分，它仅更新第一个表，并保存用于更新其他（引用）表的列和偏移量。

updating reference tables：服务器正在执行多表更新的第二部分，并从其他表更新匹配的行。

User lock：线程将要求或正在等待通过GET_LOCK()呼叫请求的咨询锁定  。因为 SHOW PROFILE，这个状态意味着线程正在请求锁定（不等待它）。

User sleep：线程调用了一个 SLEEP()调用。

<![if !supportLists]>· <![endif]>**故障诊断状态（****State****）值（个人提取）**

logging slow query：线程正在向慢查询日志写入语句。

altering table：服务器正在执行就地ALTER TABLE。

Receiving from client：服务器正在从客户端读取数据包。

Copying to tmp table：服务器正在复制磁盘到内存的临时表，是直接在磁盘创建的临时表而并非从内存转到磁盘的临时表。

Copying to tmp table on disk：对于线程将临时表从内存中更改为基于磁盘的格式存储以节省内存后，又把临时表从磁盘复制到内存时的状态。

Creating tmp table：线程正在内存或磁盘上创建临时表。如果表在内存中创建，但后来转换为磁盘表，则该操作中的状态将为Copying to tmp table on disk。

Sending data：线程正在读取和处理SELECT语句的行，并将数据发送到客户端。由于在此状态期间发生的操作往往执行大量的磁盘访问（读取），所以在给定查询的整个生命周期内通常是最长的运行状态。

Sending to client：服务器正在向客户端写入数据包。

Waiting for commit lock：FLUSH TABLES WITH READ LOCK正在等待提交锁。

Waiting for global read lock：FLUSH TABLES WITH READ LOCK正在等待全局读锁定或read_only正在设置全局系统变量。

Waiting for tables：线程得到一个通知，表格的底层结构已经改变，需要重新打开表以获得新的结构。但是，要重新打开表格，必须等到所有其他线程都关闭该表。如果另一个线程已使用FLUSH TABLES或下面的语句之一：FLUSH TABLES tbl_name, ALTER TABLE, RENAME TABLE, REPAIR TABLE, ANALYZE TABLE, 或OPTIMIZE TABLE都会发生通知。

Waiting for table flush：线程正在执行FLUSH TABLES并正在等待所有线程关闭它们的表，或者线程得到一个通知，表中的底层结构已经改变，并且需要重新打开表以获得新的结构。但是，要重新打开表，必须等到所有其他线程都关闭该表。如果另一个线程已使用FLUSH TABLES或下面的语句之一：FLUSH TABLES tbl_name, ALTER TABLE, RENAME TABLE, REPAIR TABLE, ANALYZE TABLE, 或OPTIMIZE TABLE都会发出这个通知。

Waiting for lock_type lock：服务器正在等待THR_LOCK从元数据锁定子系统获取锁或锁，其中lock_type指示锁的类型。THR_LOCK状态表示：Waiting for table level lock；这些状态表示等待元数据锁定：Waiting for event metadata lock、Waiting for global read lock、Waiting for schema metadata lock、Waiting for stored function metadata lock、Waiting for stored procedure metadata lock、Waiting for table metadata lock、Waiting for trigger metadata lock。

Writing to net：服务器正在将数据包写入网络，如果一个线程长时间在执行并且一直处于Writing to net状态，那么一直在发送数据包到网络，可以试着调整max_allowed_packet大小。另外，这可能会导致其他线程大量阻塞。

Waiting on cond：线程等待条件成为true的一般状态，没有特定的状态信息可用。

System lock：线程已经调用mysql_lock_tables() ，且线程状态从未更新。这是一个非常普遍的状态，可能由于许多原因而发生。例如, 线程将请求或正在等待表的内部或外部系统锁。当InnoDB在执行锁表时等待表级锁时, 可能会发生这种情况。如果此状态是由于请求外部锁而导致的，并且不使用正在访问相同表的多个mysqld服务器MyISAM，则可以使用该–skip-external-locking选项禁用外部系统锁  。但是，默认情况下禁用外部锁定，因此这个选项很有可能不起作用。因为SHOW PROFILE，这个状态意味着线程正在请求锁定（不等待它）。对于系统表，使用Locking system tables状态。

<![if !supportLists]>· <![endif]>**查询缓存状态（****State****）值**

checking privileges on cached query：服务器正在检查用户是否具有访问缓存查询结果的权限。

checking query cache for query：服务器正在检查当前查询是否存在于查询缓存中。

invalidating query cache entries：查询缓存条目被标记为无效，因为底层表已更改。

sending cached result to client：服务器正在从查询缓存中获取查询的结果，并将其发送给客户端。

storing result in query cache：服务器将查询结果存储在查询缓存中。

Waiting for query cache lock：当会话正在等待采取查询缓存锁定时，会发生此状态。这种情况可能需要执行一些查询缓存操作，如使查询缓存无效的INSERT或DELETE语句，以及RESET QUERY CACHE等等。

<![if !supportLists]>· <![endif]>**事件调度器线程状态（****State****）值**

这些状态适用于事件调度程序线程，创建用于执行调度事件的线程或终止调度程序的线程。

Clearing

调度程序线程或正在执行事件的线程正在终止，即将结束。

Initialized

调度程序线程或将执行事件的线程已初始化。

Waiting for next activation

调度程序具有非空事件队列，但下一次激活是将来。

Waiting for scheduler to stop

线程发出SET GLOBAL event_scheduler=OFF并正在等待调度程序停止。

Waiting on empty queue

调度程序的事件队列是空的，它正在休眠。

  
mysql主从复制线程状态转变 参考：

[https://www.jb51.net/article/156311.htm](https://www.jb51.net/article/156311.htm)

**常用操作**

1、按客户端 IP 分组，看哪个客户端的链接数最多

**select**

client_ip**,**

**count****(** client_ip **)**  **as** client_num

**from**

**(**  **select**  **substring_index****(**  **host****,**  ':'**,**  1  **)**  **as** client_ip **from** information_schema**.**processlist **)**  **as** connect_info

**group**  **by**

client_ip

**order**  **by**

client_num **desc****;**

2、查看正在执行的线程，并按 Time 倒排序，看看有没有执行时间特别长的线程

**select**  *****  **from** information_schema**.**processlist **where** Command **!=**  'Sleep'  **order**  **by**  **Time**  **desc****;**

3、找出所有执行时间超过 5 分钟的线程，拼凑出 kill 语句，方便后面查杀  （此处 5分钟  可根据自己的需要调整SQL标红处）

**select**  **concat****(**'kill '**,** id**,**  ';'**),**Command **from** information_schema**.**processlist **where** Command **!=**  'Sleep'  **and**  **Time**  **>**  300  **order**  **by**  **Time**  **desc****;**

# 锁

**作用：**

<![if !supportLists]>1） <![endif]>锁的所用是管理共享资源的并发访问

<![if !supportLists]>2） <![endif]>锁用于实现事物的隔离性

**类型：**

共享锁（也称读锁）

独占锁（也称写锁）

**粒度：**

表级锁 lock table + 表名 write

行级锁

## **MyISAN****存储引擎**

MyISAM 存储引擎只支持表锁，**  
<![if !supportLineBreakNewLine]>  
<![endif]>**

查询表锁争用情况：

如果 Table_locks_waited 的值比较高，则说明存在着较严重的表级锁争用情况。

### MySQL的表级锁的两种模式

表共享读锁（Table Read Lock）

表独占写锁（Table Write Lock）

**MySQL****中的表锁兼容性：**

**请求锁模式  
矩阵结果表示是否兼容  
当前锁模式**

**None**

**读锁**

**写锁**

读锁

是

是

否

写锁

是

否

否

  
<![if !supportLineBreakNewLine]>  
<![endif]>

在MyISAM读模式下，不会阻塞其它用户的同一表读操作，但是会阻塞写操作；

在写模式下，会同时阻塞其它用户同一表的读写操作。

### **测试MyISAM的写锁模式**

新建一个user表，引擎是MyISAM：

可以看出，通过lock table user write将user表锁住后，其它用户进行对该表操作时，都会被阻塞。

### **测试MyISAM读锁**

在执行LOCK TABLES后，只能访问显式加锁的这些表，不能访问未加锁的表；

如果加的是读锁，那么只能执行查询操作，而不能执行更新操作。

### **MyISAM****支持并发插入**

MyISAM表的读和写是串行的，但这是就总体而言的。在一定条件下，MyISAM表也支持查询和插入操作的并发进行。MyISAM存储引擎有一个系统变量concurrent_insert，专门用以控制其并发插入的行为，其值分别可以为0、1或2。  
<![if !supportLineBreakNewLine]>  
<![endif]>

<![if !supportLists]>· <![endif]>当concurrent_insert设置为0时，不允许并发插入。

<![if !supportLists]>· <![endif]>当concurrent_insert设置为1时，如果MyISAM表中没有空洞（即表的中间没有被删除的行），MyISAM允许在一个进程读表的同时，另一个进程从表尾插入记录。这也是MySQL的默认设置。

<![if !supportLists]>· <![endif]>当concurrent_insert设置为2时，无论MyISAM表中有没有空洞，都允许在表尾并发插入记录。  
<![if !supportLineBreakNewLine]>  
<![endif]>

### **MyISAM****的锁调度**

MyISAM存储引擎的读锁和写锁是互斥的，读写操作是串行的。但它认为写锁的优先级比读锁高，所以即使读请求先到锁等待队列，写请求后到，写锁也会插到读锁请求之前！这也正是MyISAM表不太适合于有大量更新操作和查询操作应用的原因，因为，大量的更新操作会造成查询操作很难获得读锁，从而可能永远阻塞。可以通过一些设置来调节MyISAM的调度行为。  
<![if !supportLineBreakNewLine]>  
<![endif]>

<![if !supportLists]>· <![endif]>通过指定启动参数low-priority-updates，使MyISAM引擎默认给予读请求以优先的权利。

<![if !supportLists]>· <![endif]>通过执行命令SET LOW_PRIORITY_UPDATES=1，使该连接发出的更新请求优先级降低。

<![if !supportLists]>· <![endif]>通过指定INSERT、UPDATE、DELETE语句的LOW_PRIORITY属性，降低该语句的优先级。

虽然上面3种方法都是要么更新优先，要么查询优先的方法，但还是可以用其来解决查询相对重要的应用（如用户登录系统）中，读锁等待严重的问题。另外，MySQL也提供了一种折中的办法来调节读写冲突，即给系统参数max_write_lock_count设置一个合适的值，当一个表的读锁达到这个值后，MySQL就暂时将写请求的优先级降低，给读进程一定获得锁的机会。上面已经讨论了写优先调度机制带来的问题和解决办法。

  
<![if !supportLineBreakNewLine]>  
<![endif]>

这里还要强调一点：一些需要长时间运行的查询操作，也会使写进程“饿死”！因此，应用中应尽量避免出现长时间运行的查询操作，不要总想用一条SELECT语句来解决问题，因为这种看似巧妙的SQL语句，往往比较复杂，执行时间较长，在可能的情况下可以通过使用中间表等措施对SQL语句做一定的“分解”，使每一步查询都能在较短时间完成，从而减少锁冲突。如果复杂查询不可避免，应尽量安排在数据库空闲时段执行，比如一些定期统计可以安排在夜间执行。

## Innodb存储引擎

# 隔离级别

查看系统隔离级**别**：

**select** @@**global****.**tx_isolation**;**

查看当前会话隔离级**别**

**select** @@tx_isolation**;**

设置当前会话隔离级**别**

**SET**  **session**  **TRANSACTION**  **ISOLATION**  **LEVEL** serializable**;**

设置全局系统隔离级**别**

**SET**  **GLOBAL**  **TRANSACTION**  **ISOLATION**  **LEVEL**  **READ** UNCOMMITTED**;**

**//mysql8 tx****改为****transaction**

# 系统性能测试

定义:  
基准测试是一种测量和评估软件性能指标的活动用于建立某个时刻的性能基准，以便当系统发生软硬件变化时重新进行基准测试以评估变化对性能的影响

基准测试是针对系统设置的一种压力测试

-   基准测试

直接、简单、易于比较 ，用于评估服务器的处理能力

-   压力测试

对真实的业务数据进行测试，获得真实系统所能承受的压力

eg:

-   压力测试需要针对不同主题，所使用的数据和查询也是真实用到的
-   基准测试可能不关心业务逻辑，所使用的查询和业务的真实性可以和业务环境没关系

#### 基准测试的目的

<![if !supportLists]>· <![endif]>建立MySQL服务器的性能基准线  
确定当前MySQL服务器运行情况、以及优化是否有效

<![if !supportLists]>· <![endif]>模拟比当前系统更高的负载，以找出系统的扩展瓶颈

<![if !supportLists]>· <![endif]>测试不同的硬件、软件和操作系统配置

<![if !supportLists]>· <![endif]>证明新的硬件设备是否配置正确

#### 如何进行基准测试

<![if !supportLists]>1. <![endif]>对整个系统进行基准测试

从系统入口进行测试(如网站Web前端，手机APP前端)

<![if !supportLists]>o <![endif]>优点：

<![if !supportLists]>§ <![endif]>能够测试整个系统的性能，包括web服务器缓存、数据库等

<![if !supportLists]>§ <![endif]>能反映出系统中各个组件接口间的性能问题体现真实性能状况

<![if !supportLists]>o <![endif]>缺点：

-   测试设计复杂，消耗时间长

<![if !supportLists]>2. <![endif]>单独对MySQL进行基准测试

<![if !supportLists]>o <![endif]>优点：

-   测试设计简单，所需要耗费时间短

<![if !supportLists]>o <![endif]>缺点：

-   无法全面了解整个系统的性能基准线

#### MySQL基准测试的常见指标

<![if !supportLists]>· <![endif]>单位时间内所处理的事务数（TPS）

<![if !supportLists]>· <![endif]>单位时间内所处理的查询数（QPS）

<![if !supportLists]>· <![endif]>响应时间

平均响应时间、最小响应时间、最大响应时间、各时间所占百分比

<![if !supportLists]>· <![endif]>并发量：同时处理的查询请求的数量

并发量不等于连接数

##   
mysql基准测试工具

## mysqlslap

## sysbench  
<![if !supportLineBreakNewLine]>  
<![endif]>

# Mysql参数

## autocommit参数

1.首先准备一张innodb引擎的测试表：

<![if !supportLists]>1. <![endif]>CREATETABLE`test` (

<![if !supportLists]>2. <![endif]>`id`int(11) NOTNULL

<![if !supportLists]>3. <![endif]>) ENGINE=InnoDB;

<![if !supportLists]>4. <![endif]>INSERTINTO`test`VALUES ('1');

<![if !supportLists]>5. <![endif]>INSERTINTO`test`VALUES ('3');

<![if !supportLists]>6. <![endif]>INSERTINTO`test`VALUES ('5');

2.执行如下命令可以发现mysql的autocommit默认值是ON，也就是开启状态：

3. 当autocommit为开启状态时，即使没有手动start transaction开启事务，mysql默认也会将用户的操作当做事务即时提交。怎么理解呢？例如，你执行了insert into test values(2)语句，mysql默认会帮你开启事务，并且在这条插入语句执行完成之后，默认帮你提交事务。这时候可能有人会问了，那如果我手动开启了事务呢？例如如下操作，开启事务并插入两条数据：

由于A客户端没有提交，因此如果我们用B客户端去查询数据，会发现新插入的数据并没有被查询到：

当我们把A客户端的事务提交了之后，B客户端就能查询到新增加的数据了：

从上述的操作中我们可以明白，当autocommit为ON的情况下，并且又手动开启了事务，那么mysql会把start transaction 与 commit之间的语句当做一次事务来处理，默认并不会帮用户提交需要手动提交，如果用户不提交便退出了，那么事务将回滚。

4.如果我们将autocommit设置为OFF，如下：

那么系统仍然会自动开启事务，但是需要用户手动提交：

这时候，用客户端B去查询数据，你会发现，新增加的4记录没有被查询到：

原因就在于，将autocommit设置为OFF之后，系统默认开始了事务，但是并没有默认帮你提交了事务，因此如果我们在A客户端执行commit之后，B客户端就能查询到新的数据：

# Mysql参考

[https://gitbook.cn/books/5e9a69426e10e519aa233ff1/index.html](https://gitbook.cn/books/5e9a69426e10e519aa233ff1/index.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU4ODA4ODgzXX0=
-->