# redis
## 注意要点
    1.先配置，配置完要带配置启动(配置守护启动daemonize yes，允许外链接客户端使用bind 0.0.0.0，)》启动服务./bin/redis-server redis.conf 启动客户端./bin/redis-cli 
    2. linux安装先要先安装c语言编译器


## 安装教程
[链接](http://note.youdao.com/noteshare?id=c01078eb2aaa15a0f5dfca4d605a3474)
## 常用操作命令
```
一、键命令：
    keys pattern    查找键，支持正则表达式
        keys *
        key 'a*'
    exists key      判断 键是否存在
    type key        查找键对应的数据类型
    del key1 key2 . 删除键
	expire key seconds  设置key的过期时间
	ttl key      查看键剩余的过期时间

二、String 字符串 最多512M
    set key value  key不存在则设置键值，存在则修改键值
    set key seconds value 设置键值以及过期时间
		mset key1 value1 key2 value2 ... 设置多个键值
    append key value  追加值

    get key  获取值
		mget key1 key2 ...  获取多个键值

三、hash 哈希
    hset key field value  设置键值
        hmset key field1 value1 field2 vlaue2 ...
	hkeys key 获取key的所有属性
    hget key  field 获取值
        hmget keys key1 field1 key2 field2 ..
	hvals key  获取所有属性的值
    hdel key field 删除值

四、List 链表
    lpush key value  在链表的左侧追加元素
    rpush key value  在链表的右侧追加元素
    insert key before或after 现有元素  新元素  在指定位置插入值
	lset key key index value  设置指定位置元素的值

    lrange key start stop 获取元素的值
	lrem key count(移除元素的次数) vlaue 删除元素
		count > 0 从左往右移除
		count < 0 从右往左移除
		count = 0 移除所有
	
	llen 获取列表的长度
	ltrim key star stop  对列表进行裁剪

五、set 集合 不能重复  无序
	sadd key member1 member2 ...  添加元素
	smemebers key  获取元素
	srem key members 删除元素

六、zset 有序集合
	zadd key score1 member1 score2 member2 ... ... 添加元素
	zrange key start end 获取元素
	zrangebyscore key a b  获取权重在a到b之间的成员
	zcore key member  查看成员的权重
	zrem key member1 member2 ...  删除成员
————————————————
版权声明：本文为CSDN博主「苍穹之宇」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_43192730/article/details/86259569
```
## java连接redis
[教程](https://www.cnblogs.com/youcong/p/8098881.html)