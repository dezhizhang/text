### egg 运行 npm run dev 报错 nodejs.AppWorkerDiedError 怎么解决？
#### 1，数据库密码错误
#### 2，mysql为强密码模式。
这个问题是由于mysql安装时傻瓜式一键下一步导致的（我就这样），所以下图选项最好选择第二个，普通模式就不会有这个报错了。
![mysql](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL2ktYmV0YS8xMDY5MDUxLzIwMjAwMy8xMDY5MDUxLTIwMjAwMzE3MTA0MDI1MTc3LTE0MDc5MjgwNzYucG5n?x-oss-process=image/format,png)
但这个错误，那肯定是安装好的，大家可以通过命令行修改为普通模式，步骤如下
1、 打开命令行，输入cd /usr/local/mysql/，进入mac文件夹， 此为mac地址， 其他系统的地址我不知道，就麻烦大家自行搜索了。

2、切换到bin目录下，输入 cd bin

3、登录mysql， 输入 ./mysql -u root -p  然后输入初始密码，如果提示密码错误或者需要修改执行第4步，不需要修改密码的直接看第6步就好了

4、输入 SET PASSWORD FOR ‘root’@‘localhost’ = PASSWORD(‘新密码’)；

5、修改完密码 刷新权限， 输入 FLUSH PRIVILEGES;

6、强密码模式改为普通模式，输入ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER; 提示Query OK就是成功了。

7、更新用户密码，输入 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

8、刷新权限， 输入 FLUSH PRIVILEGES;

这样就可以了，再次连接好数据库，重新跑项目就好了。