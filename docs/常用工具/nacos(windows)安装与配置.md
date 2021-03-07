### Nacos下载
Nacos官网地址：[https://nacos.io/zh-cn/index.html](https://nacos.io/zh-cn/index.html)
Nacos下载地址：[https://github.com/alibaba/nacos/releases](https://github.com/alibaba/nacos/releases)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614002708971-a95130b3-150d-4403-8646-5d947116b9a9.png#align=left&display=inline&height=175&margin=%5Bobject%20Object%5D&name=image.png&originHeight=175&originWidth=1012&size=14922&status=done&style=none&width=1012)
我这里下载好了上传到网盘了
链接：[https://pan.baidu.com/s/1P4hM2mrVWsMFTWsCTLfKLg](https://pan.baidu.com/s/1P4hM2mrVWsMFTWsCTLfKLg) 提取码：1avq 
### Nacos安装
1.解压文件，进入conf目录,修改application.properties文件，配置数据库
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614002851235-a5f228ff-4493-4020-9081-7c2c083132ba.png#align=left&display=inline&height=520&margin=%5Bobject%20Object%5D&name=image.png&originHeight=520&originWidth=863&size=57004&status=done&style=none&width=863)
2.执行nacos-mysql.sql
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614002563338-410fbb90-2cd4-4dc3-b333-a38dc7a95418.png#align=left&display=inline&height=274&margin=%5Bobject%20Object%5D&name=image.png&originHeight=274&originWidth=556&size=23924&status=done&style=none&width=556)
### 选择启动模式
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614002980578-cdb2045d-82cc-4858-accb-444aee7654b0.png#align=left&display=inline&height=241&margin=%5Bobject%20Object%5D&name=image.png&originHeight=241&originWidth=646&size=21569&status=done&style=none&width=646)
#### 单机模式
编辑startup.cmd文件，修改 `set MODE="standalone"` ，设置为单机模式，双击cmd启动服务
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614003030063-961731b1-d032-468e-89cd-648f236f5a3a.png#align=left&display=inline&height=389&margin=%5Bobject%20Object%5D&name=image.png&originHeight=661&originWidth=1407&size=74591&status=done&style=none&width=827)
默认地址：[http://127.0.0.1:8848/nacos](http://127.0.0.1:8848/nacos)，初始账号密码都是nacos
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614003191204-7b6265a9-a9b1-4e63-be74-4e1891b31042.png#align=left&display=inline&height=888&margin=%5Bobject%20Object%5D&name=image.png&originHeight=888&originWidth=1894&size=127879&status=done&style=none&width=1894)
#### 集群模式
1.编辑startup.cmd文件，修改`set MODE="cluster"`，设置为集群模式
2.进入conf目录,去除cluster.conf.example文件的.example后缀，配置两个服务地址
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614003684768-b2f6ea9e-da93-4197-91e6-d52c1f451b9b.png#align=left&display=inline&height=768&margin=%5Bobject%20Object%5D&name=image.png&originHeight=768&originWidth=1024&size=69971&status=done&style=none&width=1024)
3.双击startup.cmd启动，发现8848可以访问nacos,但是8849端口访问不了，这里需要复制一份nacos服务，只把服务端口号改为8849即可
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614003960522-35ec25a3-b3cb-4211-a9c9-e9f32861f1e1.png#align=left&display=inline&height=49&margin=%5Bobject%20Object%5D&name=image.png&originHeight=49&originWidth=573&size=4105&status=done&style=none&width=573)
修改application.properties文件
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614003982141-5d447b09-59fa-4cfc-9982-b38a1820e905.png#align=left&display=inline&height=768&margin=%5Bobject%20Object%5D&name=image.png&originHeight=768&originWidth=1024&size=107280&status=done&style=none&width=1024)
将两个服务都启动，这时8848和8849端口都可以访问nacos了
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1614004105623-f85a6faf-0098-4a85-8105-af57c20c2315.png#align=left&display=inline&height=430&margin=%5Bobject%20Object%5D&name=image.png&originHeight=430&originWidth=1289&size=31783&status=done&style=none&width=1289)
