### MongoDB一些要点

#### MongoDB数据的备份 

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
默认情况下，MongoDB 会在当前目录下创建一个 dump 目录，并把所有的数据库按数据库名称创建目录。在这个实例中，有两数据库 admin 、test、express-demo、population-test 四个数据库。

以下是可用于 mongodump 命令的可用选项的列表。
语法 | 描述 | 示例 
- | :-: | -: 
mongodump —host HOST_NAME —port PORT_NUMBER | 此命令将备份指定的 mongod 实例的所有数据库。| mongodump --host 127.0.0.1 --port 27017 
mongodump —out BACKUP_DIRECTORY | 此命令将仅在指定路径上备份数据库。 | mongodump --out /mongodb/mongobak 
mongodump —collection COLLECTION —db DB_NAME | 此命令将仅备份指定数据库的指定集合。 | mongodump --collection mycol --db test

#### MongoDB数据的恢复

要恢复备份数据，使用MongoDB的 mongorestore 命令。 此命令从备份目录中恢复所有数据。
```bash
mongorestore
```
