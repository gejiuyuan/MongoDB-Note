### 一、MongoDB简介



#### 1、什么是MongoDB

MongoDB时一个基于分布式文件存储的数据库，由C++编写，旨在为Web应用提供可扩展的高性能（比MySQL高、Redis低）数据存储解决方案。

MongoDB时一个介于关系型和非关系型数据库之间的产品，时非关系型数据库中功能最丰富，最像关系型数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。MongoDB最大特点是支持的查询语言非常强大，语法类似于面向对象的查询语言，几乎可以实现类似关系型单表查询的绝大部分功能，而且还支持对数据建立索引。



#### 2、什么是NoSQL

NoSQL全称Not Only SQL，不仅仅是SQL，是一项全新的数据库革命性运动，早起就有人提出，发展到2009年趋势愈发高涨。



#### 3、NoSQL数据库分类



##### 3.1 键值存储数据库

这一类数据库主要会使用到一个哈希表，这个表中有一个特定的键和一个指针指向特定的数据。key/value模型对于it系统来说的优势在于简单、易部署。但如果是DBA只对部分值进行查询或更新的时候，key/value就显得效率低下，常用于数据缓存。常见的如：Tokyo、Redis

##### 3.2 列存储数据库

这类数据库通常是用来应对分布式存储的海量数据。键仍然存在，但是它们的特点是指向了多个列。这些列是由列家族来安排的。如HBase、Riak

##### 3.3 文档型数据库

文档型数据库的灵感来自于Lotus Notes办公软件（很像Excel、Access）的，而且它同第一种键值存储类似。该类型的数据模型是版本化的文档，半结构化的文档以特定的格式存储，比如JSON、XML。文档型数据库可以看作是键值数据库的升级版，允许之间嵌套键值。而且文档型数据库比键值数据库的部分数据批量查询效率更高。比如：CouchDB、MongoDB，国内也有文档型数据库SequoiaDB

##### 3.4 图形（Graphic）数据库

图形结构的数据库同其他行列以及刚性结构的SQL数据库不同，它使用灵活的图形模型，并且能够扩展到多个服务器上。

NoSQL数据库没有标准的查询语言（SQL），因此进行数据库查询需要指定数据模型。许多NoSQL数据库都有REST式的数据接口或者查询API。如Neo4J、InfoGrid、Infinite Graph。



#### 4、MongoDB与关系型数据库属于对比

| SQL术语     | MongoDB术语 | 解释说明                                               |
| ----------- | ----------- | ------------------------------------------------------ |
| database    | database    | 数据库                                                 |
| table       | collection  | 数据库表/集合                                          |
| row         | document    | 数据记录行/文档                                        |
| column      | field       | 数据字段/域                                            |
| index       | index       | 索引                                                   |
| table joins |             | 表连接，MongoDB不支持                                  |
| primary key | primary key | 主键，MongoDB自动将_id字段（类型：ObjectId）设置为主键 |



#### 5、RDBMS与MongoDB对应的术语

| RDBMS  | MongoDB                     |
| ------ | --------------------------- |
| 数据库 | 数据库                      |
| 表格   | 集合                        |
| 行     | 文档                        |
| 列     | 字段                        |
| 表联合 | 嵌入文档                    |
| 主键   | 主键(MongoDB提供了key为_id) |



#### 6、数据库服务和客户端

| 数据库  | 服务端 | 客户端  |
| ------- | ------ | ------- |
| MongoDB | mongod | mongo   |
| MySQL   | Mysqld | mysql   |
| Oracle  | Oracle | sqlplus |

例如要连接一个MogonDB服务器，即mongod，可以在命令行中通过mongo指令来连接mongod。



### 二、MongoDB数据类型

| 数据类型     | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| String       | 字符串。存储数据常用的数据类型，在MongoDB中，UTF-8编码的字符才是合法的 |
| Integer      | 整型数值。用于存储数值。根据服务器类型，可分为32和64位       |
| Boolean      | 布尔值。                                                     |
| Double       | 双精度浮点值，用于存储浮点值                                 |
| Min/Max keys | 将一个值和BSON（二进制的JSON）元素的最低值和最高值相对比     |
| Array        | 用于将数组或列表或者多个值存储为一个键                       |
| Timestamp    | 时间戳。记录文档修改或添加的具体时间                         |
| Object       | 用于内嵌文档                                                 |
| Null         | 用于创建空值                                                 |
| Symbol       | 符号。该数据类型基本上等同于字符串，但不同是，它一般用于采用特殊符号类型的语言 |
| Date         | 日期时间。用UNIX时间格式来存储当前日期或事件。你可以指定自己的日期时间：创建Date对象，传入年月日信息 |



### 三、MongoDB下载和安装



### 四、用户管理



#### 1、MongoDB中常用权限

| 权限名               | 描述                                                         |
| -------------------- | ------------------------------------------------------------ |
| read                 | 允许用户读取指定数据库                                       |
| readWrite            | 允许用户读写指定数据库                                       |
| dbAdmin              | 允许用户在指定数据库中执行管理函数，如索引创建、删除、查看统计或者访问system.profile |
| userAdmin            | 允许用户向system.users集合（一个表）写入，可以在指定数据库里创建、删除和管理用户 |
| clusterAdmin         | 只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限 |
| readAnyDatabase      | 只在admin数据库中可用，赋予用户所有数据库的读权限            |
| readWriteAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的读写权限          |
| userAdminAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的userAdmin权限     |
| dbAdminAnyDatabase   | 只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限       |
| root                 | 只在admin数据库中可用。超级账号、超级权限                    |



#### 2、



### 五、Database操作



### 六、Collection操作



MongoDB中的集合是一组文档的集，相当于关系型数据库中的表。



#### 1、创建集合

```
db.createCollection(name, options)
```

- name：集合名称

- options：

  | 名称        | 含义                                                         |
  | ----------- | ------------------------------------------------------------ |
  | capped      | 布尔值，表示该集合的容量限制与否。默认false，即该集合没有容量限制 |
  | size        | 若capped为true，则该属性必须指定。单位：字节（byte），如size:2000，表示2048字节 |
  | max         | 限制集合中最多存入的对象                                     |
  | autoIndexId | 布尔值，表是否为_id元数据自动创建索引，默认值为true。注意：该属性未来将被废弃 |



#### 2、查看集合



| 命令                            | 含义                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| show tables 或 show collections | 查看所有的集合                                               |
| db.user_info.stats()            | 查看user_info集合的状态（如存储容量大小storageSize，数据数量count等） |
| db.user_info.drop()             | 删除user_info集合，成功删除返回true。如果已经删除过了，再删除，则返回false |

 

### 七、Document操作



在MongoDB中文档是指多个键及其关联的值有序的放置在一起的对象，其数据结构和JSON基本一样，所有存在集合中的数据都是BSON（B）格式。



#### 1、新增数据

##### 1.1 insert

| 命令                                                         | 含义                          |
| ------------------------------------------------------------ | ----------------------------- |
| db.user_info.insert({"name":"guoxiaoyou", "pswd":"123"})     | 给user_info集合中添加一条数据 |
| db.user_info.insert([{"name":"guoxiaoyou", "pswd":"123"}, {"name":"dididi", "pswd":"345"}]) | 给user_info集合中添加两条数据 |

##### 1.2 save

| 命令                                                         | 含义                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| db.user_info.save({"name":"guoxiaoyou", "pswd":"123"})       | 给user_info集合添加一条数据（可以是覆盖一条数据） |
| db.user_info.save([{"name":"guoxiaoyou", "pswd":"123"}, {"name":"dididi", "pswd":"345"}]) | 给user_info集合添加两条数据（可以是覆盖一条数据） |

##### 1.3 insertOne

这也是MongoDB 3之后推荐的插入一条数据的写法

| 指令                                                      | 含义                          |
| --------------------------------------------------------- | ----------------------------- |
| db.user_info.insertOne({"name":"xiaoming", "pswd":"567"}) | 给user_info集合中添加一条数据 |

##### 1.4 insertMany

这也是MongoDB 3之后推荐的插入多条数据的写法

| 指令                                                         | 含义                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| db.user_info.insertMany([{"name":"guoxiaoyou", "pswd":"123"}, {"name":"dididi", "pswd":"345"}]) | 给user_info集合添加两条数据（可以是覆盖一条数据） |

##### 1.5 变量

```
user_info=({"name":"xiaoming", "pswd":"567"}) //声明一个user_info变量值
db.user_info.insert(user_info) //插入该变量值数据

user_info2=([{"name":"guoxiaoyou", "pswd":"123"}, {"name":"dididi", "pswd":"345"}]) //声明一个user_info2变量值
db.user_info.insert(user_info2) //插入该变量值数据
```



#### 2、查询数据

##### 2.1 find

即查询匹配到的所有数据



**基本查询**

| 命令                                     | 含义                                                    |
| ---------------------------------------- | ------------------------------------------------------- |
| db.user_info.find()                      | 查找user_info集合中的所有文档（数据）                   |
| db.user_info.find({})                    | 查找user_info集合中的所有文档（数据）                   |
| db.user_info.find({"name":"guoxiaoyou"}) | 查找user_info集合中的name属性为guoxiaoyou的文档（数据） |



**投影查询**

现有user_info集合表，其数据为：

```
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" , "age": 20 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d3"), "name": "huahua" , "age": 22 }

db.user_info.find({} , {"name": 0}) //表示查询所有数据，但过滤掉name属性。为1时，则表示不过滤
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "age": 20 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "age": 21 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d3"), "age": 22 }

//同样的
db.user_info.find({"name":"guoxiaoyou"}, {"age": 0})
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" }
```

> *投影约束：*
>
> 在MongoDB中，_id字段是默认返回显示的投影字段。砸门通过传入1或0来筛选要显示或过滤掉的数据属性值。但有两点要注意：
>
> - 若"_id"为0，其它字段可为1，也可为0，而如果为1，则其它字段必须都为1，否则报错
> - 若没有指定"_id"约束，其它字段不能互斥

例如：

```
db.user_info.find( {}, { "age": 0 , "_id": 0 } ) //可以
db.user_info.find( {}, { "age": 1, "_id": 0 } ) //可以

db.user_info.find( {}, { "age": 0 , "_id": 1 } ) //报错
db.user_info.find( {}, { "age": 0 , "name": 1,  "_id": 1 } ) //报错
db.user_info.find( {}, { "age": 1 , "_id": 1 } ) //可以

db.user_info.find( {}, { "age": 0 , "name": 1 } ) //报错
db.user_info.find( {}, { "age": 0 , "name": 0 } ) //可以
```



**比较查询**

$lt（小于）、$gt（大于）、$lte（小于等于）、$gte（大于等于）、$ne（不等于），如：

```
//查询age小于22的文档
db.user_info.find({"age":{"$lt":22}})
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" , "age": 20 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 } 

//查询name小于"hc"的文档
db.user_info.find( { "name": { "$lt": "hc" } } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" , "age": 20 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }

//查询name小于"hc"并且大于"gz"的文档
db.user_info.find( { "name": { "$lt": "hc" , "$gt":  "gz" } } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }

//查询name小于"hc"并且大于"gz"，以及age大于20的文档
db.user_info.find( { "name": { "$lt":"hc", "$gt": "gz" } }, "age": { "$gt": 20 } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }
```



**或查询**

即$or（或者）

```
//查询name小于"hc"并且大于"gz"，或者age大于20的文档
db.user_info.find( { "$or": [ {"name":{"$lt":"hc", "$gt": "gz"}}, "age":{"$gt": 20} ] } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }
```



**类型查询**

即$type（数据类型)

```
//查询name的类型为string的文档
db.user_info.find( { "name": { "$type": "string" } } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" , "age": 20 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d2"), "name": "hahaha" , "age": 21 }
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d3"), "name": "huahua" , "age": 22 }
```

$type有效值为：

| 类型                   | 数字编号 | 别名                  | 注意               |
| ---------------------- | -------- | --------------------- | ------------------ |
| Double                 | 1        | "double"              |                    |
| String                 | 2        | "string"              |                    |
| Object                 | 3        | "object"              |                    |
| Array                  | 4        | "array"               |                    |
| Binary data            | 5        | "binData"             |                    |
| Undefined              | 6        | "undefined"           | Deprecated已废弃   |
| ObjectId               | 7        | "objectid"            |                    |
| Boolean                | 8        | "bool"                |                    |
| Date                   | 9        | "data"                |                    |
| Null                   | 10       | "null"                |                    |
| Regular Expression     | 11       | "regexp"              |                    |
| DBPointer              | 12       | "dbPointer"           | Deprecated已废弃   |
| JavaScript             | 13       | "javascript"          |                    |
| Symbol                 | 14       | "symbol"              | Deprecated已废弃   |
| JavaScript(with scope) | 15       | "javascriptWithScope" |                    |
| 32-bit integer         | 16       | "int"                 |                    |
| Timestamp              | 17       | "timestamp"           |                    |
| 64-bit integer         | 18       | "long"                |                    |
| Decimal128             | 19       | "decimal"             | New in Version 3.4 |

使用$type匹配时，即可使用类型别名，也可使用数字编号，如：

```
db.user_info.find( { "name": { "$type": "string" } } )
//和
db.user_info.find( { "name": { "$type": 2 } } )
//同义
```



**正则查询**

```
//查询name属性以g开头的文档
db.user_info.find( { "name": { $regexp: /^g/  } )
//简写为
db.user_info.find( { "name": /^g/ } )

//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" , "age": 20 }
```



##### 2.2 findOne

即查询匹配到的第一条数据，具体查询语法与find一致



##### 2.3 pretty

让查询结果格式化显示（在命令行中）

```
db.user_info.find( { "name": "guoxiaoyou" } , { "age":  0 } )
//结果为
{ "_id": ObjectId("5e9e9f945868ff5951bdf6d1"), "name": "guoxiaoyou" }

//而如果是
db.user_info.find( { "name": "guoxiaoyou" }, { "age": 0 } ).pretty()
//则结果为
{ 
	"_id": ObjectId("5e9e9f945868ff5951bdf6d1"),
	"name": "guoxiaoyou" 
}
```

另外，对于findOne方法，其查询结果默认是pretty格式化过的，所以无需再使用pretty操作，如果再调用了，则会报错。



### 八、内置函数



### 九、运算符























