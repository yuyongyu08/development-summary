# UDP

**用户数据报协议**（User Datagram Protocol）

<table><thead><tr><th width="144.33333333333331"></th><th>UDP</th><th>TCP</th></tr></thead><tbody><tr><td>是否连接</td><td>无连接</td><td>面向连接</td></tr><tr><td>是否可靠</td><td>不可靠传输，不使用<strong>流量控制</strong>和<strong>拥塞控制</strong></td><td>可靠传输，使用流量控制和拥塞控制</td></tr><tr><td>连接对象个数</td><td>支持一对一，一对多，多对一和多对多交互通信</td><td>只能是一对一通信</td></tr><tr><td>传输方式</td><td>面向<strong>报文</strong></td><td>面向<strong>字节流</strong></td></tr><tr><td>首部开销</td><td>首部开销小，仅8字节</td><td>首部最小20字节，最大60字节</td></tr><tr><td>适用场景</td><td>适用于<strong>实时性高</strong>应用（IP电话、视频会议、直播等）</td><td>适用于要求<strong>可靠传输</strong>的应用（文件传输）</td></tr></tbody></table>



参考：

* [https://juejin.cn/post/6844903800336023560](https://juejin.cn/post/6844903800336023560)
