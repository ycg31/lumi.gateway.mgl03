## 通过 UART 将固件刷入小米网关 v3。
如果您只需要在官方固件上打开 telnet，请使用“软件”方法：
https://gist.github.com/zvldz/1bd6b21539f84339c218f9427e022709

＃＃＃ 硬件

1.打开网关外壳：

   <img src=https://user-images.githubusercontent.com/511909/98269111-6da8b980-1f9e-11eb-82ef-d435a900edf1.jpg>

2.连接UART：
   UART Tx <--> TP4（网关 Rx）
   UART Rx <--> TP11（网关 Tx）
   UART GND <--> TP8 (网关 GND)

   <img src="https://user-images.githubusercontent.com/511909/98268507-a8f6b880-1f9d-11eb-80f6-3ae2bee27c5e.png" width="640">
   
   如果您损坏了 UART 引脚，电路板背面还有备用 UART：
   
   <img src="https://raw.githubusercontent.com/serrj-sv/lumi.gateway.mgl03/main/media/mgl03_back_uart_eth.jpg" width="640">

    关于 UART 的重要说明：
    * UART 适配器必须处于 3.3V 模式。网关无法承受 5v电压。
    * 不要将VCC通过UART供电到主板，请使用外部电源从micro-usb口供电。
    * 请勿触摸任何其他测试点（如 TP16、TP17 等），这不是必需的。
1.如果您对焊接感到不舒服或没有信心-购买“pcb pogo clip”（例如：[Aliexpress]（https://www.aliexpress.com/item/4001015704531.html），选择“2.54MM 3P Single")

### 文件
1. 以您选择的速度从 [bootloader](https://github.com/serrj-sv/lumi.gateway.mgl03/tree/main/uart_recovery/bootloader) 文件夹下载中间引导加载程序：
    * [rtkboot_38400.bin](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/bootloader/rtkboot_38400.bin) 是最慢且最可靠的（上传固件需要一些时间超过 1 小时）。
    * [rtkboot_57600.bin](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/bootloader/rtkboot_57600.bin) 比 rtkboot_38400.bin 快一点
    * [**rtkboot_115200.bin**](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/bootloader/rtkboot_115200.bin)（推荐）是速度和可靠性的最佳折衷选择（上传固件大约需要 20 分钟）。
    * [rtkboot_230400.bin](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/bootloader/rtkboot_230400.bin) 比 rtkboot_115200.bin 快一点
    * [rtkboot_460800.bin](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/bootloader/rtkboot_460800.bin) 是最快的（上传固件大约需要 6 分钟）。
1.从您选择的[固件文件夹]（https://github.com/zvldz/mgl03_fw/tree/main/firmware）下载mgl03_xxxxx.uart文件。

### Windows
1.下载[mgl03_uart_recovery.ttl](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/mgl03_uart_recovery.ttl)
2.下载安装【Tera Term】(https://ttssh2.osdn.jp/index.html.en)
3. 运行 Tera Term
4.选择“串口->COM口”，OK
5.选择“控制->宏”
6.打开您在步骤[1]中下载的.mgl03_uart_recovery.ttl文件
7. 按照屏幕上的说明进行操作
8. 执行恢复出厂设置：网关完全启动后，重复按按钮10次。

### Linux（[@CODERUS](https://github.com/coderus)）
1.下载[mgl03_uart_recovery.expect](https://github.com/serrj-sv/lumi.gateway.mgl03/raw/main/uart_recovery/mgl03_uart_recovery.expect)
1.确保安装了以下程序：
  * expect
  * sx（来自包 lrzsz）
  * stty
1.确保引导加载程序（rtkboot_xxxx.bin）、固件（mgl03_xxxxxx.uart）和mgl03_uart_recovery.expect在同一个文件夹中
2.确保你在“dialout”组
3.运行：
   ```
   chmod +x mgl03_uart_recovery.expect
   ./mgl03_uart_recovery.expect
   ```
4. 按照屏幕上的说明进行操作
5. 执行恢复出厂设置：网关完全启动后，重复点击它的按钮 10 次。
 
 ＃＃＃ 故障排除
 #### 如果出现问题，请检查以下内容：
1. 用酒精清洁焊接区域，污垢和助焊剂残留可能导致短路（参见：[issue 87](https://github.com/AlexxIT/XiaomiGateway3/issues/87#issuecomment-754325553)）
2.确保你UART正确连接，唯一正确的方法是Tx到Rx，反之亦然（而不是Tx到Tx和Rx到Rx）：（参见[问题18]（https://github.com/serrj -sv/lumi.gateway.mgl03/issues/18))：
   ```
   UART Tx -> MGL03 Rx
   UART Rx -> MGL03 Tx
   UART GND -> MGL03 GND
   ```
1. 确保您知道如何在 GitHub 上下载文件（参见 [问题 1](https://github.com/serrj-sv/lumi.gateway.mgl03/issues/1)）：
   1. 不要对文件名执行“右键单击并‘另存为’”，而是：
   2.首先点击您要下载的文件，然后点击“下载”按钮
