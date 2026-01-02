---
date: 2024-03-22T21:50:00
aliases:
  - linux 操作
tags:
  - linux
---
## 根据uid定位user

```bash
ps aux grep [your_PID]
```

## **目录创建**

**mkdir(make directory)** 命令可用来创建子目录。

- mkdir app 在当前目录下创建app目录
- mkdir –p app2/test 级联创建aap2以及test目

**rmdir(remove directory)** 命令可用来删除“空”的子目录：

rmdir app  删除app目录

---

## **浏览文件（cat、more、less）**

**cat** 用于显示文件的内容。格式：

```shell
cat [参数]<文件名>
cat yum.conf
```
`

**more** 一般用于要显示的内容会超过一个画面长度的情况。按空格键显示下一个画面。

回车显示下一行内容。

按 q 键退出查看。

```shell
more yum.conf
```
- 空格显示下一页数据 回车显示下一行的数据

less 用法和more类似，不同的是less可以通过PgUp、PgDn键来控制。
```shell
less yum.conf
```

    
- PgUp 和 PgDn 进行上下翻页.
    

**tail** 命令是在实际使用过程中使用非常多的一个命令，它的功能是：用于显示文件后几行的内容。

用法:
```shell
tail -10 /etc/passwd    查看后10行数据

tail -f catalina.log    动态查看日志(*****)

**ctrl+c** 结束查看
```


---

## **压缩命令**

### **tar**

 **tar命令位于/bin目录下，它能够将用户所指定的文件或目录打包成一个文件，但不做压缩。一般Linux上常用的压缩方式是选用tar将许多文件打包成一个文件，再以gzip压缩命令压缩成xxx.tar.gz(或称为xxx.tgz)的文件。常用参数：**

- c：创建一个新tar文件
- v：显示运行过程的信息
- f：指定文件名
- z：调用gzip压缩命令进行压缩
- t：查看压缩文件的内容
- x：解开tar文件

```shell
tar –cvf xxx.tar ./*    // 打包
tar –zcvf xxx.tar.gz ./*   // 打包并且压缩：

// 解压 
tar –xvf xxx.tar
tar -zxvf xxx.tar.gz -C /usr/aaa
```

**zip**

```shell
zip -r mydata.zip mydata
```

---

## **查找搜索**

**find**

find指令用于查找符合条件的文件

示例：

```bash
find / -name “ins*” 查找文件名称是以ins开头的文件
find / -name “ins*” –ls 
find / –user itcast –ls 查找用户itcast的文件
find / –user itcast –type d –ls 查找用户itcast的目录
find /-perm -777 –type d-ls 查找权限是777的文件
```

**grep**

查找文件里符合条件的字符串。

用法: grep [选项]... PATTERN [FILE]...示例：

```bash
grep lang anaconda-ks.cfg  在文件中查找lang
grep lang anaconda-ks.cfg –color 高亮显示`
```

---

## **系统管理命令**

```bash
ps 正在运行的某个进程的状态

ps –ef  查看所有进程

ps –ef | grep ssh 查找某一进程

kill 2868  杀掉2868编号的进程

kill -9 2868  强制杀死进程
```

---

## **重定向&管道**

> 重定向输出，覆盖原有内容；>> 重定向输出，又追加功能；示例：

```bash
cat /etc/passwd > a.txt  将输出定向到a.txt中
cat /etc/passwd >> a.txt  输出并且追加
ifconfig > ifconfig.txt
```

管道是Linux命令中重要的一个概念，其作用是将一个命令的输出用作另一个命令的输入。示例

```bash
ls --help | more  分页查询帮助信息
ps –ef | grep java  查询名称中包含java的进程
 
ifconfig | more
cat index.html | more
ps –ef | grep aio
```

---

## **权限管理**

![https://cdn.nlark.com/yuque/0/2020/png/2947745/1606197760646-d8d88cbf-8691-4d42-a02d-836a32c48571.png](https://cdn.nlark.com/yuque/0/2020/png/2947745/1606197760646-d8d88cbf-8691-4d42-a02d-836a32c48571.png)

r-4
w-2
x-1
### **文件权限管理：**

**chmod** 变更文件或目录的权限。

```shelll
chmod 755 a.txt chmod u=rwx,g=rx,o=rx a.txt
```
---
## **查看硬盘大小
```bash  
df -h  
```

```bash  
sudo fdisk -l  
```

  
```bash
lsblk
```  
---
### 远程复制文件：

```bash
scp fry@10.21.237.216:/media/T/chenhaoming/Code/DcPose/weights/detector/YOLOv3/yolov3.weights /Users/runyang/Desktop
```

---

## Screen窗口：

```bash
screen -dmS name # creatre 窗口

screen -r id/name # 进入窗口

screen -D id/name # Detach窗口

screen -X -S session_id quit # kill 窗口

nohup python -u train.py &>nohup.out& # 命令调到后台执行，并且输出信息写到nohup.out文件中，这个很有用，操作服务器时本地窗口可以关掉不影响服务器运行
```


## 统计文件数量

```bash
ls -lR | grep "^-" | wc -l
```

## 显卡占用看不到PiD，但是程序卡死

```bash
htop # 直接查找卡死的程序杀掉即可，百度的做法比较繁琐
```

### Net 网络相关

---
```bash
ifconfig -a # 查看ip地址、端口等网络相关信息

**ssh jion@1.tcp.cpolar.cn -p 20279 # ssh远程连接 ssh username@ip -p(端口)
```


