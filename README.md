# uart_splitter
Linux service that allows multiple app to monitor and access uart physical port


Term:

    App port: which communicates with other device
    Sniffer Port: which only listens and can not write to device

Topology:
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

- first create NULL modem using socat for app port. repeate same for listner port
    socat -d -d pty,raw,echo=0 pty,raw,echo=0
- Compile the code by updating /dev/pts/n in file sniffer.c


