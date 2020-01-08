# samba
## 安装
- sudo apt-get install samba samba-common-bin

## 创建共享目录并赋予权限
- mkdir /home/pi/share
- sudo chmod 777 /home/pi/share

## 配置conf文件
- sudo vim /etc/samba/smb.conf
```
#在最后添加配置内容
[share]
   path = /home/pi/share
   valid users = pi
   browseable = yes
   public = yes
   writable = yes
   guest ok = yes
   read only = no
```
## 重启samba
- sudo /etc/init.d/samba restart
- sudo samba restart    


Job for samba-ad-dc.service failed because the control process exited with error code.




# aria2
### 强大的下载软件，支持BT下载，通过web控制台控制
## 安装
- sudo apt-get install aria2

## 配置aria2
- sudo mkdir /etc/aria2
- sudo touch /etc/aria2/aria2.session
- sudo vim /etc/aria2/aria2.conf

```
# dir=/data/download         
#下载文件保存目录,建议挂载移动硬盘，SD卡经不住这么玩儿
 
#因为我们是以 pi 用户执行的aria2c 进程，所以这里此目录的读写权限
# sudo chown -R pi:pi /data/download
#打开rpc的目的是为了给web管理端用 
#configuration file for aria2c
enable-rpc=true
rpc-allow-origin-all=true
rpc-listen-all=true
 
#rpc-listen-port=6800
file-allocation=none
disable-ipv6=true
disk-cache=32M
split=3
max-concurrent-downloads=3
max-connection-per-server=3
max-file-not-found=3
max-tries=5
retry-wait=3
continue=true
check-integrity=true
log-level=error
log=/var/log/aria2.log
 
input-file=/etc/aria2/aria2.session
save-session=/etc/aria2/aria2.session
 
dir=/data/download
```

- sudo aria2c --conf-path=/etc/aria2/aria2.conf (测试是否有问题）
- sudo vim /etc/rc.locl （在此文件中写入sudo aria2c --conf-path=/etc/aria2/aria2.conf -D 实现开机启动）

## 安装apache(通过web节目远程下载）
- sudo apt-get install apache2
- 在浏览器输入IP地址，若出现默认界面则成功
- git clone https://github.com/ziahamza/webui-
- 将整个目录文件移到/var/www/html文件夹下
- sudo mv -rf webui-aria2 /var/www/html
- 在浏览器输入IP即可打开aria2管理web界面
 
