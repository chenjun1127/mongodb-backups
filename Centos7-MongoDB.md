### Ceontos安装nodejs

参考：[阿里云服务器安装 nodejs](https://help.aliyun.com/document_detail/50775.html?spm=5176.doc25429.6.644.3D2aMv)

### Centos7 安装 Mongodb

* 下载安装包

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.9.tgz
```

* 解压

```
tar -zxvf  mongodb-linux-x86_64-4.0.9.tar.xz
```

* 移动到指定位置
```
mv mongodb-linux-x86_64-3.2.12/ /usr/local/mongodb 
```

* 建软链接
```
ln -s /usr/local/mongodb/bin/mognod /user/local/bin/mongod
ln -s /usr/local/mongodb/bin/mogno /user/local/bin/mongo
```

* 新建 mongodb 存放目录
```
cd /usr/local/mongodb/
mkdir -p logs/mongodb.log
mkdir data
```

* 建 Mongodb 配置文件
```
cd /user/local/mongodb/bin/
vim mongodb.conf
```

* 在 mongodb.conf 输入以下
```
dbpath = /usr/local/mongodb/data #数据文件存放目录
logpath = /usr/local/mongodb/logs/mongodb.log #日志文件存放目录
port = 27017  #端口
fork = true  #以守护程序的方式启用，即在后台运行
auth = true
bind_ip = 0.0.0.0
```

* 启动，在/user/local/mongodb/bin/目录下
```
mongod -f mongodb.conf 或 ./mongod -f mongodb.conf
```

参考：[centos7 安装mongodb](https://www.cnblogs.com/saryli/p/9822819.html)
