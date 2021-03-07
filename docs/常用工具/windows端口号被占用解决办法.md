1.打开cmd命令窗口
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1610899341251-0a8f7ad1-0745-42a8-8fb8-af9644337d43.png#align=left&display=inline&height=198&margin=%5Bobject%20Object%5D&name=image.png&originHeight=198&originWidth=397&size=10445&status=done&style=none&width=397)
2.在弹出的命令创建输入命令  netstat -aon|findstr "3306"，引号的3306就是我们需要查询的端口号
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1610899465426-adf3445c-3e94-4dd1-b5cf-1d7aa35dd98c.png#align=left&display=inline&height=480&margin=%5Bobject%20Object%5D&name=image.png&originHeight=480&originWidth=960&size=19044&status=done&style=none&width=960)
查询到对应的程序pid号
3.输入新的命令，查询端口被占用程序，tasklist|findstr "2740"
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1610899554990-7ffc67d6-253b-44c8-84c2-a1dcc6654851.png#align=left&display=inline&height=480&margin=%5Bobject%20Object%5D&name=image.png&originHeight=480&originWidth=960&size=20756&status=done&style=none&width=960)
这里显示被mysqld.exe占用了
4.杀死这个进程，打开任务管理器，找到对应程序右键结束任务即可
![image.png](https://cdn.nlark.com/yuque/0/2021/png/163552/1610899634968-1931ad13-8b39-4513-b6cc-78afacd6abc2.png#align=left&display=inline&height=541&margin=%5Bobject%20Object%5D&name=image.png&originHeight=541&originWidth=664&size=71206&status=done&style=none&width=664)
