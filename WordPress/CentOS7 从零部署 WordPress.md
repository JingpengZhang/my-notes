```shell
# 1. 设置PHP安装源
sudo yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm
# 2. 安装支持命令 yum-config-manager
sudo yum install yum-utils
# 3. 禁用PHP版本（除8.3）
sudo yum-config-manager --disable 'remi-php*'
sudo yum-config-manager --enable remi-php83
# 4. 安装PHP支持组件
sudo yum install -y php-fpm php-mysql php-pdo
# 5. 安装PHP
sudo yum install -y php
# 6. 设置PHP开机自启
sudo systemctl start php-fpm
sudo systemctl enable php-fpm.service
```
测试是否安装成功
```shell
php -v
```
如果控制台出现PHP版本信息，则表示安装成功
```shell
PHP 8.3.8 (cli) (built: Jun  4 2024 14:53:17) (NTS gcc x86_64)
...
```
原作者： https://blog.csdn.net/cive/article/details/134688070
### 2. 安装Nginx
```shell
# 安装
sudo yum -y install nginx
# 设置开机自启
sudo systemctl enable nginx
# 启动
sudo service nginx start
```
测试是否安装并启动成功
在浏览器上输入`服务器公网IP:80`,如果能成功访问即为安装成功（请先在防火墙设置中放行`80`端口）
附常用Nginx命令
```shell
# 卸载
sudo yum remove nginx
# 停止服务
sudo service nginx stop
# 重启服务
sudo service nginx restart
# 重新加载配置（修改配置文件后使用，否则修改不生效）
sudo service nginx reload

```
### 3. 安装Mysql8
1. 下载mysql官方yum源（地址见 https://dev.mysql.com/downloads/repo/yum/ ）
```shell
# 将源下载到指定目录
wget https://dev.mysql.com/get/mysql84-community-release-el7-1.noarch.rpm
```
2. 安装官方源
```shell
sudo rpm -ivh mysql84-community-release-el7-1.noarch.rpm
```
1. 清理并更新yum源缓存
```shell
# 清理 yum 缓存目录
yum clean all
# 更新 yum 缓存
yum makecache
```
2. 导入GPG密钥（GPG密钥是处于安全考虑，用来验证下载的包是否是原始的、未被篡改的，如果不需要校验密钥，可在安装时加入`--nogpgcheck`参数跳过校验。）
```shell
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```
3. 安装 mysql
```shell
sudo yum install -y mysql-community-server mysql-community
```
4. 验证是否安装成功
```shell
mysql -V
```
5. 出现下列信息表示安装成功：
```shell
mysql  Ver 8.4.2 for Linux on x86_64 (MySQL Community Server - GPL)
```
6. 查看 root 初始密码
```shell
sudo grep 'temporary password' /var/log/mysqld.log
```
控制台会打印
```shell
2024-10-11T02:00:36.802916Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: '初始密码'
```
7. 登录 mysql
```shell
mysql -u root -p
# 会提示输入上一步获取的初始密码
```
8. 修改密码
```shell
ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';
```
> 注意：如果在修改密码时，提示 `ERROR 1819 (HY000): Your password does not satisfy the current policy requirements`，表示新密码不符合设定的密码规则。可以通过 `SHOW VARIABLES LIKE 'validate_password%';` 命令查看密码规则，但是该命令只能在修改密码成功后使用。新密码可以尝试包含各一位特殊字符、大写字母、小写字母、数字（我尝试之后可以）。

### 4. 安装 wordpress
9. 进入nginx网站部署目录
10. 下载 wordpress 包
```shell
sudo wget https://wordpress.org/latest.tar.gz
```
11. 解压 wordpress 包
```shell
sudo tar -xzvf latest.tar.gz
```
12. 配置 nginx
13. 防火墙放行指定端口号