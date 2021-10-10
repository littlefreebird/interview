# linux命令
1. 如何通过进程监听端口查询此进程  
lsof -i:8080  
netstat -anp | grep 8080 | grep LISTEN
2. 如何检测远程服务是否启动  
telnet 1.2.3.4 8080
3. 如何查询磁盘使用情况  
df -h 
4. 如何查询进程cpu、内存使用情况  
top
5. 如何查询进程工作目录  
cat /proc/1234/cwd
6. 如何查询进程运行时间、启动时间  
ps -eo pid,lstart,etime | grep nginx
7. 如何让一个bin以守护进程启动运行  
./xxx &
8. 如何进入自己home目录  
cd   
cd ~
9. 当前root账号，如何进入用户xxx的home目录  
cd xxx~
10. 如何让一个脚本定时执行  
crontab
11. 如何设置白名单：特定机器可以给当前机器发消息  
iptable
12. 如何抓包：从远端某机器发送到本机器特定端口  
tcpdump -i eth1 dst port 8080 and src host 1.2.3.4 
13. 一个命令：计算某个bin启动了多少个进程  
ps -ef | grep xxx | grep -v grep | wc -l
14. 遇到错误去哪里看错误日志  
/var/log/mesages   
/var/log/secure
15. log同时输出到终端和文件  
xxx | tee xxx.log
# python
1. 如何定义类私有函数和公有函数  
函数名以__开头即为私有函数，否则为公有函数  
    ```
    class Object:
        def __func1():
            pass
        def func2():
            pass

    ```
2. 构造函数和析构函数是哪两个函数？  
__init\_\_  
__del\_\_
3. 什么是类变量，什么是对象变量  
    ```
    class Object:
        x = 1
        def __init__(self):
            self.y = 1
        
    ```
    在类作用域绑定变量是类变量，使用self绑定变量是对象变量
4. 如何访问类变量  
使用类访问  
使用对象访问
    ```
    class Object:
        x = 1
        def __init__(self):
            self.y = 1
    o = Object()
    print(o.x)
    print(Object.x)
    ```
5. import和from区别  
   - import sys导入整个sys模块，使用sys模块时候如下所示：  
sys.argc, sys.argv  
   - import sys.argc导入sys中argc，使用如下所示：  
sys.argc
   - from sys import argc, argv导入sys中argc和argv，使用如下所
示：  
argc, argv
6. python如何注释
   - #注释单行  
   - 三个单引号包含多行注释
   - 三个双引号包含多行注释
7. 执行一个python脚本有哪几种方式
   - python xxx.py
   - 脚本的第一行添加#! /usr/bin/env python，然后chmod +x 
xxx.py，./xxx.py
8. 如何查询python的所有保留字
import keyword
print(keyword.kwlist)
9. print函数换行吗？如果不换行如何做？
   - print函数默认换行
   - print(123, end="")不换行
10. 如何一行显示多行语句？  
分号隔开
11. 如何修改工作目录  
import os  
os.chdir(xxx)
12. 如何查看一个模块有哪些函数  
import sys  
dir(sys)
13. 如何查看一个模块的简介  
import sys
help(sys)
14. if/else引入作用域吗？
模块、lamda、函数引入作用域，但是if/else, try/except, for/while不会引入新的作用域
15. 如何在函数内修改全局变量的值  
global x   
x = 1
16. 如何修改嵌套作用域的变量值  
nonlocal
17. try/except/else/finally  
    ```
    try:
        #可能异常代码
    except:
        #如果上面代码抛出异常，执行这里
    else:
        #如果上面代码没有抛出异常，执行这里
    finally:
        #不管是否抛出异常，都会执行这里
    ```
18. with关键字作用  
打开文件，使用完后自动关闭
19. python有哪些数组结构  
    - 字典
    - 元组
    - 列表
20. 如何查看所有python搜索路径  
import sys; print(sys.path)
21. 可变对象与不可变对象
a=1; a=2相当于新建一个对象2，而不是把先前对象修改为2, a只是一个引用指向了新的对象  
b = [1, 2, 3]; b[0] = 3， b没有改变，只是修改了b指向的对象
22. python有哪几种标准数据类型
    - 数字
    - 字典
    - 元组
    - 列表
    - 字符串
23. 元组与列表区别  
元组不可修改，列表可修改
# 其它
1. 知道哪些中间件  
redis、kafka、rabbitmq
2. redis用来做什么  
    * 多个进程间共享数据
    * 数据库与进程之间缓存
3. redis为什么比mysql快  
redis基于内存存储，mysql是磁盘存储
4. redis有哪些数据结构  
string、zset、set、list、hash  
5. tcp和udp区别  
    * tcp基于连接，udp基于报文
    * tcp对系统要求资源更多
    * tcp保证数据准确性、顺序性，udp可能丢包
6. http处于tcp/ip协议哪一层？  
应用层
7. 使用python访问tcp服务，使用哪几个api  
socket    
connect  
send  
recv  
8. 有一个服务进程收到请求马上给出回复，连续给此服务发送10条消息，收到的消息是有序的吗？如果没有序如何做到请求和应答一一对应  
tcp收到消息有序，udp可能无序，可以在消息体里面加一个序号，服务进程回复消息时候把请求里面的序号也一并返回
9. 如果给一个服务集群发送消息，服务是tcp的，收到消息有序吗？  
长连接有序因为都是发给的同一个进程，短连接可能无序因为可能发给不同进程
10. 服务为什么都以集群方式提供服务  
    * 避免单点故障
    * 单点能力有限，集群提供更大服务能力
11. 消息队列用来干嘛，举几个使用消息队列例子  
    * 外部请求量太大，服务处理不过来，收到消息先不处理而是放到消息队列，其它服务从消息队列获取消息慢慢处理
12. mysql有哪些引擎  
innodb，myisam
13. 什么场景使用事务，举例子  
把A账户的钱转给B账户
14. mysql主键索引和普通索引有什么区别  
主键索引不能为空
15. mysql底层数据结构是什么  
b+树



    






