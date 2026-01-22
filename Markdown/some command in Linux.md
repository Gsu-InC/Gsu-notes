# Linux系统学习日记
## 指令
### ls
1. ls 列出当前目录下所有文件
2. ls -l 列出当前目录下所有文件的属性 大部分系统可以简写为ll
3. ls -a 列出所有文件包括隐藏文件
4. ls -la 列出所有文件(包括隐藏文件)和属性
5. ls -lh 让文件属性以更可读的形式列出
6. ls -lh + 路径 读取对应路径的......
### cd
1. cd + 文件名 
2. cd .. 进入上一层目录
3. cd . 进入当前目录
4. cd ../.. 进入上层目录的上层目录
5. cd - 回到刚才所在的目录
6. cd ~ 切换到home目录
### pwd (print working directery) 打印当前路径
### cat 文件内容 
### head
1. head + 文件名 看文件开头
2. head --lines=n + 文件名 看文件前n行
### tail
- tail --lines=n + 文件名 看尾部n行
- tail -f 显示末尾十行并持续更新
不写-lines默认看10行
### less
- less + 文件名 阅读全文 可以用键盘上下键阅读 按q退出
### more
- more + 文件名 阅读全文 只能往下翻
### nano
nano + 文件名 进入编辑器
### vim
- vi或vim + 文件名
- 按i键 进入编辑模式 insert
- 退出 
- 1. 先按Esc(或者 Ctrl + "["键)退出编辑模式(iPad上的iSH被我改成了左上角波浪键)
- 2. q！ 强制退出
- 2. wq 写了之后保存退出
### file  看文件属性
### where 找文件路径 可能是 which 或者 whereis 
which 查找程序
### find 
find 起始路径(从哪里开始找) -name "被查找的文件名"
find 起始路径(从哪里开始找) -size 大小
k M G ......
```
find / -size -10k 从根目录开始找小于10kb的文件 注意k是小写
find / -size +100M 从根目录开始找大于100M的文件
```
### echo 回声，返回你发的东西
### rm -rf / 
rm 支持通配符*做模糊匹配
eg：test* 删除text结尾的文件
<font color = "red"> 删光文件 </font>

### grep
从文件中通过关键字过滤文件
找到==有关键字==的文本的行数
grep [-n] 关键字 文件路径 关键词如果有空格等特殊符号用""把文件包起来

### wc
统计文件
wc [-c -m -l -w] 文件路径
-c,统计bytes数量
-m,统计字符数量
-l,统计行数
-w,统计单词数

不写选项返回 行数 单词数 字节数 文件名

### 管道符 |
管道符将左边命令的结果作为右边命令的输入

eg：cat file | grep "" 此时grep把cat的结果作为输入，不用写路径

### 漂号 `
被漂号包围的内容会被作为命令来执行

### 重定向符
```
> 将左边的结果覆盖写入到右边指定的文件
>> 将左边的结果追加写入到右边指定的文件
```
### 复制
cp [-r] 参数1(被复制的文件或文件夹路径) 参数2(复制到的路径) -r 代表递归，在复制文件夹时使用

### 剪切
mv 参数1 参数2 

## 脚本编程
- 定义变量
```
h="hello"
echo $h  //使用要加上$符号
h = "hellox"
echo "abc$h" //输出 abchellox
echo "abc${h}efg" //用花括号括住变量防止歧义  输出abchelloxefg
echo "abc$hefg" // 只输出前面部分abc
```
- 改文件名 
```
mv week01 chapter01 //把week01改成chapter01 mv:move
```
- for循环
```
for ff in week?? // week* 以week开头的文件 week?? 以week开头后面有2个字符的文件(有点像SQL语句) ff变量名，随便起的
do
//执行的命令
done
${ff#week} // 把开头的week给去掉(文件中有 week01 week02等)
mv $ff chapter${ff#week} //  把week开头改成chapter开头 去尾是% 如ff%week
```
<font color = "red">注意无法撤销，只能手动调回去，所以要注意做好备份，执行操作前先echo看看有没有问题 </font>

## 快捷键 
1. 按住Tab键自动补齐
2. 上下键 返回过去输过的命令

## 写语言
### 创建
- 文件夹 mkdir + 文件夹名
- 文件夹 makdir -p +路径 创建多层级的连续体系
- 文件 touch + 文件夹名
- vi  指令进入
## 编译
- 编译器 + 源码名 -o 文件名.exe
- ./文件名.exe  备注：在当前文件目录下执行程序



alpine 安装基础工具包：apk add coreutils

## 切换用户
su - 用户名 切换用户

## root
su - root 输入密码切换root
su 输入密码进入root
sudo -i 输入密码会出问题
sudo password root 重设密码
输入exit 退出root

### 临时为命令授权 sudo 需要为普通用户配置认证

#### 配置
```
visudo # 自动通过vi编辑器打开:/etc/sudoers
# 在文件最后添加 
用户名 ALL=(ALL)    NOPASSWD: ALL #注意中间的空格是一个tab的距离
```

>配置后可以sudo su - root 无需输密码直接进入管理员模式

## 用户和用户组
groupadd 用户组名    创建用户组

groupdel 用户组名    删除用户组

- useradd [-g -d] 用户名
-g 指定加入的用户组，不-g则创建一个同名的用户组自动把这个用户放到组内 如果存在同名组则报错
-d 指定home路径，不指定，home默认在：/home/用户名

- userdel [-r] 用户名
-r 删除用户的home目录，不使用-r则不删除

- id [用户名]
如果不写用户名则查看自身

- usermod -aG 用户组 用户名
将指定用户加入指定用户组

- getent passwd 查看有哪些用户
用户名 密码 用户ID 组ID 描述信息
- getent group 查看有那些组
组名称 组认证 组ID

## 权限
|:---:|:---:|:---:|
|r=4|w=2|x=1|
常用权限值 755 644


```
权限 所属用户 所属用户组 
drwxr-xr-x. 2 gsu gsu  6 Jan 20 04:00 Desktop
```
### 权限细节
10个槽位 文件属性+所属用户权限+所属用户组权限+其他用户权限
1. -表示文件 d表示文件夹 l表示软链接
2. -表示无权限
- r 读权限 
- w 写权限
- x 执行权限(execute) 可以把文件作为程序去执行 可以cd进入文件夹

### 修改权限


- chmod 命令修改权限 
只有所属用户或root用户可修改

chmod [-R] 权限 文件或文件夹 
-R：对文件夹内全部内容应用同样的操作
e.g:
```
chmod u=rwg,g=rx,o=x hello.txt

chmod 751 hello.txt
```
u 表示user权限，g 表示group权限，o 表示other权限

### 修改权限控制
- chown
修改所属用户和用户主
chown [-R] [用户][:][用户组] 文件或文件夹
-R 同chmod

e.g:
```
chown root 1.txt 将1.txt所属用户修改为root
chown :root 1.txt 将1.txt所属用户组修改为root 
```
## 快捷键
- 强制停止程序的运行或退出当前命令输入 ctrl + c
- 退出登录或者退出某些页面 ctrl + d !不能退vi/vim
- 搜索历史命令 history
- ！ + 之前执行过的命令开头 自动执行之前执行过的命令 不建议
- ctrl + r 输入内容去匹配历史命令 ehter直接执行 按键盘左右键可得到此命令
- ctrl + a 跳到命令开头
- ctrl + e 跳到命令结尾
- ctrl + 键盘左键 向左跳一个单词
- ctrl + 键盘右键 向右跳一个单词
- ctrl + l 清空终端内容 等于clear指令

## 软件安装
>CentOS
### yum
程序后缀.rpm
yum 需要root权限 需要联网
yum [-y] [install | remove |search] 软件名称
- -y 自动确认无需手动确认或安装
- install 安装
- remove 卸载
- search 搜索 

>Ubuntu
.deb
apt 

### systemctl
systemctl start | stop | status | enable | disable + 服务 
enable disable 控制是否开机自启


### ping 
检查指定的网络服务器是否可联通
ping www.baidu.com 检查无数次
ping -c 4 www.baidu.com 检查3次
### wget程序
wget [-b] url
-b 后台下载
### curl 
用于获取信息或下载文件
curl [-O] url
选项-O 用于下载文件 不下载就不用 -O

### 软链接
类似于快捷方式
语法： ln -s parameter1 parameter2 
-s 创建软链接
参数1  被链接的文件或文件夹
参数2 链接去的地方

### 时间和时区
#### 查时间
date [-d] [+格式化字符串]

-d
date -d "+1 day" 显示明天日期
格式化字符串
- %Y 年
- %y 年份后两位数字
- %m 月份
- %d 日
- %H 小时
- %M 分钟
- %S 秒数
- %s 自1970-01-01 00：00：00 到现在的时间

应用ntp自动查时间

## 特殊ip
127.0.0.1 表示本机ip

0.0.0.0 
- 可以指代本机
- 可以在端口绑定中确定绑定关系
- 可以表示对任意ip放行

## 主机名
hostname 查看主机名
hostnamectl set-hostname 主机名 修改主机名

## 为Linux系统设置静态IP
修改配置文件
使用vim编辑/etc/sysconfig/network-scripts/ifcfg-ens33文件
修改：
BOOTPROTO = "static" 或者改为"none" 由dhcp改为static动态改为静态
追加：
IPADDR="" 你的IP地址
NETMASK="255.255.255.0" 子网掩码固定
GATEWAY="" 你的虚拟机的网关
DNS1="114.114.114.114" 域名解析服务器1,填入中国电信的DNS
DNS2="8.8.8.8" google's DNS 

## Linux中的端口
公认端口 1~1023 为系统或知名程序预留 如SSH服务的22端口，HTTPS服务的443端口
注册端口 1024~49151 通常可以随意使用，用于松散的绑定程序或服务
动态端口 49152~65535 通常不会固定绑定程序，而是对外链接时临时使用
- nmap
安装 yum -y install nmap
语法 nmap + 被查看的IP地址 查看被使用的端口
- netstat 
安装 yum -y install net-tools
语法 netstat-anp|grep 端口号 查看指定端口占用情况

## Linux的进程管理
- 查看进程
ps [-e -f]

-e 显示出全部的进程
-f 展示全部信息
一般用法：ps -ef 
配合管道符过滤 ps -ef | grep 

- 关闭进程
kill [-9] 进程ID
-9选项 强制关闭进程

- 查看系统资源占用 
top 进入资源占用界面
top中按H键 进入帮助界面 按Q退出
F 控制展示那些列
M 按内存排序
P 按cpu排序
T 按时间
E 上方字典切换内存单位
I 切换是否显示无用进程

- 查看磁盘信息
df 
df -h 改变单位，让单位显示更好看

iostat[-x][num1][num2]
-x 显示更多信息
num1 ：刷新间隔
num2 ：刷新次数

- 网络监控
sar
固定写法 sar -n DEV num1 num2


## 设置环境变量
环境变量 KeyValue型 用于操作系统运行时记录关键信息


- 临时
export 变量名=变量值

- 永久
1. 针对当前用户生效：
```
vi ~/.bashrc
写入 export 变量名=变量值
退出
source .bashrc
这样就在当前用户环境永久生效
```

2. 全局环境变量
```
vim etc/profile
写入 /export 变量名=变量值
退出
source /etc/profile
```

e.g:添加新的变量到PATH
```
vim etc/profile
export PATH=$PATH:(/root/myenv)换成你的路径 
```
注意一定要写&PATH把原有的路径带上


## finalshell文件传输

图形化直接拖
rz,sz

yum -y install lrzsz

## 压缩或解压
格式 zip tar gzip

### tar 命令
1. .tar 只是简单的封装，体积没有太多压缩




2. .gz 文件体积压缩


tar [-c -v -x -f -z -C] 参数1 参数2 参数3......参数n
-c 创建压缩文件
-v 显示压缩、解压过程用于查看进度
-x 解压模式
-f 要创建的文件或被解压的文件 -f在所有选项中一定排在最后一个
-z gzip模式 不使用就是tarball 使用时一般在选项第一个
-C 选择解压的目的地，用于解压组合

常用选项：
tar -cvf + 文件们
tar -zcvf + 文件们

tar -xvf test.tar 解压到当前目录
tar -xvf test.tar -C /home/gsu  解压到指定路径/home/gsu
tar -zxvf test.tar.gz

### zip压缩文件
.zip
- 压缩：
zip [-r] 参数1 参数2 ......
-r 有文件夹时写-r

- 解压：
unzip [-d] 参数
-d 后面跟路径指定路径
```
unzip test.zip -d home/gsu 如果解压时有同名内容会替换原来的内容
建议到空文件夹里解压
```
