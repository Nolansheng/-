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

- 配置文件解释
```
# 4种日志模式：stdout、stderr、syslog、topic
# none 则表示不记日志，此配置可以提升些许性能
log_dest none

# 选择日志的级别（可设置多项）
#log_type error
#log_type warning
#log_type notice
#log_type information

# 是否记录客户端连接信息
#connection_messages true

# 是否记录日志时间
#log_timestamp true
```
- 默认端口1883.地址为IP地址


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
  
  5. 命令解释
  ```
  例"mosquitto_sub -t -v sensor"开启一个终端用于订阅消息
  -d 打印debug消息
  -h 指定域名
  
 
