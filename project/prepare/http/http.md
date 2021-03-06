## 配置本地yum源
我们默认在封闭的网络内部安装集群，将parcel包放置在HTTP协议仓库，可以让ClouderaManager命令Agent去下载内部HTTP仓库的文件。这样免去了手动分发到各个节点的麻烦。

### 操作1(选择在lion部署）
1. 如果按照之前的CentOS安装步骤，那么系统是默认自带Apache HTTP服务的
    - Apache HTTP下载地址：http://httpd.apache.org/download.cgi
    - 如果你连接了外网的话，执行yum安装 $ yum install httpd -y
2. 开启httpd服务 
    - CentOS6 $ service httpd start
    - CentOS7 $ systemctl start httpd
3. 尝试使用浏览器访问其Web UI界面 例如：http://lion
4. 将下载的cm和cdh包都存到/var/www/html下
5. 解压cm包 $tar -xvf cm5.16.1-centos6.tar.gz
6. 创建/var/www/html/cdh目录，将cdh包放入该目录
7. 使用浏览器访问http仓库 http://lion/cm 和 http://lion/cdh

注：请严格按照截图中的路径存放cm和cdh包

### 操作2(所有节点）
1. 进入yum仓库路径 $ cd /etc/yum.repos.d/
2. 创建备份目录bak，将原仓库文件放入其中
3. 创建cloudera-repo.repo文件，并加入HTTP仓库路径等信息（具体操作请看截图）

### 参考资料
- [Cloudera: Using an Internal Parcel Repository](https://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_create_local_parcel_repo.html)
- [Cloudera: Configuring a Local Package Repository](https://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_create_local_package_repo.html)

### 操作截图
- 开启httpd服务

![开启httpd服务](./httpd_start.png)

- Apache界面（里面的owo域名，你用lion就可以了）

![Apache界面](./http_web_ui.png)

- http仓库cm

![http仓库cm](./http_cm.png)

- http仓库cdh

![http仓库cdh](./http_cdh.png)

- 配置yum源仓库（需要自己创建cloudera-repo.repo文件，然后添加内容）

![配置yum源仓库](./conf_yum_repo.PNG)
