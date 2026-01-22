#
## CentOS7 
yum 配置其他源
```
# 备份所有现有repo文件
mkdir /tmp/yum-backup
cp /etc/yum.repos.d/*.repo /tmp/yum-backup/

# 删除所有现有的repo文件（CentOS 7默认配置）
rm -f /etc/yum.repos.d/*.repo
```

## Alpine
```
cp /etc/apk/repositories /etc/apk/repositories.bak
vi /etc/apk/repositories
```
https://mirrors.aliyun.com/alpine/<version>/main
https://mirrors.aliyun.com/alpine/<version>/community