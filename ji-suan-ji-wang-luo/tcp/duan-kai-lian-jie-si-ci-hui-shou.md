# 断开连接（四次挥手）



<figure><img src="../../../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>



**为什么要四次握手？**

TCP连接是**全双工**的（数据在两个方向能同时传输），同时TCP支持**半关闭**（发送一方结束发送数据还能接收数据），所以每个方向都要单独关闭，且需要在收到关闭通知后回复确认
