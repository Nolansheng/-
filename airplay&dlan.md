# airplay
## 安装一系列依赖模块
1. sudo apt-get install libao-dev libssl-dev libcrypt-openssl-perl libio-socket-inet6-perl libwww-perl avahi-untils libmodule-build-perl

## 安装perl net-sdp
1. git clone https://github.com/njh/perl-net-sdp.git perl-net-sdp
2. cd perl-net-sdp
3. perl Build.PL
4. sudo ./Build
5. sudo ./Build test
6. sudo ./Build install

## 安装shairport
1. git clone https://github.com/abrasive/shairport.git
2. cd shairport
3. make
4. ./shairport -a RaspberryPi 测试是否生效（ctrl-c 退出）
5. sudo make install

设置开机启动
```
sudo cp /home/pi/shairport/scripts/debian/init.d/shairport /etc/init.d/shairport
sudo cp /home/pi/shairport/scripts/debian/default/shairport /etc/default/shairport
sudo chmod +x /etc/init.d/shairport
sudo chmod +x /etc/default/shairport
sudo update-rc.d shairport defaults
```
# dlna
## 安装
```
sudo apt-get install minidlna
sudo vim /etc/minidlna.conf

A表示这个目录是存放音乐的，当minidlna读到配置文件时，它会自动加载这个目录下的音乐文件
media_dir=A,/samba/DLNA/Music
media_dir=P,/samba/DLNA/Picture
media_dir=V,/samba/DLNA/Video
配置minidlna的数库数据的存放目录
db_dir=/samba/DLNA/db
配置日志目录
log_dir=/samba/DLNA/log

重启
/etc/init.d/minidlna restart

查看状态
/etc/init.d/minidlna status

随机启动
sudo update-rc.d minidlna defaults

卸载
sudo apt-get remove --purge minidlna
可在 网页 IP:8200查看

```
