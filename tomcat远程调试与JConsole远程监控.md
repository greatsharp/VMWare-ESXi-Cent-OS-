JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=2345 -Dcom.sun.management.jmxremote.port=2346 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Djava.rmi.server.hostname=172.18.42.129"

如上所配置，2345是用来remote debug的端口。 2346是JConsole用来远程监控的端口

![](https://github.com/greatsharp/VMWare-ESXi-Cent-OS-/blob/master/images/JConsole_remote.png)
