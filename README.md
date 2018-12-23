# mysqlDocker

### 数据库容器化

1. 安装docker

2. 后端添加连接数据库的代码
````
  path := strings.Join([]string{userName, ":", password, "@tcp(", ip, ":", port, ")/", dbName, "?charset=utf8"}, "")
  DB, _ = sql.Open("mysql", path)
````

3. 编写sql文件，建立数据库，建立表格，插入数据
4. 编写dockerfile文件
````
FROM mysql:5.7

#设置免密登录
ENV MYSQL_ALLOW_EMPTY_PASSWORD yes

#将所需文件放到容器中
COPY setup.sh /mysql/setup.sh
COPY schema.sql /mysql/schema.sql
COPY privileges.sql /mysql/privileges.sql

#设置容器启动时执行的命令
CMD ["sh", "/mysql/setup.sh"]
````
5. 构建docker镜像
`sudo docker build -t web_mysql .`
6. 生成容器
`sudo docker run -d --name myweb_mysql  -it -p 3306:3306 web_mysql`



