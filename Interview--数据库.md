# Interview--数据库

精心收录整理互联网笔试面试题，以及自己发布的文章，欢迎各位star！或者关注微信公众号【1024笔记】，免费获取海量学习资源

. 作者：江夏、

. 简书：https://www.jianshu.com/u/b3263fc54bce

. 知乎：https://www.zhihu.com/people/qing-ni-chi-you-zi-96

. GitHub：https://github.com/JiangXia-1024?tab=repositories

. 博客地址：https://blog.csdn.net/qq_41153943

------

### 1、**数据库的三大范式**

**1 、第一范式（1NF）**

在任何一个关系数据库中，第一范式（1NF）是对关系模式的基本要求，不满足第一范式（1NF）的数据库就不是关系数据库。 

所谓第一范式（1NF）是指数据库表的每一列都是不可分割的基本数据项，同一列中不能有多个值，即实体中的某个属性不能有多个值或者不能有重复的属性。如果出现重复的属性，就可能需要定义一个新的实体，新的实体由重复的属性构成，新实体与原实体之间为一对多关系。

在第一范式（1NF）中表的每一行只包含一个实例的信息。简而言之，第一范式要求数据表中的每一列（每个字段）必须是不可拆分的最小单元。

**2、 第二范式（2NF）**

第二范式（2NF）是在第一范式（1NF）的基础上建立起来的，即满足第二范式（2NF）必须先满足第一范式（1NF）。第二范式（2NF）要求数据库表中的每个实例或行必须可以被惟一地区分。为实现区分通常需要为表加上一个列，以存储各个实例的惟一标识。

第二范式（2NF）要求实体的属性完全依赖于主关键字。所谓完全依赖是指不能存在仅依赖主关键字一部分的属性，如果存在，那么这个属性和主关键字的这一部分应该分离出来形成一个新的实体，新实体与原实体之间是一对多的关系。为实现区分通常需要为表加上一个列，以存储各个实例的惟一标识。简而言之，第二范式要求表中的所有列，都必须依赖于主键，而不能有任何一列与主键没有关系。

**3 、第三范式（3NF）** 

满足第三范式（3NF）必须先满足第二范式（2NF）。第三范式（3NF）要求一个数据库表中不包含其它表中已包含的非主关键字信息。简而言之，第三范式要求表中的每一列只与主键直接相关而不是间接相关，表中的每一列只能依赖于主键。

### 2、**msyql优化方式**

1、对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。

2、应尽量避免在 where 子句中使用!=或<>操作符，否则引擎将放弃使用索引而进行全表扫描。

3、尽量使用数字型字段，若只含数值信息的字段尽量不要设计为字符型，这会降低查询和连接的性能，并会增加存储开销。这是因为引擎在处理查询和连接时会逐个比较字符串中每一个字符，而对于数字型而言只需要比较一次就够了。

4、任何地方都不要使用 select * from t ，用具体的字段列表代替“*”，不要返回用不到的任何字段。

5、避免频繁创建和删除临时表，以减少系统表资源的消耗。

### **3、说出一些数据库优化方面的经验?**

用PreparedStatement 一般来说比Statement性能高：一个sql 发给服务器去执行，涉及步骤：语法检查、语义分析， 编译，缓存

```
“inert into user values(1,1,1)”-→二进制

“inert into user values(2,2,2)”-→二进制

“inert into user values(?,?,?)”-→二进制
```

有外键约束会影响插入和删除性能，如果程序能够保证数据的完整性，那在设计数据库时就去掉外键。（比喻：就好比免检产品，就是为了提高效率，充分相信产品的制造商）

（对于hibernate来说，就应该有一个变化：empleyee->Deptment对象，现在设计时就成了employee→deptid）

看mysql帮助文档子查询章节的最后部分，例如，根据扫描的原理，下面的子查询语句要比第二条关联查询的效率高：

1、select e.name,e.salary where e.managerid=(select id from employee where name='zxx');

2、select e.name,e.salary,m.name,m.salary from employees e,employees m where

 e.managerid = m.id and m.name='zxx';

表中允许适当冗余，譬如，主题帖的回复数量和最后回复时间等

将姓名和密码单独从用户表中独立出来。这可以是非常好的一对一的案例哟！

sql语句全部大写，特别是列名和表名都大写。特别是sql命令的缓存功能，更加需要统一大小写，sql语句→发给oracle服务器→语法检查和编译成为内部指令→缓存和执行指令。根据缓存的特点，不要拼凑条件，而是用?和PreparedStatment

还有索引对查询性能的改进也是值得关注的。

备注：下面是关于性能的讨论举例

4航班 3个城市

```
m*n

select * from flight,city where flight.startcityid=city.cityid and city.name='beijing';

m + n

select * from flight where startcityid = (select cityid from city where cityname='beijing');

select flight.id,'beijing',flight.flightTime from flight where startcityid = (select cityid from city where cityname='beijing')

```

### 4、**union和union all有什么不同?**

Union和Union All的区别之一在于对重复结果的处理。

UNION在进行表链接后会筛选掉重复的记录，所以在表链接后会对所产生的结果集进行排序运算，删除重复的记录再返回结果。实际大部分应用中是不会产生重复的记录，最常见的是过程表与历史表UNION。如：
select * from gc_dfys
union
select * from ls_jg_dfys
这个SQL在运行时先取出两个表的结果，再用排序空间进行排序删除重复的记录，最后返回结果集，如果表数据量大的话可能会导致用磁盘进行排序。
而UNION ALL只是简单的将两个结果合并后就返回。这样，如果返回的两个结果集中有重复的数据，那么返回的结果集就会包含重复的数据了。
从效率上说，UNION ALL 要比UNION快很多，所以，如果可以确认合并的两个结果集中不包含重复的数据的话，那么就使用UNION ALL，

### **5、大数据量下的分页解决方法。**

最好的办法是利用sql语句进行分页，这样每次查询出的结果集中就只包含某页的数据内容。再sql语句无法实现分页的情况下，可以考虑对大的结果集通过游标定位方式来获取某页的数据。

sql语句分页，不同的数据库下的分页方案各不一样，下面是主流的三种数据库的分页sql：

sql server:

​	String sql = 

​	"select top " + pageSize + " * from students where id not in" +

 

 "(select top " + pageSize * (pageNumber-1) + " id from students order by id)" + 

 

 "order by id";

 

mysql:

 

​	String sql = 

​	"select * from students order by id limit " + pageSize*(pageNumber-1) + "," + pageSize;

​	

oracle:

 

​	String sql = 

​	 "select * from " +  

​	 (select *,rownum rid from (select * from students order by postime desc) where rid<=" + pagesize*pagenumber + ") as t" + 

​	 "where t>" + pageSize*(pageNumber-1);