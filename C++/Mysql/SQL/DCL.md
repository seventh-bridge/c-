# DCL（创建数据库用户、控制数据库的访问权限）
## 管理用户
1. 查询用户：`use mysql`;
2. 创建用户：`create user '用户名'@'主机名(%表示任意用户都能访问)' identified by '密码';`
3. 修改用户密码：`alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';`
4. 删除用户：`drop user '用户名'@'主机名';`
## 权限控制
1. 查询权限：`show grants for '用户名'@'主机名';`
2. 授予权限：`grant 权限列表 on 数据库.表名 to '用户名'@'主机名';`
3. 撤销权限：`revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';`