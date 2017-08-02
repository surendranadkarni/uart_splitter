# uart_splitter
Rudimentary Linux tool that allows multiple app to monitor and access uart physical port. This tool is useful while debugging the application that communicates over UART.


Terms:

 - App port: which communicates with other device
 - Sniffer Port: which only listens to incoming and outgoing UART trafic. However, it can not write to device

Topology:
```
                                                                +--------------+
                                                                | AppPort      |
                                            +-------------------+              |
                                            |                   |              |
                                            |                   +--------------+
        +--------------+         +----------+-+                                 
        |              |         | Physical   |                                 
        | Device       +---------+ UART       |                                 
        |              |         |            |                                 
        +--------------+         +---------+--+                  +-------------+
                                           |                     | Listner Port|
                                           |                     |             |
                                           +---------------------+             |
                                                                 |             |
                                                                 +-------------+
```

Usage:

 - the tool acts as simple conveyer for the data from app-port to physical-UART-port.
 - One has to create app-port using socat. Socat will create null modem. one end of null modem will be used by the app that one is debugging and another by the tool.
   for instance, if /dev/ttyS1 is real port then /dev/pts/10 and /dev/pts/11 (say) is null-modem pair then configure your app to use /dev/pts/11 (say) and tool will use /dev/pts/10 (say)
 - One has to recompile the tool when he updates port-configuaion in the file sniffer.c.


