### MongoDB一些要点

#### 一、MongoDB数据的备份与恢复 

* 备份

要在MongoDB中创建数据库备份，应该使用 mongodump 命令。 此命令将导出转储服务器的整个数据到转储目录。

启动 mongod 服务，并连接数据库，然后启动命令：
```bash
mongodump
```
回车之后可以看到如下：
```bash
2017-11-23T18:11:18.684+0800    writing admin.system.version to
2017-11-23T18:11:18.710+0800    done dumping admin.system.version (1 document)
2017-11-23T18:11:18.710+0800    writing population-test.comments to
2017-11-23T18:11:18.710+0800    writing population-test.posts to
2017-11-23T18:11:18.710+0800    writing express-demo.movies to
2017-11-23T18:11:18.710+0800    writing express-demo.categories to
2017-11-23T18:11:18.711+0800    done dumping population-test.posts (38 documents
)
2017-11-23T18:11:18.711+0800    done dumping population-test.comments (38 docume
nts)
2017-11-23T18:11:18.712+0800    writing test.users to
2017-11-23T18:11:18.712+0800    writing express-demo.comments to
2017-11-23T18:11:18.713+0800    done dumping test.users (4 documents)
2017-11-23T18:11:18.713+0800    writing express-demo.users to
2017-11-23T18:11:18.714+0800    done dumping express-demo.comments (5 documents)

2017-11-23T18:11:18.714+0800    done dumping express-demo.movies (28 documents)
2017-11-23T18:11:18.715+0800    writing express-demo.sessions to
2017-11-23T18:11:18.716+0800    writing population-test.users to
2017-11-23T18:11:18.716+0800    done dumping express-demo.categories (5 document
s)
2017-11-23T18:11:18.716+0800    done dumping express-demo.users (3 documents)
2017-11-23T18:11:18.717+0800    writing test.news to
2017-11-23T18:11:18.718+0800    done dumping population-test.users (3 documents)

2017-11-23T18:11:18.718+0800    done dumping express-demo.sessions (1 document)
2017-11-23T18:11:18.719+0800    writing test.books to
2017-11-23T18:11:18.719+0800    done dumping test.news (1 document)
2017-11-23T18:11:18.720+0800    done dumping test.books (1 document)
```
默认情况下，MongoDB 会在当前目录下创建一个 dump 目录，并把所有的数据库按数据库名称创建目录。在这个实例中，有以下 admin 、test、express-demo、population-test 四个数据库。

以下是可用于 mongodump 命令的可用选项的列表。

| 语法        										| 描述           								| 示例  									|
| ------------------------------------------------- |:----------------------------------------------| ------------------------------------------|
| ongodump —host HOST_NAME —port PORT_NUMBER      	| 此命令将备份指定的 mongod 实例的所有数据库。 	| mongodump --host 127.0.0.1 --port 27017 	|
| mongodump —out BACKUP_DIRECTORY     				| 此命令将仅在指定路径上备份数据库。      		| mongodump --out /mongodb/mongobak 		|
| mongodump —collection COLLECTION —db DB_NAME      | 此命令将仅备份指定数据库的指定集合。			| mongodump --collection mycol --db test 	|


* 恢复

要恢复备份数据，使用MongoDB的 mongorestore 命令。 此命令从备份目录中恢复所有数据。
```bash
mongorestore
```
#### 二、MongoDB数据的导入与导出

数据导出：mongoexport

* 概念：

mongoDB中的mongoexport工具可以把一个collection导出成JSON格式或CSV格式的文件。可以通过参数指定导出的数据项，也可以根据指定的条件导出数据。

* 语法：

mongoexport -d dbname -c collectionname -o file --type json/csv -f field
参数说明：
-d ：数据库名
-c ：collection名
-o ：输出的文件名
--type ： 输出的格式，默认为json
-f ：输出的字段，如果-type为csv，则需要加上-f "字段名"

* 示例：
```bash
mongoexport -d shop-mall -c users -o /back-up/mongoDB/shop-mall/users.json 
```

数据导入：mongoimport

*语法：
```bash
mongoimport -d dbname -c collectionname --file filename --headerline --type json/csv -f field
```

参数说明：
 -d ：数据库名
-c ：collection名
--type ：导入的格式默认json
-f ：导入的字段名
--headerline ：如果导入的格式是csv，则可以使用第一行的标题作为导入的字段
--file ：要导入的文件
 
* 示例：
```bash
mongoimport -d shop-mall -c users --file back-up/data/shop-mall/users.json
```


#### 三、MongoDB的配置启动 

众所周知，Mongodb的启动首先要指定数据库的存储目录，可以在命令行指定，也可以通过配置文件的方式来指定。通过配置文件的指定见下面，新建一个mongo.conf文件，输入以下
```bash
#数据库路径
dbpath=d:\MongoDB\data\
#日志输出文件路径
logpath=d:\MongoDB\logs\mongo.log
#错误日志采用追加模式，配置这个选项后mongodb的日志会追加到现有的日志文件，而不会重新创建一个新文件
logappend=true
#启用日志文件，默认启用
journal=true
#这个选项可以过滤一些无用的日志信息，若需要调试使用请设置为false
quiet=false
#端口号，默认为27017
port=27017
```
然后保存文件，在命令行启动：
```
mongod --config d:\mongo.conf
```
即可启动成功（前提是上面配置指定的文件目录存在）。

#### 3、将Mongo安装到系统服务启动
上面的方法无法避免每次都要打开命令行输入相关命令，那么如何将mongo安装到电脑服务里启动呢？见下面：
```
mongod --config d:\mongo.conf --install --serviceName "MongoDB"
```
回车之后，就已经安装到系统服务了，可以打开控制面板--管理工具--服务，即可看到MongoDB服务。


