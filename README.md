Docker安装

下载Docker依赖组件

```bash
yum install -y yum-utils device-mapper-persistent-data lvm2
```

设置下载Docker的镜像源为阿里云

```bash
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

安装Docker服务

```bash
yum install -y docker-ce
```

安装成功后，启动Docker并设置开机自启

```bash
systemctl start docker
systemctl enable docker
```

测试安装成功

```bash
docker version
```



Docker-compose安装

下载地址 https://github.com/docker/compose/releases/download/v2.5.1/docker-compose-linux-x86_64

```bash
wget -c https://github.com/docker/compose/releases/download/v2.5.1/docker-compose-linux-x86_64
```

赋予可执行权限

```bash
chmod +x docker-compose-linux-x86_64
mv docker-compose-linux-x86_64 docker-compose
mv docker-compose /usr/bin/
```

测试安装

```bash
docker-compose --version
```



### 配置打卡服务

编写环境变量配置数据库账户，文件.env为环境变量配置

```bash
# 数据库名
MYSQL_DATABASE=django_mysql
# 数据库root用户密码
MYSQL_ROOT_PASSWORD=123
# 数据库普通用户名
MYSQL_USER=yiban
# 数据库普通用户密码
MYSQL_PASSWORD=123
# 数据库主机名，参考docker-compose
MYSQL_HOST=db
# 数据库端口
MYSQL_PORT=3306
# 指定时区
TZ=Asia/Shanghai
# 后台管理地址
ADMIN_PATH=admin
# 邮箱用户名
MAIL_USER=your mail user name
# 邮箱秘钥
MAIL_PASS=your mail user password
# 邮箱服务器
MAIL_HOST=your mail host
```
需要在邮箱设置中开启SMTP服务，并设置，报错提示key cannot contain a space：需要填写邮箱相关信息
启动服务

```bash
docker-compose up -d
```

服务启动完成后访问`http://服务器IP/admin/`进行登录



创建管理员用户

```bash
docker exec -it yiban_web python manage.py createsuperuser
```

