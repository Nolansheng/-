# 在树莓派安装MQTT代理“mosquitto"
1. 安装最新版本的mosquitto
```
sudo wget https://repo.mosquitto.org/debian/mosquitto-repo.gpg.key
sudo apt-key add mosquitto-repo.gpg.key
cd /etc/apt/sources.list.d/
sudo wget http://repo.mosquitto.org/debian/mosquitto-stretch.list
sudo apt-get update
sudo apt-get install mosquitto
```
2. 安装mosquitto的另外三个部分
- mosquitto- the MQTT broker(or in other words a server)
- mosquitto-clients-command line clients, very useful in debugging
- paho-mqtt the python language bindings
```
sudo apt-get install mosquitto mosquitto-clients
sudo apt-get install python-pip	
sudo pip install paho-mqtt
```

3. 先停止服务，更改配置信息
```
sudo /etc/init.d/mosquitto stop
sudo vim /etc/mosquitto/mosquitto.conf
```
- 文件应当如下
```
# Place your local configuration in /etc/mosquitto/conf.d/
#
# A full description of the configuration file is at
# /usr/share/doc/mosquitto/examples/mosquitto.conf.example
 
pid_file /var/run/mosquitto.pid
 
persistence true
persistence_location /var/lib/mosquitto/
 
log_dest topic
 
 
log_type error
log_type warning
log_type notice
log_type information
 
connection_messages true
log_timestamp true
 
include_dir /etc/mosquitto/conf.d
```




4. 重启服务
```
sudo /etc/init.d/mosquitto start
```

5. 测试服务
  - 打开两个终端窗口
  - 在终端1中输入：
  ```
  mosuitto_sub -d -t hello/world
  ```
  - 在终端2中输入：
  ```
  mosquitto_pub -d -t hello/world -m "hello from terminal window2"
  
 
