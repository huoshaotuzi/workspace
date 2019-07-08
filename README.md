# Docker-compose project
包含了 PHP+MySQL+Redis 环境的 docker-compose 项目，clone 下来进入到文件目录，使用 docker-compose up -d 启动即可！妈妈再也不用担心我的 PHP 环境了。

# 目录结构
- var/logs 项目各种日志文件存放点
- nginx/conf/conf.d nginx 配置文件目录
- php-fpm/conf php-fpm 配置文件目录
- redis/conf redis 配置文件目录
- www web 项目文件目录

# 连接 MySQL
由于 docker 容器是隔离的，容器之间如果需要通信，需要使用容器名称，而不是 127.0.0.1 这样的地址。

连接 MySQL 中的 host 应该为：mysql

# 连接 Redis
同上，连接 Redis 的地址应该填写：redis

# 示例代码
一个简单的连接 MySQL 与 Redis 的代码。

```
<?php
// 数据库类型
$dbms='mysql';
// 数据库主机名，此处不能填写IP地址，而是容器名字
$host='mysql';
//使用的数据库
$dbName='test';
//数据库连接用户名
$user='root';
// mysql/Dockerfile 中的密码
$pass='huotu@666';
$dsn="$dbms:host=$host;dbname=$dbName;";

try {
    $dbh = new PDO($dsn, $user, $pass); //初始化一个PDO对象
    echo "连接成功<br/>";
    foreach ($dbh->query('SELECT * from users') as $row) {
        print_r($row);
    }

    $dbh = null;
} catch (PDOException $e) {
    die ("Error!: " . $e->getMessage() . "<br/>");
}

try {
    $redis = new Redis();
    // 连接 redis 同样使用容器名称
    $redis->connect('redis',6379);
    $redis->set('name', 'xiaobai');

    $name = $redis->get('name');
    var_dump($name);
} catch (\Exception $e) {
    die('Redis错误：' . $e->getMessage());
}
```
