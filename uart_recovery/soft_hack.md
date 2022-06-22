# 软破解打开 telnet
您需要将网关连接到米家APP以获取ip和网关令牌。

### 方法1（推荐）
通过 [XiaomiGateway3](https://github.com/AlexxIT/XiaomiGateway3) 组件。

您必须在“打开 Telnet 命令”字段中输入（**原样，无需更改任何内容**）：
```
{"method":"set_ip_info","params":{"ssid":"\"\"","pswd":"123123 ; passwd -d admin ; echo enable > /sys/class/tty/tty/enable; telnetd"}}
```

### 方法2（如果不使用 Home Assistant，建议使用）
php-miio (https://github.com/skysilver-lab/php-miio)

您可能需要更改 id。
```外壳
php miio-cli.php --ip GW_IP --token GW_TOKEN --sendcmd '{"id":123,"method":"set_ip_info","params":{"ssid":"\"\"","pswd":"123123 ; passwd -d admin ; echo enable > /sys/class/tty/tty/enable; telnetd"}}'
```

### 方法3（序列号可能存在问题）
python-miio (https://github.com/rytilahti/python-miio)
```外壳
miiocli device --ip GW_IP --token GW_TOKEN raw_command set_ip_info '{"ssid":"\"\"","pswd":"123123 ; passwd -d admin ; echo enable > /sys/class/tty/tty/enable; telnetd"}'
```


用户名：admin

密码为空

打开telnet后最好安装自定义固件**（仅适用于小米网关3 mgl03）**。

在这里阅读：
https://github.com/zvldz/mgl03_fw/tree/main/firmware#the-easy-way

**打开 telnet 命令** 也应该适用于：
* lumi.gateway.mgl03 - 小米智能家居中心
* lumi.gateway.acn01 - Aqara Hub M1S CN
* lumi.gateway.aeu01 - Aqara Hub M1S EU
* lumi.aircondition.acn05 - Aqara 空调控制器 P3
* lumi.gateway.sacn01 - 智能 USB 墙壁插座集线器

# Aqara Hub E1 (ZHWG16LM usb stick)
您需要将网关 E1 连接到米家APP以获取ip和网关令牌。

### 方法1（推荐）
通过 [XiaomiGateway3](https://github.com/AlexxIT/XiaomiGateway3) 组件，版本 2+。

您必须在“打开 Telnet 命令”字段中输入（**原样，无需更改任何内容**）：
```
{"method":"set_ip_info","params":{"ssid":"\"\"","pswd":"123123 ; /bin/riu_w 101e 53 3012; telnetd"}}
```

### 方法2（如果不使用 Home Assistant，建议使用）
php-miio (https://github.com/skysilver-lab/php-miio)

您可能需要更改 id。
```外壳
php miio-cli.php --ip GW_IP --token GW_TOKEN --sendcmd '{"id":123,"method":"set_ip_info","params":{"ssid":"\"\""," pswd":"123123 ; /bin/riu_w 101e 53 3012; telnetd"}}'
```

### 方法3（序列号可能存在问题）
python-miio (https://github.com/rytilahti/python-miio)
```外壳
miiocli 设备 --ip GW_IP --token GW_TOKEN raw_command set_ip_info '{"ssid":"\"\"","pswd":"123123 ; /bin/riu_w 101e 53 3012 ; telnetd"}'
```

登录：root

密码为空



***我不是作者，我只是测试、改进和发表。***



[在 Aqara G3 hub 上启用 telnet](https://github.com/Wh1terat/aQRootG3)
