#  TcpIp 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIp|
|描述|Configuration of the TcpIp (TCP/IP stack) module.|
|描述|概述：TcpIp配置项是以太通信协议栈的一部分，它定义了TCP/IP协议栈的参数，包括IP地址、子网掩码、默认网关等，以实现网络通信功能。|
|描述|注意：在配置TcpIp模块时，需要确保IP地址的唯一性和正确性，避免网络冲突；子网掩码应正确配置以确保网络分割的正确性。|
|多实例个数|0 - 1|

## 1. TcpIpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpConfig|
|描述|This container contains the configuration parameters and sub containers of TcpIp module.|
|描述|概述：TcpIpConfig 用于配置TCP/IP协议栈的参数，包括IP地址、子网掩码、默认网关等网络相关的各种协议和服务的设置。|
|描述|注意：在配置TcpIpConfig时，需要确保IP地址分配不会与网络中的其他设备冲突；子网掩码应正确反映网络的拓扑结构。|
|多实例个数|1 - 1|

### 1.1. TcpIpBufferMemoryConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpBufferMemoryConfig|
|描述|Specifies the EthIf controller used for IP communication.|
|描述|概述：TcpIpBufferMemoryConfig 是用于配置TCP/IP协议栈中用于存储网络数据的缓冲区内存的参数，包括缓冲区的大小和数量。|
|描述|注意：在配置TcpIpBufferMemoryConfig时，需要确保为网络通信预留足够的缓冲区内存，以避免数据丢失或通信延迟；同时，过多的缓冲区分配可能会导致系统资源的浪费。|
|多实例个数|1 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpBufferMemoryLen|
|描述|Specifies the default value for the priority for all outgoing frames.|
|描述|概述：TcpIpBufferMemoryLen定义了TCP/IP协议栈用于存储网络数据的缓冲区大小，这个参数直接影响到网络通信的效率和稳定性。|
|描述|注意：缓冲区大小需要根据实际网络通信量和系统资源合理配置，过小可能导致数据丢失，过大可能浪费系统资源；调整此参数时，应考虑系统的最大网络负载和并发连接数。|
|说明|该值可以通过 TcpIp_ChangeParameter() 服务为每个套接字单独修改。如果未提供该可选参数，则默认优先级为 0。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpBufferMemoryNum|
|描述|Specifies the default value for the priority for all outgoing frames.|
|描述|概述：TcpIpBufferMemoryNum 是一个配置参数，用于指定TCP/IP协议栈中用于存储网络数据的特定长度缓冲区数量。|
|描述|注意：在配置TcpIpBufferMemoryNum时，需要确保分配的缓冲区数量能够满足系统的网络通信需求；过多的缓冲区可能会导致系统资源的浪费，而过少则可能导致网络通信的延迟或丢包；此外，该参数的配置应考虑到系统的内存资源限制和预期的网络负载。|
|说明|该值可通过 TcpIp_ChangeParameter() 服务为每个套接字单独修改。如果未提供该可选参数，则默认优先级为 0。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 65535|

### 1.2. TcpIpCtrl

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpCtrl|
|描述|Specifies the EthIf controller used for IP communication.|
|描述|概述：TcpIpCtrl配置项用于定义TCP/IP协议栈的控制器属性，包括但不限于IP地址配置、子网掩码、默认网关等网络参数，以实现网络通信的基本要求。|
|描述|注意：在配置TcpIpCtrl时，必须确保IP地址的唯一性和正确性，避免网络冲突；子网掩码和默认网关的配置应符合实际网络架构要求。|
|多实例个数|1 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpFramePrioDefault|
|描述|Specifies the default value for the priority for all outgoing frames.|
|描述|概述：TcpIpIpFramePrioDefault配置项用于定义TCP/IP协议栈中，发送IP帧时默认使用的网络优先级。|
|描述|注意：该配置项的值应当符合网络的QoS（Quality of Service）要求；在不同网络环境下，可能需要调整该值以优化网络性能。|
|说明|该值可以通过 TcpIp_ChangeParameter() 服务针对每个套接字单独修改。如果未提供此可选参数，则默认优先级为 0。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 7|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpEthIfCtrlRef|
|描述|Reference to EthIf controller where the IP address shall be assigned.|
|描述|概述：TcpIpEthIfCtrlRef 是一个配置参考，它指定了TCP/IP协议栈与特定的以太网接口控制器之间的关联。|
|描述|注意：在配置TcpIpEthIfCtrlRef时，必须确保引用的以太网接口控制器已经在系统中定义并且是有效的；此配置项是实现网络通信的关键，错误的配置可能导致网络通信失败。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfController|

### 1.3. TcpIpIpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpConfig|
|描述|Specifies the configuration parameters of the IP (Internet Protocol) sub-module|
|描述|概述：TcpIpIpConfig配置项用于定义TCP/IP协议栈的IP相关配置，包括IPV4的配置和IPV6的配置（如果支持）。|
|描述|注意：当前不支持IPV6，无需配置IPV6的功能，只需配置IPV4相关的ICMP，分片和ARP配置。|
|多实例个数|0 - 1|

#### 1.3.1. TcpIpIpV4Config

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpV4Config|
|描述|Specifies the configuration parameters of the IPv4 (Internet Protocol version 4) sub-module.|
|描述|概述：TcpIpIpV4Config配置项用于定义TCP/IP协议栈中IPv4的相关配置，包括ICMPv4，IPv4分片重组，ARP配置。|
|描述|注意：当前不支持IPV6，无需配置IPV6的功能，只需配置IPV4相关的ICMP，分片和ARP配置。|
|多实例个数|0 - 1|

##### 1.3.1.1. TcpIpArpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpArpConfig|
|描述|Specifies the configuration parameters of the ARP (Address Resolution Protocol) sub-module.|
|描述|概述：TcpIpArpConfig配置项用于定义TCP/IP协议栈中ARP（地址解析协议）的相关参数，包括ARP表的大小、ARP条目的生命周期等，以支持网络通信中的IP地址到物理地址的映射。|
|描述|注意：在配置TcpIpArpConfig时，需要确保ARP表的大小与网络环境相匹配，避免因表过小而频繁更新；ARP条目的生命周期应根据网络稳定性合理设置，以减少网络通信延迟。|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpArpPacketQueueEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of the ARP Packet Queue according to IETF RFC 1122, section 2.3.2.2.|
|描述|概述：TcpIpArpPacketQueueEnabled配置项用于启用或禁用在等待ARP响应时对IP数据包的队列处理功能，以控制在ARP解析过程中数据包的处理方式。|
|描述|注意：在启用此功能时，系统将会缓存等待ARP响应的IP数据包，直到收到响应或超时；禁用此功能可能导致在ARP解析期间发送的数据包丢失；此配置项对网络性能和资源利用率有直接影响，应根据实际网络条件和应用需求谨慎配置。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpArpPacketQueueLength|
|描述|The maximum number of packets which may be queued for each unresolved address by other network layers.|
|描述|概述：用于指定ARP（地址解析协议）中每个目标IP地址的队列长度。这队列用于暂存待发送的数据包。|
|描述|注意：默认值为3。所有ARP表项数量之和不能超过MEMP_NUM_ARP_QUEUE，否则内存不足。当队列满时，旧的数据包会被丢弃，新数据包则会进入队列。|
|多实例个数|0 - 1|
|取值范围|1 - 30|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpArpRequestTimeout|
|描述|Specifies a timeout in seconds for the validity of ARP requests. After the transmission of an ARP request the TcpIp shall skip the transmission of any further ARP requests to the same destination within a duration of TcpIpArpRequestTimeout seconds. (IETF RFC 1122, section 2.3.2.1) The value for this parameter shall be an integral multiple of TcpIpMainFunctionPeriod or 0. If this parameter set to 0 this features is disabled and no delay between ARP requests is enforced.|
|描述|概述：TcpIpArpRequestTimeout 配置项用于定义发送ARP（地址解析协议）请求后等待ARP响应的超时时间，这个时间值决定了系统在重新发送ARP请求前将等待多久。|
|描述|注意：该值应当根据网络的具体延迟和负载情况进行调整，以避免不必要的网络流量或连接延迟；超时时间设置过短可能导致ARP请求频繁重发，增加网络负担；设置过长可能导致网络响应缓慢，影响通信效率。|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpArpTableEntryTimeout|
|描述|Timeout in seconds after which an unused ARP entry is removed.|
|描述|概述：TcpIpArpTableEntryTimeout 配置项定义了在ARP（地址解析协议）表中一个条目在没有被刷新的情况下可以保持的最大时间，超过这个时间后，该条目会从ARP表中移除。|
|描述|注意：该值需要根据网络的具体情况进行调整，以避免因为过快的移除有效的ARP条目而导致不必要的网络流量；同时，设置过长的超时时间可能会导致ARP表中保留过时的无效条目，影响网络性能。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpArpNumGratuitousARPonStartup|
|描述|Specifies the number of gratuitous ARP replies which shall be sent on assignment of a new IP address.|
|描述|概述：TcpIpArpNumGratuitousARPonStartup 配置项定义了在网络启动时发送的免费ARP（Gratuitous ARP）消息的数量，用于更新其他网络节点上的ARP缓存，以通知它们本节点的IP地址映射。|
|描述|注意：该值应根据网络的具体需求和特性来配置，以确保网络中的其他节点能够及时更新ARP缓存；过多的免费ARP消息可能导致网络拥塞，而过少可能导致ARP缓存更新不及时；在配置此项时，还应考虑到启动时网络的负载和性能影响。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpArpTableSizeMax|
|描述|Maximum number of entries in the ARP table.|
|描述|概述：TcpIpArpTableSizeMax 配置项用于定义TCP/IP协议栈中ARP（地址解析协议）表的最大尺寸，这个尺寸决定了可以缓存多少个IP地址到MAC地址的映射关系。|
|描述|注意：在配置TcpIpArpTableSizeMax时，需要确保其值不超过网络环境中可能出现的最大设备数；过大的ARP表可能会增加内存消耗，而过小的ARP表可能导致频繁的ARP广播，影响网络性能；此配置项的设置应当与实际的网络拓扑和通信需求相匹配。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

###### 1.3.1.1.1. TcpIpStaticArpEntry

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpStaticArpEntry|
|描述|This container includes a static IP address to physical address mapping.|
|描述|概述：TcpIpStaticArpEntry 配置项用于定义静态ARP（地址解析协议）表项，这些表项将IP地址映射到固定的物理硬件地址，通常用于网络通信中的地址解析。|
|描述|注意：在配置静态ARP表项时，确保IP地址与物理地址的映射是正确且必要的；静态ARP条目通常用于网络设备或关键节点，以避免ARP广播引起的延迟。|
|多实例个数|0 - inf|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpStaticArpEntryIpAddr|
|描述|This parameter defines the IP address that shall be statically mapped to the physical address defined in IpV4StaticArpEntryPhysAddr|
|描述|概述：TcpIpStaticArpEntryIpAddr 配置项用于定义静态ARP表中的IP地址，这是网络通信中用于将IP地址映射到物理MAC地址的过程的一部分。|
|描述|注意：在配置静态ARP条目时，需要确保IP地址与网络拓扑和地址分配策略一致；静态ARP条目通常用于网络设备或关键节点，以减少ARP广播和提高通信效率。|
|多实例个数|1 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpStaticArpEntryPhysAddr|
|描述|This parameter defines the physical address that shall be used for outgoing packets to the IP address specified in IpV4StaticArpEntryIpAddr|
|描述|概述：TcpIpStaticArpEntryPhysAddr配置项用于定义静态ARP表中条目的物理地址，即MAC地址，这有助于网络通信中的IP地址与物理地址的映射。|
|描述|注意：在配置静态ARP条目时，确保物理地址的格式正确且与网络中的实际硬件地址相匹配；静态ARP条目应谨慎使用，以避免网络上的地址冲突。|
|多实例个数|1 - 1|

##### 1.3.1.2. TcpIpIcmpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIcmpConfig|
|描述|Specifies the configuration parameters of the ICMP (Internet Control Message Protocol) sub-module.|
|描述|概述：TcpIpIcmpConfig配置项用于定义TCP/IP协议栈中ICMP(Internet Control Message Protocol)的相关参数，这包括ICMP消息的处理方式、错误消息的生成条件等，以确保网络通信的正确性和高效性。|
|描述|注意：在配置TcpIpIcmpConfig时，需要确保ICMP消息类型和错误代码的正确性和适用性。|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpEchoReplyEnabled|
|描述|Enables or disables transmission of ICMP echo reply message in case of a ICMP echo reception.|
|描述|概述：TcpIpIcmpEchoReplyEnabled配置项用于启用或禁用ICMP（Internet Control Message Protocol）回声应答功能，这是网络通信中用于诊断网络连接问题的一种机制。|
|描述|注意：需要确保网络管理策略与此配置项相协调，以避免潜在的安全风险；此配置项对于网络诊断和远程通信的可靠性至关重要，应谨慎启用；在低带宽或高安全要求的网络环境中，可能需要禁用此功能以优化性能和安全性。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpUnreachReplyEnabled|
|描述|Enables or disables transmission of ICMP unreach reply message in case of a Unreachable UDP reception.|
|描述|概述：TcpIpIcmpUnreachReplyEnabled配置项用于启用或禁用ICMP不可达消息的回复功能，当IP层无法将数据包传递给上层时，此功能决定是否发送ICMP不可达消息给发送者。|
|描述|注意：在配置此项时，应考虑网络安全策略和资源使用情况；过多的ICMP不可达消息可能会导致网络拥塞或被用于网络攻击。|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIcmpTtl|
|描述|Default Time-to-live value of outgoing ICMP packets.|
|描述|概述：TcpIpIcmpTtl 配置项用于定义在TCP/IP协议栈中，ICMP（Internet Control Message Protocol）数据包的生存时间（Time To Live），即数据包在网络中可以经过的最大路由器数目。|
|描述|注意：该值通常设置为一个较小的固定数值，如64或128，以防止数据包在网络中无限循环；不同的操作系统或网络设备可能有默认的TTL值，需确保在AUTOSAR环境中的设置与网络环境兼容。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.3.1.3. TcpIpIpFragmentationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpFragmentationConfig|
|描述|Specifies the configuration parameters of IPv4 packet fragmentation/reassembly.|
|描述|概述：TcpIpIpFragmentationConfig 是一个配置参数，用于定义TCP/IP协议栈中IP分片的行为，包括是否允许分片以及分片的具体参数。|
|描述|注意：需要确保网络栈配置与IP分片需求相匹配；过大的分片可能会导致网络效率降低，而过小的分片可能会增加处理的复杂性；此外，某些网络环境可能不支持IP分片，因此在设计时需考虑目标部署环境。|
|说明|如果多个 IPv4 实例需要使用相同的配置，则可以引用此容器；如果不同的 IPv4 实例需要不同的配置，则可以为该容器创建多个实例。|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIpFragmentationTxEnabled|
|描述|Enables (TRUE) or disables (FALSE) support for fragmentation of output datagrams according to IETF RFC 815.|
|描述|概述：TcpIpIpFragmentationTxEnabled配置项用于启用或禁用TCP/IP协议栈在传输时的IP分片功能，这决定了系统是否能够将大于网络MTU的数据包分割成较小的片段进行发送。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保网络带宽和处理能力与IP分片功能的开启状态相匹配；过度使用IP分片可能会增加网络延迟和处理开销；在设计系统通信策略时，应考虑到目标网络环境的特性和限制。|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIpFragmentationRxEnabled|
|描述|Enables (TRUE) or disables (FALSE) support for reassembling of incoming datagrams that are fragmented according to IETF RFC 815 (IP Datagram Reassembly Algorithms).|
|描述|概述：TcpIpIpFragmentationRxEnabled 配置项用于启用或禁用TCP/IP协议栈中接收IP分片的功能，这是网络通信中处理大于最大传输单元（MTU）的数据包所必需的。|
|描述|注意：需要确保此配置项与系统的内存和性能要求相匹配；如果系统资源有限，接收大量的IP分片可能会导致性能下降；此外，需要考虑网络安全方面的影响，因为IP分片可能会被用于恶意目的。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpIpReassTimeout|
|描述|Specifies the timeout in [s] after which an incomplete datagram gets discarded.|
|描述|概述：TcpIpIpReassTimeout 配置项用于定义TCP/IP协议栈中IP分片重组的超时时间，即在多长时间内未完成分片重组则放弃重组过程，释放相关资源。|
|描述|注意：该值需要根据网络条件和应用场景合理设置，以避免过早放弃重组导致数据丢失，或过长等待导致资源占用；该配置项的单位通常是毫秒，确保与系统定时器分辨率兼容；超时值过小可能导致在高延迟网络中频繁重组失败，而超时值过大可能会导致系统资源长时间被占用。|
|说明|Note: 仅当 TcpIpIpFragmentationRxEnabled 为 TRUE 时，该参数才起作用。|
|多实例个数|0 - 1|
|默认值|60|
|取值范围|0 - Inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpNumFragments|
|描述|Specifies the maximum number of IP fragments per datagram.|
|描述|概述：TcpIpIpNumFragments 配置项用于定义TCP/IP协议栈中，IP层可以同时处理的IP分片数量，这个参数影响着网络通信中数据包的处理能力。|
|描述|注意：在设置TcpIpIpNumFragments时，需要确保值不超过系统资源允许的最大值；过低的设置可能导致在高数据流量下丢包；此配置项应与网络通信的预期负载和系统内存资源相匹配。|
|说明|Note: 仅当 TcpIpIpFragmentationRxEnabled 为 TRUE 时，此参数才适用。|
|多实例个数|0 - 1|
|默认值|10|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpNumReassDgrams|
|描述|Specifies the maximum number of fragmented IP datagrams that can be reassembled in parallel.|
|描述|概述：TcpIpIpNumReassDgrams配置项用于定义系统能够同时重组的IP数据报的最大数量，这有助于管理内存资源并防止拒绝服务攻击。|
|描述|注意：该值应根据系统的内存资源和网络需求谨慎配置；过低的值可能导致在高负载下数据报无法被正确重组，过高的值可能会消耗过多的系统资源。|
|说明|Note: 仅当 TcpIpIpFragmentationRxEnabled 为 TRUE 时，该参数才有意义。|
|多实例个数|0 - 1|
|默认值|5|
|取值范围|0 - 65535|

### 1.4. TcpIpLocalAddr

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpLocalAddr|
|描述|Specifies the local IP (Internet Protocol) addresses used for IP communication.|
|描述|概述：TcpIpLocalAddr配置项定义了TCP/IP协议栈中本地地址的配置信息，包括IP地址、子网掩码和默认网关等，用于网络通信中的地址分配和识别。|
|描述|注意：在配置TcpIpLocalAddr时，必须确保IP地址的唯一性和正确性，避免网络冲突；子网掩码需要正确配置以确保网络分段的准确性；默认网关的配置应当指向可达的路由器地址，以保证外网通信的可行性。|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpAddressType|
|描述|Address type.|
|描述|概述：TcpIpAddressType配置项用于定义TCP/IP模块中使用的IP地址类型，包括unicast，multicast，anycast，确保网络通信的正确性和兼容性。|
|描述|注意：在配置TcpIpAddressType时，需要依据实际的通信场景选择正确的IP地址类型，unicast为单播通信，multicast为多播通信，anycast为任意地址通信。|
|多实例个数|1 - 1|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpDomainType|
|描述|Address family.|
|描述|概述：TcpIpDomainType配置项用于指定TCP/IP协议栈中使用的网络域类型，决定了网络通信的地址族，常见的类型包括IPv4和IPv6。|
|描述|注意：需要确保选择的TcpIpDomainType与项目的网络需求一致；若项目需要同时支持IPv4和IPv6，则需要为每种协议配置独立的TcpIpDomainType；配置错误可能导致网络通信失败或性能下降。|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpAddrId|
|描述|IP address table identifier assigned by TCP/IP stack.|
|描述|概述：TcpIpAddrId 是一个配置项，用于唯一标识网络栈中的IP地址，它关联了特定的IP地址配置和使用该地址的网络接口。|
|描述|注意：在配置TcpIpAddrId时，必须确保每个ID在整个系统中是唯一的；此外，TcpIpAddrId的分配应与网络接口和IP地址配置保持一致；在配置过程中，还需注意与其他网络配置参数的依赖关系和兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpCtrlRef|
|描述|Reference to a TcpIpCtrl specifying the EthIf Controller where the IP address shall be assigned.|
|描述|概述：TcpIpCtrlRef 是一个配置参数，用于指定 TCP/IP 协议栈控制器的引用，确保网络通信功能与特定的网络控制器相关联。|
|描述|注意：在配置 TcpIpCtrlRef 时，必须确保引用的网络控制器与 TCP/IP 协议栈兼容；引用的控制器必须在系统中存在并被正确初始化；在多控制器系统中，每个 TCP/IP 堆栈应有其唯一的控制器引用。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpCtrl|

#### 1.4.1. TcpIpAddrAssignment

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpAddrAssignment|
|描述|This container is a subcontainer of TcpIpLocalAddr and specifies the assignment policy for the IP address.|
|描述|概述：TcpIpAddrAssignment 配置项用于定义TCP/IP协议栈中网络接口的IP地址分配机制，包括静态配置、DHCP、LinkLocal（如IPv4的APIPA）或者SLAAC（无状态地址自动配置，用于IPv6）等方式。|
|描述|注意：在配置TcpIpAddrAssignment时，需要确保所选的地址分配方式与网络环境和应用需求相匹配；对于静态地址配置，必须保证IP地址的唯一性和正确性；在使用DHCP或SLAAC时，应确保网络中存在相应的服务器或代理以支持地址分配过程。|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpAssignmentLifetime|
|描述|Defines the lifetime of a dynamically fetched IP address.|
|描述|概述：TcpIpAssignmentLifetime 配置项定义了TCP/IP协议栈中动态分配的IP地址的租约时间，即该地址在没有续租的情况下可以保留多久。|
|描述|注意：在配置动态IP地址时，需要确保租约时间与网络中的DHCP服务器设置相匹配；租约时间过短可能导致频繁的IP地址续租，增加网络负载；租约时间过长可能导致IP地址资源不足，影响新设备的接入。|
|说明|If TcpIpAssignmentMethod = TCPIP_STATIC then TcpIpAssignmentLifetime shall be omitted.|
|多实例个数|0 - 1|
|默认值|TCPIP_FORGET|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpAssignmentMethod|
|描述|Method of address assignment|
|描述|概述：TcpIpAssignmentMethod 配置项用于定义TCP/IP协议栈中网络接口的IP地址分配方法，例如静态分配、动态分配或者通过LinkLocal地址分配。|
|描述|注意：需要确保选择的IP地址分配方法与系统设计和网络管理策略相匹配；对于动态分配，通常需要集成DHCP客户端；对于静态分配，需要确保配置的静态IP地址在网络中是唯一的，避免地址冲突。|
|多实例个数|1 - 1|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpAssignmentTrigger|
|描述|Trigger of address assignment.|
|描述|概述：TcpIpAssignmentTrigger配置项用于定义TCP/IP协议栈中网络接口的IP地址分配机制，决定是静态分配还是动态获取（如DHCP）。|
|描述|注意：在配置TcpIpAssignmentTrigger时，需确保网络接口与分配机制的兼容性；动态分配（DHCP）可能导致启动时延迟；静态分配需确保IP地址在网络中的唯一性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpAssignmentPriority|
|描述|Priority of assignment (1 is highest). If a new address from an assignment method with a higher priority is available, it overwrites the IP address previously assigned by an assignment method with a lower priority.|
|描述|概述：TcpIpAssignmentPriority 配置项用于定义网络接口（如以太网接口）的IP地址分配优先级，它决定了在多种IP地址分配方法（如静态配置、DHCP等）可用时，系统应优先选择哪种方法。|
|描述|注意：在配置TcpIpAssignmentPriority时，需要确保它与系统中所有可用的IP地址分配方法相匹配；优先级设置应符合网络设计和通信需求。|
|多实例个数|1 - 1|
|取值范围|1 - 3|

#### 1.4.2. TcpIpStaticIpAddressConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpStaticIpAddressConfig|
|描述|This container is a subcontainer of TcpIpLocalAddr and specifies a static IP address including directly related parameters.|
|描述|概述：TcpIpStaticIpAddressConfig 是一个配置项，用于定义TCP/IP协议栈中静态IP地址的配置，包括IP地址、子网掩码和默认网关。|
|描述|注意：在配置静态IP时，需要确保IP地址在网络中是唯一的，避免地址冲突；子网掩码需要正确配置以确保网络分割和通信的正确性；默认网关应当是可达的，且在同一子网内。|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNetmask|
|描述|Network mask of IPv4 address or address prefix of IPv6 address in CIDR Notation, i.e. decimal value between 0 and 32 (IPv4) or 0 and 128 (IPv6) that describes the number of significant bits defining the network number or prefix of an IP address.|
|描述|概述：TcpIpNetmask 配置项用于定义TCP/IP协议栈中网络接口的子网掩码，它决定了网络的大小和主机地址的范围。|
|描述|注意：子网掩码必须与网络的IP地址范围相匹配；在配置子网掩码时，应确保它符合CIDR（无类别域间路由）标准。|
|多实例个数|0 - 1|
|取值范围|0 - 128|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpDefaultRouter|
|描述|IP address of default router (gateway)|
|描述|概述：TcpIpDefaultRouter 配置项用于定义TCP/IP协议栈中的默认路由器的IP地址，这是网络通信中用于将数据包从一个网络转发到另一个网络的设备。|
|描述|注意：在配置TcpIpDefaultRouter时，需要确保提供的IP地址与网络拓扑和地址分配方案相匹配；如果系统中存在多个网络接口，可能需要为每个接口配置不同的默认路由器；在动态IP环境下，如使用DHCP，应确保默认路由器的配置能够动态更新以适应可能的网络变化。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpStaticIpAddress|
|描述|Static IP Address.|
|描述|概述：TcpIpStaticIpAddress配置项用于定义网络接口的静态IP地址配置，包括IP地址、子网掩码和默认网关地址，用于网络通信中的地址分配和路由选择。|
|描述|注意：在使用静态IP配置时，确保IP地址在网络中的唯一性，避免地址冲突；子网掩码需正确配置以确保网络分段正确；默认网关地址应指向可达的路由器接口，以保证外网通信的连通性。|
|说明|要为特定的 EthIfCtrl 指定任意 IP 地址，必须将通配符设置为 “ANY”。更多详情请参见 TcpIp_Bind()。|
|多实例个数|1 - 1|

### 1.5. TcpIpSocketOwnerConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpSocketOwnerConfig|
|描述|Specifies the upper layer modules of TcpIp using the socket API.|
|描述|概述：TcpIpSocketOwnerConfig配置项用于定义TCP/IP协议栈中的套接字所有者信息，包括所有者的标识符和其所拥有的套接字的配置。|
|描述|注意：确保每个套接字所有者的标识符在系统中是唯一的；配置时需考虑系统中所有网络通信需求，以避免资源冲突。|
|多实例个数|1 - 1|

#### 1.5.1. TcpIpSocketOwner

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpSocketOwner|
|描述|This container is a subcontainer of TcpIpSocketOwnerConfig and specifies an upper layer of TcpIp that uses the socket API.|
|描述|概述：TcpIpSocketOwner配置项定义了拥有TCP/IP套接字的模块或组件，用于指定哪些模块可以创建和管理TCP/IP连接。|
|描述|注意：在配置TcpIpSocketOwner时，需要确保指定的模块或组件已经包含了网络通信的功能和权限；此配置项对于网络通信的安全性和稳定性至关重要，需要仔细规划。|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerUpperLayerType|
|描述|This parameter specifies the type of the upper layer module.|
|描述|概述：TcpIpSocketOwnerUpperLayerType配置项用于定义TCP/IP协议栈中，上层所有者（如DoIP, HTTP, or SOME/IP）使用的套接字类型。|
|描述|注意：在配置时需确保上层协议与所选套接字类型兼容；正确配置此项对于网络通信的性能和稳定性至关重要。|
|多实例个数|1 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpSocketOwnerTcpIpEventName|
|描述|This parameter defines the name of the <Up_TcpIpEvent> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerTcpIpEventName 配置项用于定义与特定TCP/IP套接字相关联的事件名称，这些事件用于通知套接字所有者有关网络状态变化或数据传输状态的信息。|
|描述|注意：在配置TcpIpSocketOwnerTcpIpEventName时，需要确保事件名称的唯一性，以避免在系统中的事件处理混淆；此外，事件名称应与实际的网络管理和数据传输逻辑相对应，以确保正确的事件触发和处理。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerCopyTxDataName|
|描述|This parameter defines the name of the <Up_CopyTxData> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerCopyTxDataName配置项用于指定在发送数据过程中，哪个Socket所有者（如某个网络管理模块）负责复制待发送的数据到TCP/IP栈。|
|描述|注意：在配置此项时，确保指定的Socket所有者具有相应的数据复制能力；此配置项对于实现零拷贝发送机制尤为重要；不正确的配置可能导致数据发送失败或性能下降。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerHeaderFileName|
|描述|This parameter specifies the name of the header file containing the definition of the TcpIpSocketOwner module functions. The header file name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerHeaderFileName配置项指定了TCP/IP协议栈为Socket所有者模块生成的头文件名称，该文件包含必要的声明和定义，以便于模块通过TCP/IP协议栈进行通信。|
|描述|注意：文件名应遵循项目的命名约定，以确保一致性和可维护性；确保该文件在项目的包含路径中，以便于编译器找到。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerLocalIpAddrAssignmentChgName|
|描述|This parameter defines the name of the <Up_LocalIpAddrAssignmentChg> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerLocalIpAddrAssignmentChgName 配置项用于指定当TCP/IP套接字所有者的本地IP地址分配状态发生变化时，应调用的回调函数的名称。|
|描述|注意：在配置此项时回调函数应当能够处理IP地址分配状态的变化，并执行相应的网络状态更新或资源回收；此配置项通常与网络管理和通信堆栈的配置紧密相关，因此在设计时应考虑整体网络架构。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerRxIndicationName|
|描述|This parameter defines the name of the <Up_RxIndication> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerRxIndicationName 配置项用于指定当TCP/IP协议栈接收到新数据时，应调用的上层组件（Socket Owner）的接收指示函数的名称。|
|描述|注意：确保指定的函数名在上层组件中存在并且正确实现了接收指示的接口。在配置多个Socket Owner时，每个Socket Owner的接收指示函数名应该是唯一的。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerTcpAcceptedName|
|描述|This parameter defines the name of the <Up_TcpAccepted> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerTcpAcceptedName配置项用于定义TCP/IP协议栈中，当一个TCP连接被接受时，所使用的Socket连接的名称。|
|描述|注意：该配置项需要确保与TcpIpSocket连接的配置一致，以便正确地映射和管理TCP连接；在配置时需注意名称的唯一性，避免在同一TCP/IP协议栈中出现重名。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerTcpConnectedName|
|描述|This parameter defines the name of the <Up_TcpConnected> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerTcpConnectedName配置项用于定义TCP/IP协议栈中，当TCP连接建立时，所属Socket的标识名称。|
|描述|注意：该配置项的命名需要遵循AUTOSAR命名规范，确保在整个项目中的唯一性；在配置过程中，需要确保所引用的Socket已经在系统中定义。|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpSocketOwnerTxConfirmationName|
|描述|This parameter defines the name of the <Up_TxConfirmation> function of the TcpIpSocketOwner module. The function name shall only be configurable if TcpIpSocketOwnerUpperLayerType is set to CDD.|
|描述|概述：TcpIpSocketOwnerTxConfirmationName 是一个配置参数，用于指定在TCP/IP协议栈中，当数据成功发送后，哪个Socket所有者（如某个应用层模块）将被通知确认信息。|
|描述|注意：在配置时需确保该名称与系统中定义的Socket所有者名称一致；此参数通常与TcpIpSocketOwner配置项相关联，需要与其保持一致性；在配置多个Socket所有者时，每个Socket所有者的确认函数名称应该是唯一的，以避免潜在的冲突。|
|多实例个数|0 - 1|

### 1.6. TcpIpTcpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTcpConfig|
|描述|Specifies the configuration parameters of the TCP (Transmission Control Protocol) sub-module.|
|描述|概述：TcpIpTcpConfig 是用于配置TCP/IP协议栈中TCP协议相关参数的配置项，它包括了如超时时间、最大重传次数等TCP连接的参数设置。|
|描述|注意：在配置TcpIpTcpConfig时，需要确保参数设置符合网络通信的性能要求和稳定性需求。|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpCongestionAvoidanceEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of TCP congestion avoidance algorithm according to IETF RFC 5681.|
|描述|概述：TcpIpTcpCongestionAvoidanceEnabled 配置项用于启用或禁用TCP/IP协议栈中的拥塞避免机制，该机制负责在网络拥塞时调整数据传输速率。|
|描述|注意：在配置此项时，需考虑网络的实际条件和性能要求；不正确的配置可能导致网络拥塞控制不当，影响通信效率。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpFastRecoveryEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of TCP Fast Recovery according to IETF RFC 5681.|
|描述|概述：TcpIpTcpFastRecoveryEnabled 是一个配置参数，用于启用或禁用TCP快速恢复机制，该机制在TCP发生丢包时帮助快速恢复连接的稳定性和性能。|
|描述|注意：需要确保此配置项与网络堆栈的其他部分和TCP协议的实现细节保持一致；考虑到系统资源和性能要求，合理启用或禁用此功能；在配置时应注意与TcpIpTcpFastRetransmitEnabled配置项的关系和协同工作。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpFastRetransmitEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of TCP Fast Retransmission according to IETF RFC 5681.|
|描述|概述：TcpIpTcpFastRetransmitEnabled配置项用于启用或禁用TCP快速重传机制，这是一种网络通信性能优化手段，旨在快速恢复丢失的数据包。|
|描述|注意：需要确保网络管理策略与此配置项相协调，以优化网络性能；不当的启用或禁用可能导致网络延迟增加或通信不稳定；此配置项对实时数据传输尤为关键，需根据应用需求谨慎配置。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpKeepAliveEnabled|
|描述|Enables (TRUE) or disables (FALSE) TCP Keep Alive Probes according to IETF RFC 1122 chapter 4.2.3.6|
|描述|概述：TcpIpTcpKeepAliveEnabled 配置项用于启用或禁用TCP连接的Keep Alive机制，该机制可以定期检查TCP连接是否仍然有效，以维持长时间的连接。|
|描述|注意：在配置该项时，需考虑系统对网络连接稳定性的要求；过于频繁的Keep Alive消息可能会增加网络负载；不正确的配置可能导致资源浪费或连接不稳定。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpNagleEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of Nagle's algorithm according to IETF RFC 896. If enabled the Nagle's algorithm is activated per default for all TCP sockets, but can be deactivated via TcpIp_ChangeParameter() API.|
|描述|概述：TcpIpTcpNagleEnabled配置项用于启用或禁用TCP/IP协议栈中的Nagle算法，该算法旨在减少网络上的小分组数量，通过合并小的TCP数据包来提高网络效率。|
|描述|注意：在实时性要求较高的应用中应谨慎启用Nagle算法，因为它可能增加数据的传输延迟；此配置项的默认值依赖于具体的AUTOSAR TCP/IP协议栈实现，需查阅具体实现文档确认；在配置此项时，应考虑网络带宽和延迟的权衡。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpSlowStartEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of TCP slow start algorithm according to IETF RFC 5681.|
|描述|概述：TcpIpTcpSlowStartEnabled 是一个配置参数，用于启用或禁用TCP协议中的慢启动算法，该算法用于控制数据传输的拥塞窗口的增长速度，以避免网络拥塞。|
|描述|注意：需要确保此配置项与网络的拥塞控制策略一致；不当的启用或禁用可能会影响网络性能和稳定性；在配置时应考虑网络的实际条件和性能要求。|
|多实例个数|1 - 1|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpFinWait2Timeout|
|描述|Timeout in [s] to receive a FIN from the remote node (after this node has initiated connection termination), i.e. maximum time waiting in FINWAIT-2 for a connection termination request from the remote TCP.|
|描述|概述：TcpIpTcpFinWait2Timeout 配置项用于定义在TCP/IP协议栈中，TCP连接在FIN-WAIT-2状态下等待对方的FIN包的超时时间。|
|描述|注意：该值需要根据网络条件和应用需求谨慎配置，以避免过早关闭连接或资源占用过长；超时设置不当可能会导致网络连接问题，如连接挂起或资源泄露。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpKeepAliveInterval|
|描述|Specifies the interval in [s] between subsequent keepalive probes.|
|描述|概述：TcpIpTcpKeepAliveInterval 配置项用于定义TCP连接在没有数据传输时发送保活（Keep-Alive）探测包的时间间隔，以维持连接的活跃状态。|
|描述|注意：该值应根据网络条件和应用需求谨慎配置，避免过于频繁的保活探测导致不必要的网络负载；保持与系统的其他超时设置（如Nagle算法的延迟确认时间）的协调一致。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpKeepAliveTime|
|描述|Specifies the time in [s] between the last data packet sent (simple ACKs are not considered data) and the first keepalive probe. Note: Setting this configuration parameter to a value smaller or equal to the value of TcpIpMainFunctionPeriod results in the transmission of keep alive probes within every MainFunction cycle.|
|描述|概述：TcpIpTcpKeepAliveTime配置项用于定义TCP连接在没有数据传输时，保持连接活跃的时间间隔，即在此时间后发送keepalive探测包以检测连接是否仍然有效。|
|描述|注意：该值的设置需要根据网络条件和应用需求谨慎选择，以避免过频繁的探测导致不必要的网络负担；过长的时间间隔可能导致无效连接长时间占用资源。|
|多实例个数|1 - 1|
|默认值|7200|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpMsl|
|描述|Maximum segment lifetime in [s].|
|描述|概述：TcpIpTcpMsl配置项定义了TCP/IP协议栈中的最大段生命周期（Maximum Segment Lifetime），它是TCP连接被终止后，该连接的任何数据包在网络中存在的最长时间。|
|描述|注意：该值的设置对系统资源和网络性能有重要影响；过小的值可能导致有效数据包被过早丢弃，过大的值可能导致资源占用过久。|
|说明|(Note: TIME-WAIT = 2 x TcpIpTcpMsl - to ensure that the remote node received the acknowledgment to its connection termination request.)|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpRetransmissionTimeout|
|描述|Timeout in [s] before an unacknowledged TCP segment is sent again.|
|描述|概述：TcpIpTcpRetransmissionTimeout 配置项用于定义TCP协议栈中，当一个TCP段需要重传时，等待重传的超时时间。|
|描述|注意：该值需要根据网络的具体条件和性能要求来调整，以确保网络通信的可靠性和效率；设置过短可能导致不必要的网络流量和性能问题，设置过长可能导致应用响应延迟。|
|说明|If the timeout is disabled or set to INF, no TCP segments shall be retransmitted.|
|多实例个数|0 - 1|
|取值范围|0.001 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpTcpSynReceivedTimeout|
|描述|Timeout in [s] to complete a remotely initiated TCP connection establishment, i.e. maximum time waiting in SYN-RECEIVED for a confirming connection request acknowledgment after having both received and sent a connection request.|
|描述|概述：TcpIpTcpSynReceivedTimeout 配置项用于定义TCP/IP协议栈中，等待一个SYN+ACK响应的最大时间，在这个时间内如果没有收到响应，连接请求将被终止。|
|描述|注意：该值需要根据网络的延迟和拥塞情况来合理设置，以避免过早断开可能成功的连接；过高的值可能导致资源占用时间过长，影响系统性能。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpKeepAliveProbesMax|
|描述|Maximum number of times that a TCP Keep Alive is retransmitted before the connection is closed.|
|描述|概述：TcpIpTcpKeepAliveProbesMax配置项定义了在TCP连接中，当没有数据交换时，最大的保活探测报文发送次数，用于维持连接的活性。|
|描述|注意：该值应当根据网络条件和应用需求谨慎设置，以避免过早断开连接或资源浪费；超出此次数未收到响应则认为连接已断开。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpMaxRtx|
|描述|Maximum number of times that a TCP segment is retransmitted before the TCP connection is closed. This parameter is only valid if TcpIpTcpRetransmissionTimeout is configured.|
|描述|概述：TcpIpTcpMaxRtx 配置项用于定义TCP协议中最大重传次数，即一个TCP报文段在被认定为丢失之前，可以被重传的最大次数。|
|描述|注意：该值应当根据网络条件和应用场景谨慎设置，以避免过早放弃重传导致的连接失败，或者过多重传导致的网络资源浪费；该配置项的取值范围应符合标准规定，否则可能会导致不兼容或性能问题；在配置时还需考虑与TcpIpTcpRto和TcpIpTcpSynMaxRtx等参数的关系和整体网络栈的性能优化。|
|说明|Note: This parameter also applies for FIN retransmissions.|
|多实例个数|0 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpReceiveWindowMax|
|描述|Default value of maximum receive window in bytes.|
|描述|(7, TypeError("'AssertionError' object is not subscriptable"))|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpSendBufferMax|
|描述|Default value of maximum receive window in bytes.|
|描述|概述：TcpIpTcpSendBufferMax定义了TCP/IP协议栈中，TCP发送缓冲区的最大大小，用于控制每个TCP连接可以使用的最大发送缓冲区空间。|
|描述|注意：该参数的设置应考虑系统的内存资源和网络性能需求；过大的发送缓冲区可能会导致内存资源的浪费，过小可能会影响网络传输效率。|
|多实例个数|1 - 1|
|取值范围|2 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpSynMaxRtx|
|描述|Maximum number of times that a TCP SYN is retransmitted.|
|描述|概述：TcpIpTcpSynMaxRtx配置项定义了在TCP/IP协议栈中，SYN报文的最大重传次数，用于在TCP连接建立过程中控制SYN报文的重传行为。|
|描述|注意：该值过大可能导致系统资源的浪费，尤其是在网络状况不佳时；过小可能导致在网络延迟较大的情况下连接建立失败；需根据网络环境和应用需求谨慎配置。|
|说明|注意：SYN将在 TcpIpTcpRetransmissionTimeout 过后重试。如果在最后一次发送 TCP SYN 并且超出 TcpIpTcpRetransmissionTimeout 后，仍未收到匹配的连接请求，则该连接将被丢弃。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpTtl|
|描述|Default Time-to-live value of outgoing TCP packets.|
|描述|概述：TcpIpTcpTtl配置项定义了TCP/IP协议栈中TCP报文的生存时间（Time To Live），即一个TCP报文在网络中可以经过的最大路由器数目。|
|描述|注意：该值必须是一个介于1到255之间的整数，以确保报文在网络中的有效传输；过低的TTL值可能导致报文在到达目的地之前就被丢弃。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.6.1. TcpIpTcpConfigOptionFilter

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpConfigOptionFilterId|
|描述|Identification of the TCP option filter.|
|描述|None|
|多实例个数|1 - 1|
|取值范围|0 - 255|

### 1.7. TcpIpUdpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpUdpConfig|
|描述|Specifies the configuration parameters of the UDP (User Datagram Protocol) sub-module|
|描述|概述：TcpIpUdpConfig配置项用于定义UDP协议栈的参数，包括端口号、目标IP地址、以及相关的接收和发送缓冲区大小等，确保UDP通信的正确性和性能。|
|描述|注意：在配置TcpIpUdpConfig时，需确保端口号的唯一性，避免与系统中其他服务的端口号冲突；合理设置缓冲区大小，以避免数据丢失或额外的内存消耗。|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpUdpTtl|
|描述|Default Time-to-live value of outgoing UDP packets.|
|描述|概述：TcpIpUdpTtl配置项定义了UDP协议在IP网络中传输数据包时的生存时间（Time To Live，TTL），即数据包在网络中可以经过的最大路由器数目。|
|描述|注意：TTL值过低可能导致数据包在到达目的地之前就被丢弃，特别是在跨越多个网络时；过高的TTL值可能导致无效或恶意的数据包在网络中过长时间流转，增加网络负担。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

## 2. TcpIpGeneral

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpGeneral|
|描述|This container is a subcontainer of TcpIp and specifies the general configuration parameters of the TCP/IP stack.|
|描述|概述：TcpIpGeneral配置参数集合定义了TCP/IP协议栈的全局配置，包括协议栈的行为和性能特性。|
|描述|注意：在配置TcpIpGeneral时，需要确保参数设置符合网络通信需求和资源限制；此外，应注意与其他网络管理配置的兼容性和一致性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：TcpIpDevErrorDetect配置项用于启用或禁用TCP/IP协议栈中的开发错误检测功能，以便在开发阶段识别和报告潜在的错误。|
|描述|注意：在生产代码中通常禁用此功能以优化性能；确保在开发和测试阶段启用以捕获和修正错误。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpGetAndResetMeasurementDataApi|
|描述|Enables / Disables the Get and Reset Measurement Data API|
|描述|概述：TcpIpGetAndResetMeasurementDataApi 是一个配置项，用于启用或禁用一个API，该API允许获取并重置TCP/IP模块的测量数据，通常用于诊断或网络管理目的。|
|描述|注意：需要确保该API的使用不会违反任何实时性要求或影响网络通信性能；如果不需要诊断或性能测量功能，可以禁用此API以节省资源；使用此API时，应注意数据的原子性和一致性，避免在获取和重置过程中的数据竞争。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpResetIpAssignmentApi|
|描述|Enables/disables the API TcpIp_ResetIpAssignment of a DHCP-client.|
|描述|概述：TcpIpResetIpAssignmentApi 配置项用于指定是否启用了一个API，该API允许上层协议栈动态地重置网络接口的IP地址分配。|
|描述|注意：需要确保此API的使用与系统的IP地址管理策略一致；如果启用此API，需要确保网络管理和通信管理逻辑能够正确处理IP地址的动态变化；在设计网络接口管理时，考虑到重置IP分配可能对现有通信会话产生的影响。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTcpEnabled|
|描述|Enables (TRUE) or disabled (FALSE) support of TCP (Transmission Control Protocol).|
|描述|概述：TcpIpTcpEnabled配置项用于启用或禁用TCP/IP协议栈中的TCP协议支持，决定系统是否支持TCP协议的数据传输。|
|描述|注意：在不需要TCP协议支持的应用中禁用此项可以节省系统资源；确保在需要TCP通信的应用中启用此项。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpUdpEnabled|
|描述|Enables (TRUE) or disabled (FALSE) support of UDP (User Datagram Protocol)|
|描述|概述：TcpIpUdpEnabled 配置项用于启用或禁用UDP协议模块。|
|描述|注意：在不需要UDP通信的系统中可以禁用此功能以节省资源；如果项目需求包括UDP通信，则必须启用此配置；在配置时应确保与系统中其他网络配置项的兼容性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpVersionInfoApi|
|描述|If true the TcpIp_GetVersionInfo API is available.|
|描述|概述：TcpIpVersionInfoApi 配置项用于启用或禁用 TCP/IP 栈的版本信息API，允许软件组件获取当前TCP/IP栈的版本信息。|
|描述|注意：如果启用此API，必须确保实现了相应的接口以返回正确的版本信息；如果不需要此功能，可以禁用以节省资源；请注意，启用此功能可能会对系统的内存和执行时间产生轻微影响。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpScalabilityClass|
|描述|In order to customize the TcpIp Stack to the specific needs of the user it can be scaled according to the scalability classes.|
|描述|概述：TcpIpScalabilityClass 是一个配置参数，用于指定TCP/IP协议栈的可伸缩性类别，以适应不同的网络性能和资源需求。|
|描述|注意：在选择TcpIpScalabilityClass时，需要考虑ECU的资源限制和网络通信的性能要求；确保选择的可伸缩性类别与实际应用场景相匹配，以避免资源浪费或性能不足。|
|多实例个数|1 - 1|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpMainFunctionPeriod|
|描述|Period of TcpIp_MainFunction in [s].|
|描述|概述：TcpIpMainFunctionPeriod 配置项用于指定 TCP/IP 协议栈主函数的调用周期，这个周期决定了网络管理、通信控制和时间依赖性功能的处理频率。|
|描述|注意：该值应当与系统定时器和任务调度策略相匹配，以确保网络性能和响应时间满足应用需求；过小的周期可能导致CPU负载过高，而过大的周期可能影响网络通信的实时性；在配置时应参照AUTOSAR CP标准中对于网络管理和通信控制相关的时间参数要求。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpSocketMax|
|描述|Maximum number of TCP sockets|
|描述|概述：TcpIpTcpSocketMax 配置项定义了系统中可用的最大TCP套接字数量，这个值限制了同时可以建立的TCP连接的最大数目。|
|描述|注意：该值应足够大以支持应用程序的并发连接需求；过小的值可能导致无法建立新的TCP连接；过大的值可能会浪费系统资源，因为每个套接字都会占用一定的内存。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpUdpSocketMax|
|描述|Maximum number of UDP sockets.|
|描述|概述：TcpIpUdpSocketMax定义了系统中可用的最大UDP套接字数量，这个参数直接影响到UDP通信的并发能力。|
|描述|注意：在配置TcpIpUdpSocketMax时，需要考虑系统的内存限制和UDP通信的需求量；过高的配置可能会浪费系统资源，过低则可能导致无法建立更多的UDP连接。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

### 2.1. TcpIpIpV4General

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpV4General|
|描述|This container is a subcontainer of TcpIp and specifies the general configuration parameters of the TCP/IP stack for IPv4|
|描述|概述：TcpIpIpV4General配置项用于定义TCP/IP协议栈中IPv4相关的通用配置，包括启用IPv4支持、配置默认的TTL(Time To Live)值等。|
|描述|注意：需要确保IPv4和IPv6的配置不冲突；正确设置TTL值以避免数据包在网络中无限循环；如果项目不使用IPv4，可以禁用以节省资源。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpArpEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of ARP (Address Resolution Protocol).|
|描述|概述：TcpIpArpEnabled配置项用于启用或禁用TCP/IP协议栈中的地址解析协议（ARP）功能，这是决定系统是否支持通过ARP解析网络层地址到链路层地址的关键配置。|
|描述|注意：在不需要局域网通信或者使用静态IP地址配置的场景下，可以考虑禁用ARP以节省资源；确保在启用ARP时，网络配置正确以避免潜在的地址冲突。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpEnabled|
|描述|Enables (TRUE) or disabled (FALSE) support of ICMP (Internet Control Message Protocol).|
|描述|概述：TcpIpIcmpEnabled 配置项用于启用或禁用传输控制协议/互联网协议(TCP/IP)栈中的互联网控制消息协议(ICMP)支持，这对于网络错误诊断和消息控制是重要的。|
|描述|注意：需要确保此配置项与系统的安全和诊断需求相符；不当的ICMP配置可能会导致安全风险；在资源受限的系统中，启用ICMP可能会影响系统性能。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIpV4Enabled|
|描述|Enables (TRUE) or disables (FALSE) support of IPv4 (Internet Protocol version 4).|
|描述|概述：TcpIpIpV4Enabled 配置项用于启用或禁用TCP/IP协议栈中IPv4协议的支持，决定了系统是否能够处理IPv4网络通信。|
|描述|注意：在不需要IPv4支持的系统中可以禁用以节省资源；如果系统需要同时支持IPv4和IPv6，则应确保同时启用TcpIpIpV4Enabled和TcpIpIpV6Enabled；配置更改可能需要重新编译和测试以确保网络功能的正确性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpLocalAddrIpv4EntriesMax|
|描述|Maximum number of LocalAddr table entries for IPv4.|
|描述|概述：TcpIpLocalAddrIpv4EntriesMax定义了系统中可配置的IPv4本地地址的最大数量，用于限制可分配给TCP/IP协议栈的IPv4地址数量。|
|描述|注意：在设计网络配置时，需要确保此值足够容纳预期的网络接口数量；超出此限制的地址配置可能会被忽略；该参数的设置应考虑系统的扩展性和未来的网络需求。|
|多实例个数|1 - 1|
|取值范围|0 - 255|



