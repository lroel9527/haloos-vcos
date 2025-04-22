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
|名称|TcpIpDhcpServerConfigRef|
|描述|Reference to a TcpIpDhcpServerConfig which shall be used for this controller setting (VLAN).|
|描述|概述：TcpIpDhcpServerConfigRef 是一个配置参考，它指向一个特定的DHCP服务器配置，该配置定义了TCP/IP协议栈中DHCP服务器的行为和属性。|
|描述|注意：在配置TcpIpDhcpServerConfigRef时，必须确保它指向的DHCP服务器配置是有效的并且已经定义；此配置项对于实现网络管理功能至关重要，因此需要仔细检查其正确性。|
|说明|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpDhcpServerConfig|

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

###### 1.3.1.2.1. TcpIpIcmpMsgHandler

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIcmpMsgHandler|
|描述|This container is a subcontainer of TcpIpIcmpConfig and specifies the configuration parameters for the ICMP message handler.|
|描述|概述：TcpIpIcmpMsgHandler配置项用于定义网络层的ICMP(Internet Control Message Protocol)消息处理策略，包括如何响应接收到的ICMP请求（如ping请求）。|
|描述|注意：在配置TcpIpIcmpMsgHandler时，需要确保所选策略与系统的安全和性能要求相匹配；不当的ICMP处理策略可能导致网络安全风险。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpIcmpMsgHandlerName|
|描述|This parameter defines the name of the ICMP message handler function <Up_IcmpMsgHandler>.|
|描述|概述：TcpIpIcmpMsgHandlerName 是一个配置项，用于指定处理ICMP（Internet Control Message Protocol）消息的模块或函数的名称，这在网络通信中用于错误消息传递和诊断目的。|
|描述|注意：需要确保指定的处理器名称与实际实现的模块或函数名称一致；处理器应能妥善处理所有预期的ICMP消息类型；配置时需考虑系统的安全性和性能影响。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

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

#### 1.3.2. TcpIpIpV6Config

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpV6Config|
|描述|Specifies the configuration parameters of the IPv6 (Internet Protocol version 6) sub-module.|
|描述|概述：TcpIpIpV6Config 是一个配置容器，它包含了IPv6协议栈的相关配置参数，用于定义IPv6通信的各种属性，如地址配置、邻居发现协议参数等。|
|描述|注意：在配置TcpIpIpV6Config时，需要确保IPv6地址的唯一性和正确的子网划分；必须符合网络的实际需求和IPv6标准；在多网卡系统中，还需注意不同网络接口间的地址配置不冲突。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

##### 1.3.2.1. TcpIpDhcpV6Config

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpDhcpV6Config|
|描述|Specifies the configuration parameters of the DHCPv6.|
|描述|概述：TcpIpDhcpV6Config配置项用于定义IPv6环境下，通过DHCP（动态主机配置协议）获取网络配置参数的相关设置，包括地址分配、续租时间等。|
|描述|注意：在配置TcpIpDhcpV6Config时，需确保网络环境支持IPv6和DHCPv6；正确配置续租和重试策略，以避免网络连接中断；AUTOSAR CP 4.4标准中对DHCPv6的支持可能与某些特定网络设备或软件的实现有差异，需要进行兼容性测试。|
|描述|该配置项未使用|
|说明|如果多个 IPv6 实例需要使用相同的配置，则可引用此容器；如果不同的 IPv6 实例需要各自不同的配置，则可为此容器创建多个实例。|
|多实例个数|0 - inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6CnfDelayMax|
|描述|Maximum delay (s) before sending the first Confirm message. If this value is bigger than the previous minimum delay value a random delay will be chosen from the interval.|
|描述|概述：TcpIpDhcpV6CnfDelayMax 是一个配置参数，用于指定在DHCPv6客户端启动配置过程前等待的最大时间，以随机延迟的方式减少网络上的冲突和拥塞。|
|描述|注意：该值应当设置为一个合理的时间间隔，以确保网络上的多个DHCPv6客户端不会同时发送配置请求；过大的延迟可能会导致网络配置的不必要延迟；该参数的设置必须遵循RFC 3315中关于DHCPv6客户端行为的规定。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 100|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6CnfDelayMin|
|描述|Minimum delay (s) before the first Confirm message will be sent.|
|描述|概述：TcpIpDhcpV6CnfDelayMin配置项定义了在DHCPv6客户端启动配置过程中，发送第一条Solicit消息前的最小延迟时间，用于避免网络上的DHCPv6客户端同时发送消息导致的冲突。|
|描述|注意：该值应小于或等于TcpIpDhcpV6CnfDelayMax值，以确保延迟时间的设置逻辑正确；配置值应根据网络环境合理设置，以减少启动时的网络拥塞。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 100|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6InfDelayMax|
|描述|Maximum delay (s) before sending the first Information Request message. If this value is bigger than the previous minimum delay value a random delay will be chosen from the interval.|
|描述|概述：TcpIpDhcpV6InfDelayMax 配置项定义了在DHCPv6信息请求过程中，客户端在发送第一条信息请求消息前等待的最大时间。|
|描述|注意：该值通常用于控制客户端启动DHCPv6信息请求之前的延迟，以减少网络上的DHCPv6请求冲突；该参数的设置应考虑网络条件和客户端数量。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 100|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6InfDelayMin|
|描述|Minimum delay (s) before the first Information Request message will be sent.|
|描述|概述：TcpIpDhcpV6InfDelayMin配置项定义了在DHCPv6信息请求过程中，客户端在发送第一条信息请求消息前的最小延迟时间。|
|描述|注意：该值应小于或等于TcpIpDhcpV6InfDelayMax值，以避免配置错误；确保设置的延迟时间不会对网络启动时间产生负面影响。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 100|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6SolDelayMax|
|描述|Maximum delay (s) before sending the first Solicit message. If this value is bigger than the previous minimum delay value a random delay will be chosen from the interval.|
|描述|概述：TcpIpDhcpV6SolDelayMax配置项定义了在发送第一个DHCPv6 Solicit消息前等待的最大时间，用于DHCPv6客户端在启动时减少网络上的冲突和拥塞。|
|描述|注意：该值应大于或等于TcpIpDhcpV6SolDelayMin配置项的值；配置过大可能导致网络连接延迟。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 100|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpDhcpV6SolDelayMin|
|描述|Minimum delay (s) before the first Solicit message will be sent.|
|描述|概述：TcpIpDhcpV6SolDelayMin配置项定义了在发送第一个DHCPv6 Solicit消息前等待的最小时间，用于减少网络上的DHCPv6请求冲突。|
|描述|注意：该时间值应小于或等于TcpIpDhcpV6SolDelayMax值，以保证时间配置的有效性；配置值应考虑网络条件，避免因过短的延迟导致的请求冲突。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 100|

##### 1.3.2.2. TcpIpIcmpV6Config

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIcmpV6Config|
|描述|Specifies the configuration parameters of the ICMPv6 (Internet Control Message Protocol for IPv6) sub-module.|
|描述|概述：TcpIpIcmpV6Config 是用于配置IPv6的ICMP（Internet Control Message Protocol）参数，它定义了如何处理IPv6网络中的ICMP消息，例如错误消息和信息查询消息。|
|描述|注意：在配置TcpIpIcmpV6Config时，需要确保ICMPv6消息类型和代码的正确性，以符合IPv6网络的要求；还需注意ICMPv6的错误处理和速率限制设置，以避免网络拥塞和安全风险。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpV6EchoReplyAvoidFragmentation|
|描述|If enabled, the stack will respond only to incoming ICMPv6 Echo Requests (Pings) that fit the MTU of the respective interface, i.e. can be transmitted without IPv6 fragmentation. Only relevant if TcpIpIcmpV6EchoReplyEnabled is enabled.|
|描述|概述：TcpIpIcmpV6EchoReplyAvoidFragmentation 配置项用于控制当TCP/IP协议栈发送ICMPv6 Echo Reply（回显应答）消息时，是否避免IP分片。|
|描述|注意：在配置此项时，应考虑网络的最大传输单元（MTU）和预期的数据包大小，以确保数据包不会因过大而被分片；若设置为避免分片，可能需要调整应用层数据的大小以适应MTU限制；此配置项的设置应与网络的实际条件和性能要求相匹配。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpV6EchoReplyEnabled|
|描述|If enabled, the stack will respond to incoming ICMPv6 Echo Requests (Pings).|
|描述|概述：TcpIpIcmpV6EchoReplyEnabled配置项用于启用或禁用对IPv6 ICMP回显请求（即Ping请求）的回复功能，这对网络诊断和连通性测试至关重要。|
|描述|注意：需要确保网络堆栈配置正确以支持IPv6 ICMP回显回复；不恰当的配置可能导致网络安全风险；在低带宽或高安全要求的网络环境中，谨慎启用此功能。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpV6MsgDestinationUnreachableEnabled|
|描述|Dis/Enables transmission of Destination Unreachable Messages|
|描述|概述：TcpIpIcmpV6MsgDestinationUnreachableEnabled配置项用于启用或禁用ICMPv6目的地不可达消息的发送，这是网络通信中用于告知发送方目标地址不可达的一种机制。|
|描述|注意：在配置此项时，应确保网络通信需求与安全策略之间的平衡；不当的启用或禁用可能会影响网络的故障诊断能力。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpIcmpV6MsgParameterProblemEnabled|
|描述|If enabled an ICMPv6 parameter problem message will be sent if a received packet has been dropped due to unknown options or headers that are found in the packet.|
|描述|概述：TcpIpIcmpV6MsgParameterProblemEnabled 配置项用于启用或禁用ICMPv6 Parameter Problem消息的发送，这是IPv6网络中用于报告数据包中存在问题的一种机制。|
|描述|注意：需要确保此配置项与网络管理需求相符合；不正确的配置可能导致网络通信问题；在安全相关的应用中，需谨慎启用以防止潜在的拒绝服务攻击。|
|描述|该配置项未使用|
|说明|[RFC2460 4. IPv6 Extension Headers]|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIcmpV6HopLimit|
|描述|Default Hop-Limit value of outgoing ICMPv6 packets.|
|描述|概述：TcpIpIcmpV6HopLimit 配置项用于设置IPv6协议中ICMPv6消息的跳数限制，即在网络中传输的最大跳数（路由器数），用以控制消息的传播范围。|
|描述|注意：该值通常设置为255，以确保ICMPv6消息在本地链路上可靠传输；在不同网络环境下可能需要调整此值。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 255|

###### 1.3.2.2.1. TcpIpIcmpV6MsgHandler

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIcmpV6MsgHandler|
|描述|This container is a subcontainer of TcpIpIcmpConfig and specifies the configuration parameters for the ICMPv6 message handler.|
|描述|概述：TcpIpIcmpV6MsgHandler配置项用于定义处理IPv6 ICMP（Internet Control Message Protocol）消息的策略和方法，确保网络通信中的错误和信息能够被正确处理。|
|描述|注意：在配置TcpIpIcmpV6MsgHandler时，需要确保所定义的处理程序与网络需求和安全策略相匹配；此配置项对于网络的稳定性和安全性至关重要，应谨慎配置。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpIcmpV6MsgHandlerName|
|描述|This parameter defines the name of the ICMP message handler function <Up_IcmpMsgHandler>.|
|描述|概述：TcpIpIcmpV6MsgHandlerName 是一个配置参数，用于指定处理IPv6 ICMP（Internet Control Message Protocol）消息的回调函数名。|
|描述|注意：回调函数名应该遵循项目的命名规范，以便于识别和维护；确保该回调函数能够正确处理所有预期的ICMPv6消息类型，以保证网络通信的正确性和可靠性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

##### 1.3.2.3. TcpIpIpV6ConfigExtHeaderFilter

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpV6ConfigExtHeaderFilter|
|描述|This container describes the white list for the filtering of IPv6 extension headers, i.e. frames containing IPv6 extension headers not listed here shall be silently dropped.|
|描述|概述：TcpIpIpV6ConfigExtHeaderFilter 配置项用于定义IPv6通信中，哪些扩展头部应当被过滤或处理，以确保网络栈正确处理接收到的IPv6数据包。|
|描述|注意：在配置过滤规则时，需要确保与网络安全策略和性能要求相符合；过滤不当可能会导致有效数据包被错误丢弃。|
|描述|该配置项未使用|
|多实例个数|0 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6ConfigExtHeaderFilterEntry|
|描述|IPv6 Extension Header type allowed by this filter.|
|描述|概述：TcpIpIpV6ConfigExtHeaderFilterEntry配置项用于定义IPv6通信中，对特定扩展头的过滤规则，以决定哪些类型的扩展头应当被接受或拒绝。|
|描述|注意：在配置过滤规则时，需确保与网络安全策略一致；不正确的过滤配置可能导致合法数据包被错误地拒绝。|
|描述|该配置项未使用|
|多实例个数|1 - inf|
|取值范围|0 - 255|

##### 1.3.2.4. TcpIpIpV6FragmentationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpIpV6FragmentationConfig|
|描述|Specifies the configuration parameters of IPv6 packet fragmentation/reassembly.|
|描述|概述：TcpIpIpV6FragmentationConfig 是一个配置参数，用于定义TCP/IP协议栈中IPv6分片的相关配置，包括是否启用IPv6分片和分片的相关参数。|
|描述|注意：IPv6分片可能会受到限制或不被推荐使用，因为它可能会影响网络性能和安全性；配置时应确保与网络通信需求和硬件能力相匹配；在设计系统时应考虑到IPv6的路径最大传输单元（PMTU）发现机制，以避免不必要的分片。|
|描述|该配置项未使用|
|说明|此容器可被多个 IPv6 实例引用，以共享相同的配置；若不同的 IPv6 实例需要各自不同的配置，则可为此容器创建多个实例。|
|多实例个数|0 - inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpIpV6ReassemblyTimeout|
|描述|[RFC2460 4.5 Fragment Header]|
|描述|概述：TcpIpIpV6ReassemblyTimeout 配置项用于定义IPv6数据包重组过程中等待接收完整数据包的最大时间，超时后未完成重组的数据包将被丢弃。|
|描述|注意：该值应根据网络条件和应用需求合理设置，以避免因超时过短而频繁丢弃数据包；同时，过长的超时时间可能会导致系统资源（如内存）被长时间占用。|
|描述|该配置项未使用|
|说明|Default: 60 seconds|
|多实例个数|0 - 1|
|默认值|60|
|取值范围|0.001 - 100|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6ReassemblyBufferCount|
|描述|Number of buffers that can be used for fragment reassembly. In case of a reassembly error or if not all fragments are received in time this buffer will be blocked until the specified "Fragment Reassembly Timeout" has been exceeded.|
|描述|概述：TcpIpIpV6ReassemblyBufferCount 配置项用于指定IPv6协议栈中重组缓冲区的数量，这些缓冲区用于存储和重组分片化的IPv6数据包，直到它们可以完整地处理。|
|描述|注意：在配置此参数时，需要考虑系统可能同时处理的IPv6分片数据包的最大数量；配置的缓冲区数量不应超过系统资源允许的最大值；此参数的配置应与网络的通信量和系统的内存资源相匹配，以避免内存浪费或缓冲区不足。|
|描述|该配置项未使用|
|说明|值为 0 时禁用分片重组。为了发送大于路径 MTU 的数据包，节点可在源端使用 IPv6 分片头对该数据包进行分片，并在目的地重新组装。然而，对于任何能够根据测得的路径 MTU（即最低可达 1280 八位字节）调整其数据包大小的应用，都不建议使用此类分片。|
|多实例个数|1 - 1|
|默认值|2|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6ReassemblyBufferSize|
|描述|[RFC2460 5. Packet Size Issues]|
|描述|概述：TcpIpIpV6ReassemblyBufferSize 配置项用于定义IPv6协议栈中用于重组分片IPv6数据包的缓冲区大小，确保能够处理和重组接收到的IPv6分片。|
|描述|注意：缓冲区大小应足够大以容纳最大可能的分片数据包；过小的缓冲区可能导致无法重组大型数据包，而过大的缓冲区则可能浪费系统资源；在配置时还需考虑系统的内存限制和网络通信的实际需求。|
|描述|该配置项未使用|
|说明|节点必须能够接受在重新组装后大小可达 1500 八位字节的分片数据包；节点也允许接受重新组装后超过 1500 八位字节的分片数据包。测得的路径 MTU（即最低可降至 1280 八位字节）。|
|多实例个数|0 - 1|
|默认值|1500|
|取值范围|1500 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6ReassemblySegmentCount|
|描述|Specifies the maximum number of consecutive data segments that can be managed in each reassembly buffer. If all fragments are received in order, only one segment will be needed.|
|描述|概述：TcpIpIpV6ReassemblySegmentCount 配置项用于指定IPv6协议栈在重组IPv6分段时能够处理的最大分段数量，这是为了支持IPv6数据包的分段和重组功能。|
|描述|注意：该值必须足够大以支持网络通信中预期的最大分段数；过小的值可能导致无法正确重组分段数据包；在资源受限的系统中，需要平衡内存使用和网络性能。|
|描述|该配置项未使用|
|说明|为了处理乱序接收的分片，该值应配置为大于 1。|
|多实例个数|0 - 1|
|默认值|5|
|取值范围|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6TxFragmentBufferCount|
|描述|These buffers will be used if the IpV6 receives packets from the upper layer that do not fit into the MTU and thus must be fragmented.|
|描述|概述：TcpIpIpV6TxFragmentBufferCount 配置项用于指定IPv6传输层在发送分片数据包时可用的缓冲区数量，这影响着能够同时处理的分片数据包的数量。|
|描述|注意：在配置此项时，需要考虑系统的内存资源和网络通信的需求；过多的缓冲区可能会消耗较多内存，而过少可能导致网络传输效率降低；此配置项的合理设置应基于网络负载和硬件能力的评估。|
|描述|该配置项未使用|
|说明|值为 0 时禁用发送分片。如果上层传输的数据包无法适配链路或路径 MTU，IPv6 会将该数据包拆分为多个分片。参见“启用分片重组”。|
|多实例个数|1 - 1|
|默认值|2|
|取值范围|1 - 1000|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpIpV6TxFragmentBufferSize|
|描述|Size of each fragment tx buffer in bytes|
|描述|概述：TcpIpIpV6TxFragmentBufferSize定义了用于IPv6传输的TCP/IP协议栈中，发送数据包时可用的最大片段缓冲区大小。|
|描述|注意：该配置项的大小直接影响数据包的发送性能和效率；过大或过小的缓冲区大小可能导致内存浪费或数据传输延迟；需根据网络条件和应用需求合理配置缓冲区大小。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|1500|
|取值范围|1500 - 65535|

##### 1.3.2.5. TcpIpNdpConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpConfig|
|描述|Specifies the configuration parameters of the Neighbor Discovery Protocol for IPv6|
|描述|概述：TcpIpNdpConfig 是用于配置网络发现协议（Neighbor Discovery Protocol, NDP）的参数，这些参数控制着IPv6网络中的地址解析和路由发现等功能。|
|描述|注意：在配置TcpIpNdpConfig时，需要确保参数符合IPv6网络的要求和AUTOSAR CP 4.4标准；参数设置应考虑网络的实际情况，如网络大小和通信频率；不当的配置可能导致网络通信效率低下或地址解析失败。|
|描述|该配置项未使用|
|说明|本容器可由多个 IPv6 实例引用，以便它们共享相同的配置；若不同的 IPv6 实例需要各自不同的配置，则可为本容器创建多个实例。|
|多实例个数|0 - inf|

###### 1.3.2.5.1. TcpIpNdpArNudConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpArNudConfig|
|描述|Specifies the configuration parameters for NDP Address Resolution and Neighbor Unreachability Detection.|
|描述|概述：TcpIpNdpArNudConfig是用于配置邻居不可达性检测（Neighbor Unreachability Detection, NUD）的参数，这是IPv6网络中的一项机制，用于监测邻居节点的可达性状态。|
|描述|注意：在配置TcpIpNdpArNudConfig时，需要确保参数设置符合网络的实际需求和特性；不正确的配置可能导致网络通信不稳定或中断。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpDefensiveProcessing|
|描述|If enabled the NDP shall only process Neighbor Advertisements which are received in reaction to a previously transmitted Neighbor Solicitation as well as skipping updates to the Neighbor Cache based on received Neighbor Solicitations. If disabled all Neighbor Advertisements and Solicitations shall be processed as specified in RFC4861.|
|描述|概述：TcpIpNdpDefensiveProcessing配置项用于定义网络数据包处理过程中的防御机制，以提高网络通信的安全性和可靠性。|
|描述|注意：对于IPv6网络配置，需要特别注意该配置项的启用状态，以确保网络层面的安全防护；不当的配置可能导致网络性能下降或安全漏洞；建议仅在面临网络安全威胁时启用该功能。|
|描述|该配置项未使用|
|说明|[RFC4861 7.2.5. Receipt of Neighbor Advertisements]|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpNeighborUnreachabilityDetectionEnabled|
|描述|Neighbor Unreachability Detection is used to remove unused entries from the neighbor cache. This feature is a basic feature of NDP and should be turned on.|
|描述|概述：TcpIpNdpNeighborUnreachabilityDetectionEnabled 是一个配置参数，用于启用或禁用网络层的邻居不可达性检测（Neighbor Unreachability Detection, NUD）功能，这是IPv6网络中的一项机制，用于确定目标节点是否仍然可达。|
|描述|注意：在配置此项时，应确保它与网络的实际需求和策略相匹配；不正确的配置可能导致网络连接问题。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpPacketQueueEnabled|
|描述|Enables (TRUE) or disables (FALSE) support of a NDP Packet Queue according to IETF RFC 4861, section 7.2.2.|
|描述|概述：TcpIpNdpPacketQueueEnabled 配置项用于启用或禁用网络数据包队列，特别是针对邻居发现协议（NDP）的数据包，这有助于管理IPv6网络中的数据流量。|
|描述|注意：需要确保此配置项与IPv6堆栈的实现和需求相匹配；如果不使用IPv6或者不需要NDP队列管理功能，可以禁用此选项以节省资源；正确配置此项对于网络性能和资源管理至关重要。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpRandomReachableTimeEnabled|
|描述|If enabled the value of ReachableTime will be multiplied with a random value between MIN_RANDOM_FACTOR and MAX_RANDOM_FACTOR in order to prevent multiple nodes from transmitting at exactly the same time|
|描述|概述：TcpIpNdpRandomReachableTimeEnabled 配置项用于启用或禁用基于随机数的可达时间计算，这是针对IPv6邻居发现协议（NDP）的一种机制，用于确定主机认为邻居是可达的时间长度。|
|描述|注意：应确保此配置项与IPv6堆栈的实现和需求相匹配；如果启用，需要有机制生成随机的可达时间，以避免网络同步问题；此配置项的使用应遵循网络设计的安全和性能考虑。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.2. Host Variables / ReachableTime]|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpDefaultReachableTime|
|描述|Configuration of the ReachableTime (s) specified in [RFC4861 6.3.2. Host Variables].|
|描述|概述：TcpIpNdpDefaultReachableTime 是一个配置参数，用于指定网络接口在认为邻居节点是可达的默认时间（以毫秒为单位），这是IPv6邻居发现协议（NDP）的一部分。|
|描述|注意：该值通常是一个推荐的默认值，但可以根据网络条件进行调整；过小的值可能导致频繁的邻居可达性确认，而过大的值可能导致网络变化反应不及时。|
|描述|该配置项未使用|
|说明|“在收到可达性确认后，邻居被视为可达的时间。”如果选中 TcpIpNdpDynamicReachableTimeEnabled，则该值可根据接收到的路由通告重新配置。默认值：REACHABLE_TIME = 30 秒。|
|多实例个数|1 - 1|
|默认值|30|
|取值范围|0 - 120|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpDefaultRetransTimer|
|描述|Configures the default value (s) for the RetransTimer variable specified in [RFC4861 6.3.2. Host Variables].|
|描述|概述：TcpIpNdpDefaultRetransTimer配置项定义了在Neighbor Discovery协议中，当等待邻居确认消息时，默认的消息重传时间间隔。|
|描述|注意：该时间间隔的配置对网络的响应时间和负载有直接影响；值设置过小可能导致网络拥堵，过大可能导致响应延迟；需根据网络环境和性能要求谨慎配置。|
|描述|该配置项未使用|
|说明|“在解析地址或探测邻居可达性时，向邻居重传 Neighbor Solicitation 消息之间的时间间隔。”如果选中 TcpIpNdpDynamicRetransTimeEnabled，则该值可根据接收到的路由器通告重新配置。默认值：RETRANS_TIMER = 1 秒。|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 60|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpDelayFirstProbeTime|
|描述|Delay before sending the first NUD probe in (s).|
|描述|概述：TcpIpNdpDelayFirstProbeTime配置项用于定义在Neighbor Discovery协议中，从地址解析开始到发送第一个Neighbor Solicitation消息之间的延迟时间。|
|描述|注意：该配置项的值应根据网络的具体需求和性能目标进行调整；过小的值可能导致网络拥塞，过大的值可能导致延迟过高。|
|描述|该配置项未使用|
|说明|[RFC4861 7.3.3. Node Behavior] Default: DELAY_FIRST_PROBE_TIME = 5 seconds|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|0 - 60|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpMaxNeighborCacheSize|
|描述|Maximum number of entries in the neighbor cache.|
|描述|概述：TcpIpNdpMaxNeighborCacheSize定义了在IPv6网络中，TCP/IP协议栈能够缓存的最大邻居发现协议（NDP）条目的数量，用于优化网络通信效率。|
|描述|注意：该配置项的值应根据网络的规模和通信频率进行合理设置，以避免缓存溢出或资源浪费；在资源受限的嵌入式系统中，过大的缓存大小可能会影响系统性能。|
|描述|该配置项未使用|
|说明|[RFC4861 5.1. Conceptual Data Structures]|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|1 - 254|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpMaxRandomFactor|
|描述|Maximum random factor used for randomization|
|描述|概述：TcpIpNdpMaxRandomFactor 配置项用于定义Neighbor Discovery协议中重传时间间隔的最大随机因子，这个因子用于计算消息重传的时间间隔，以减少网络上的冲突和拥塞。|
|描述|注意：该值通常是一个大于1的浮点数，用于乘以基础重传时间间隔以得到最大重传时间；配置值应遵循RFC 4861中的建议；在实际应用中，需要根据网络的具体情况调整该值以优化网络性能。|
|描述|该配置项未使用|
|说明|[RFC4861 10. Protocol Constants] Default: 15 (MAX_RANDOM_FACTOR = 1.5)|
|多实例个数|1 - 1|
|默认值|15|
|取值范围|0 - 100|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpMinRandomFactor|
|描述|Minimum random factor used for randomization|
|描述|概述：TcpIpNdpMinRandomFactor配置项用于定义Neighbor Discovery协议中重传时间间隔的最小随机因子，以避免网络上的多个节点在相同时间重发消息，减少网络冲突。|
|描述|注意：该配置项的值应小于或等于TcpIpNdpMaxRandomFactor的值，以保证重传时间间隔的随机性有效；在设置时考虑网络的实际情况和性能要求；AUTOSAR CP 4.4标准中对此参数的具体数值范围没有特别限制，但建议根据网络规模和通信需求谨慎选择。|
|描述|该配置项未使用|
|说明|[RFC4861 10. Protocol Constants] Default: 5 (MIN_RANDOM_FACTOR = 0.5)|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|0 - 100|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpNumMulticastSolicitations|
|描述|Maximum number of multicast solicitations that will be sent when performing address resolution.|
|描述|概述：TcpIpNdpNumMulticastSolicitations配置项定义了在确定邻居不可达之前，发送多播邻居请求消息的最大次数。|
|描述|注意：该值必须大于0；过低的值可能导致在高丢包环境下无法可靠地发现邻居，而过高的值可能导致网络拥塞。|
|描述|该配置项未使用|
|说明|[RFC4861 7.2.2. Sending Neighbor Solicitations] Default: MAX_MULTICAST_SOLICIT = 3|
|多实例个数|1 - 1|
|默认值|3|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpNumUnicastSolicitations|
|描述|Maximum number of unicast solicitations that will be sent when performig Neighbor Unreachability Detection.|
|描述|概述：TcpIpNdpNumUnicastSolicitations 配置项定义了在IPv6网络中，为了确定一个单播地址的可达性，发送的单播邻居请求消息的数量。|
|描述|注意：该值通常是一个小的正整数，根据网络的具体需求进行配置；过高的值可能导致网络拥塞，而过低的值可能导致地址解析不可靠。|
|描述|该配置项未使用|
|说明|[RFC4861 7.3.3. Node Behavior] Default: MAX_UNICAST_SOLICIT = 3|
|多实例个数|1 - 1|
|默认值|3|
|取值范围|0 - 255|

###### 1.3.2.5.2. TcpIpNdpPrefixRouterDiscoveryConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpPrefixRouterDiscoveryConfig|
|描述|Specifies the configuration parameters for NDP Prefix and Router Discovery.|
|描述|概述：TcpIpNdpPrefixRouterDiscoveryConfig配置项用于定义网络层的IPv6邻居发现协议（NDP）中前缀和路由器发现相关的参数，以便正确处理IPv6地址的自动配置和维护。|
|描述|注意：在配置此项时，必须确保IPv6网络环境下的兼容性和正确性；该配置对网络性能和通信安全性有直接影响，应谨慎设置。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpDynamicHopLimitEnabled|
|描述|If enabled the default hop limit may be reconfigured based on received Router Advertisements.|
|描述|概述：TcpIpNdpDynamicHopLimitEnabled 是一个配置项，用于启用或禁用基于邻居发现协议（NDP）动态确定IPv6数据包的跳数限制（Hop Limit）的功能。|
|描述|注意：此配置项应当与IPv6和NDP相关的模块配置保持一致；如果网络栈不需要动态确定跳数限制，该选项应设置为禁用；在启用此功能时，需要确保网络栈正确实现了NDP相关的规范。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.4. Processing Received Router Advertisements]|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpDynamicMtuEnabled|
|描述|Allow dynamic reconfiguration of link MTU via Router Advertisements.|
|描述|概述：TcpIpNdpDynamicMtuEnabled 配置项用于启用或禁用网络层发现协议（NDP）的动态最大传输单元（MTU）发现功能，这是IPv6网络中用于确定最优MTU大小的机制。|
|描述|注意：需要确保此配置项与IPv6网络堆栈的其他设置兼容；如果启用，网络性能可能会因适应不同网络路径的MTU而提高，但也可能增加网络管理的复杂性；禁用时，系统将使用静态MTU值，可能不是最优的网络路径MTU，但配置简单。|
|描述|该配置项未使用|
|说明|[RFC4861 4.6.4. MTU]|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpDynamicReachableTimeEnabled|
|描述|If enabled the default Reachable Time value may be reconfigured based on received Router Advertisements.|
|描述|概述：TcpIpNdpDynamicReachableTimeEnabled 是一个配置项，用于启用或禁用基于网络条件动态调整IPv6邻居发现协议（NDP）的可达时间的功能。|
|描述|注意：应确保此配置项与IPv6堆栈的实现和网络需求相匹配；如果启用，需要有相应的算法来动态调整可达时间；在禁用时，系统将使用静态的可达时间配置。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.4. Processing Received Router Advertisements] Default: Enabled|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpDynamicRetransTimeEnabled|
|描述|If enabled the default Retransmit Timer value may be reconfigured based on received Router Advertisements.|
|描述|概述：TcpIpNdpDynamicRetransTimeEnabled 是一个配置参数，用于启用或禁用TCP/IP协议栈中邻居发现协议（NDP）的动态重传计时器功能，该功能允许根据网络条件调整NDP消息的重传时间间隔。|
|描述|注意：应确保此配置项与网络堆栈的实际需求和性能目标相匹配；不正确的配置可能会影响网络通信的效率和可靠性；在配置此项时，还应考虑与其他网络参数的相互作用和依赖性。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.4. Processing Received Router Advertisements] Default: Enabled|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpRndRtrSolicitationDelayEnabled|
|描述|If enabled the first router solicitation will be delayed randomly from [0...MAX_RTR_SOLICITATION_DELAY]. Otherwise the first router solicitation will be sent after exactly MAX_RTR_SOLICITATION_DELAY milliseconds.|
|描述|概述：TcpIpNdpRndRtrSolicitationDelayEnabled 是一个配置项，用于启用或禁用在发送初始路由器请求消息之前的随机延迟，这有助于减少网络上的请求冲突。|
|描述|注意：在配置此项时，应确保它与网络需求和性能目标相匹配；如果启用，需要设置合适的随机延迟范围；在高密度网络或启动时网络活动较高的场景中，此功能特别有用。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.7. Sending Router Solicitations] Default: Enabled|
|多实例个数|1 - 1|
|默认值|true|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpMaxRtrSolicitationDelay|
|描述|Maximum delay before the first Router Solicitation will be sent after interface initialization in (s).|
|描述|概述：TcpIpNdpMaxRtrSolicitationDelay配置项定义了在发送初始路由器请求消息之前等待的最大时间，用于IPv6网络中确定可用路由器的存在。|
|描述|注意：该值必须根据网络的具体需求和性能考虑进行配置；过小的值可能导致网络拥塞，过大的值可能导致网络启动延迟。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.7. Sending Router Solicitations] Default: MAX_RTR_SOLICITATION_DELAY = 1 second|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0.001 - 60|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpRtrSolicitationInterval|
|描述|Interval between consecutive Router Solicitations in (s).|
|描述|概述：TcpIpNdpRtrSolicitationInterval配置项定义了在IPv6网络中，节点发送路由器请求消息（Router Solicitation messages）的时间间隔，用于发现网络中的路由器设备。|
|描述|注意：该时间间隔值必须遵守RFC 4861中定义的最小和最大间隔限制；不正确的配置可能导致网络连接延迟或中断；在动态网络环境中，应考虑调整此值以优化网络性能。|
|描述|该配置项未使用|
|说明|[RFC4861 6.3.7. Sending Router Solicitations] Default: RTR_SOLICITATION_INTERVAL = 4 seconds|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|0.001 - 60|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpDefaultRouterListSize|
|描述|Maximum number of default router entries.|
|描述|概述：TcpIpNdpDefaultRouterListSize 配置项用于定义网络层邻居发现协议（NDP）中默认路由器列表的大小，这个列表用于存储IPv6网络中可用的默认路由器信息。|
|描述|注意：在配置时需要确保列表大小足以容纳网络中所有必要的默认路由器；过大的列表可能会浪费内存资源，而过小的列表可能导致无法存储所有有效的路由器信息。|
|描述|该配置项未使用|
|说明|[RFC4861 5.1. Conceptual Data Structures]|
|多实例个数|1 - 1|
|默认值|2|
|取值范围|2 - 254|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpDestinationCacheSize|
|描述|Maximum number of entries in the destination cache.|
|描述|概述：TcpIpNdpDestinationCacheSize配置项用于定义网络层中IPv6邻居发现协议（NDP）的目的地缓存大小，这个缓存用于存储目的地的地址解析信息，以加快数据包的传输。|
|描述|注意：在配置TcpIpNdpDestinationCacheSize时，需要考虑网络的规模和通信频率，以确保缓存大小既能满足性能需求又不会过度占用系统资源；此配置项对于优化网络性能至关重要，但设置过大可能会导致不必要的内存消耗。|
|描述|该配置项未使用|
|说明|[RFC4861 5.1. Conceptual Data Structures]|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|1 - 254|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpMaxRtrSolicitations|
|描述|Maximum number of Router Solicitations that will be sent before the first Router Advertisement has been received.|
|描述|概述：TcpIpNdpMaxRtrSolicitations配置项定义了在确定网络接口的可达性时，节点发送Router Solicitation消息的最大次数。|
|描述|注意：该值应根据网络的具体需求和性能考虑进行配置；过高的值可能导致网络拥塞，而过低的值可能导致节点无法及时发现路由器。|
|描述|该配置项未使用|
|说明|0 = No Router Solicitations will be sent. This has no impact on handling Router Advertisements. [RFC4861 6.3.7. Sending Router Solicitations] Default: MAX_RTR_SOLICITATIONS = 3 transmissions|
|多实例个数|1 - 1|
|默认值|3|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpPrefixListSize|
|描述|Maximum number of entries in the on-link prefix list.|
|描述|概述：TcpIpNdpPrefixListSize 配置项用于定义网络接口上Neighbor Discovery Protocol（NDP）前缀列表的大小，这个列表包含了IPv6地址前缀，用于地址自动配置和地址解析。|
|描述|注意：在配置TcpIpNdpPrefixListSize时，需要确保列表大小能够满足网络接口上可能出现的前缀数量；过大的列表可能会浪费资源，而过小的列表可能导致地址配置失败；此配置项应与网络的实际需求和IPv6地址规划相匹配。|
|描述|该配置项未使用|
|说明|[RFC4861 5.1. Conceptual Data Structures]|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|1 - 254|

####### 1.5.2.5.2.1. TcpIpNdpPrefixList

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpPrefixList|
|描述|Specifies a list of prefixes to be treated as "on-link" according to IETF RFC 4861 Section 5.1.|
|描述|概述：TcpIpNdpPrefixList配置项用于定义网络中的IPv6地址前缀列表，这些前缀用于自动配置网络设备的IPv6地址和识别网络中的地址范围。|
|描述|注意：在配置IPv6网络参数时，确保前缀长度和值正确匹配网络设计要求；前缀信息通常由网络管理员或自动配置协议如NDP（邻居发现协议）提供。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

######## 1.5.2.5.2.1.1. TcpIpNdpPrefixListEntry

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpPrefixListEntry|
|描述|Single entry in the prefix list.|
|描述|概述：TcpIpNdpPrefixListEntry 配置项用于定义IPv6网络中的前缀列表条目，这些条目用于Neighbor Discovery Protocol (NDP) 来管理地址自动配置和路由选择。|
|描述|注意：在配置TcpIpNdpPrefixListEntry时，需要确保前缀长度和前缀地址的有效性，以符合IPv6地址规范；此外，要注意前缀信息的一致性，以避免网络通信中的冲突或错误。|
|描述|该配置项未使用|
|多实例个数|1 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpPrefixListEntryPrefixLength|
|描述|The number of leading bits in the Prefix that are valid.|
|描述|概述：TcpIpNdpPrefixListEntryPrefixLength定义了在Neighbor Discovery Protocol（NDP）中使用的网络前缀的长度，用于IPv6地址的自动配置和网络地址的管理。|
|描述|注意：前缀长度应在1到128之间，以适应IPv6地址的结构；配置时需确保与网络实际使用的前缀长度一致，避免地址配置错误或冲突。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 128|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpNdpPrefixListEntryPrefixAddress|
|描述|The prefix of an IP address. This prefix can be used for on-link determination.|
|描述|概述：TcpIpNdpPrefixListEntryPrefixAddress 配置项用于定义IPv6网络中的前缀地址，这个地址用于自动配置和地址解析过程中，它是Neighbor Discovery Protocol (NDP) 的一部分。|
|描述|注意：在配置IPv6地址时，必须确保前缀地址的格式正确且与网络设置相匹配；前缀长度通常是64位，但应根据具体网络要求进行设置。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

###### 1.3.2.5.3. TcpIpNdpSlaacConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNdpSlaacConfig|
|描述|Specifies the configuration parameters for StateLess Address AutoConfiguration.|
|描述|概述：TcpIpNdpSlaacConfig 是一个配置参数，用于定义TCP/IP协议栈中IPv6无状态地址自动配置（SLAAC）的相关属性，这包括地址生成、有效期和其他与SLAAC相关的配置。|
|描述|注意：在配置TcpIpNdpSlaacConfig时，需要确保IPv6网络的正确性和地址的唯一性；此外，应当注意与网络硬件和操作系统的兼容性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpSlaacDelayEnabled|
|描述|If enabled transmission of the first DAD Neighbor Solicitation will be delayed by a random value from [0...MAX_DAD_DELAY].|
|描述|概述：TcpIpNdpSlaacDelayEnabled 是一个配置项，用于启用或禁用基于邻居发现协议（NDP）的无状态地址自动配置（SLAAC）的随机延迟机制，以减少网络上的冲突。|
|描述|注意：在配置此项时，应考虑网络的具体需求和行为；如果启用，需要确保随机延迟的时间范围符合网络性能要求；在某些实时性要求较高的系统中，可能需要禁用此功能以避免不确定的延迟。|
|描述|该配置项未使用|
|说明|该机制可在许多节点同时在链路上启动（例如断电恢复后）时缓解拥塞，并可在多个节点同时尝试对同一地址发起请求时帮助避免竞争条件。该延迟亦可在多个节点通过接收同一组播路由器通告来配置地址时，避免类似的拥塞。”【RFC4861 第 5.4.2 节 “发送 Neighbor Solicitation 消息”】
默认：True。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpNdpSlaacOptimisticDadEnabled|
|描述|Enable Optimistic Duplicate Address Detection (DAD) according to RFC4429.|
|描述|概述：TcpIpNdpSlaacOptimisticDadEnabled 是一个配置选项，用于启用或禁用在使用无状态地址自动配置(SLAAC)时进行乐观的重复地址检测(DAD)过程。|
|描述|注意：乐观的DAD是一个可选特性，它允许设备在地址验证过程还未完成时就开始使用该地址；这可能会提高网络接口的设置速度，但也可能增加地址冲突的风险；在配置此选项时，应当考虑网络的安全性和稳定性需求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|TcpIpNdpSlaacDadRetransmissionDelay|
|描述|Sets the maximum value for the address configuration delay (s).|
|描述|概述：TcpIpNdpSlaacDadRetransmissionDelay 配置项用于指定在使用无状态地址自动配置(SLAAC)时，网络协议栈在发送重复地址检测(DAD)消息之间的等待时间。|
|描述|注意：该值应根据网络的具体条件和性能要求进行配置；过小的重传延迟可能导致网络拥塞，而过大的延迟可能导致配置过程不必要的延长；在配置此参数时，应遵循RFC 4861中关于DAD的建议和要求。|
|描述|该配置项未使用|
|说明|“根据 [RFC4861 第 5.4.2 节 ‘发送 Neighbor Solicitation 消息’]，此值应与 MAX_RTR_SOLICITATION_DELAY 相同。默认值：MAX_RTR_SOLICITATION_DELAY = 1 秒。”|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 10|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpNdpSlaacDadNumberOfTransmissions|
|描述|Number of Neighbor Solicitations that have to be unanswered in order to set an autoconfigurated address to PREFERRED (usable) state.|
|描述|概述：TcpIpNdpSlaacDadNumberOfTransmissions配置项定义了在无状态地址自动配置(SLAAC)过程中，为验证IPv6地址的唯一性而发送的邻居发现协议(NDP)重复地址检测(DAD)消息的数量。|
|描述|注意：该值应根据网络的具体需求和性能考虑进行配置；设置过低可能导致地址冲突未被检测到，设置过高可能导致网络启动延迟。|
|描述|该配置项未使用|
|说明|[RFC4861 第 5.1 节：节点配置变量]默认值：DupAddrDetectTransmits = 1。
将此值设置为 0 可关闭重复地址检测 (DAD)。|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 254|

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

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpLocalAddrIPv6ExtHeaderFilterRef|
|描述|Reference to a set of IPv6 Extension Headers which are allowed for this local IPv6 address.|
|描述|概述：TcpIpLocalAddrIPv6ExtHeaderFilterRef 是一个配置项，用于引用IPv6扩展头过滤器的定义，该过滤器决定了哪些IPv6扩展头将被本地地址接受或忽略。|
|描述|注意：在配置时需要确保引用的IPv6扩展头过滤器已经定义；此配置项对于IPv6通信至关重要，错误的配置可能导致通信问题。|
|描述|该配置项未使用|
|说明|Note: this parameter is only relevant if the related TcpIpDomainType is TCPIP_AF_INET6.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpIpConfig/TcpIpIpV6Config/TcpIpIpV6ConfigExtHeaderFilter|

#### 1.6.1. TcpIpAddrAssignment

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

#### 1.6.2. TcpIpStaticIpAddressConfig

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

### 1.5. TcpIpNvmBlock

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpNvmBlock|
|描述|Configuration of optional usage of Nvm in case the TcpIp module requires non volatile memory in the Ecu to store information (e.g. IP Address received via DHCP and shall be stored).|
|描述|概述：TcpIpNvmBlock配置项用于定义TCP/IP模块中需要持久化存储的数据块，如IP地址配置、网关地址等，以保证系统在重启后能够恢复网络配置。|
|描述|注意：需要确保NvmBlock描述符与实际的非易失性存储区域匹配；持久化数应仅包含对系统恢复至正常工作状态必要的配置；对于动态分配的IP地址，应考虑其在系统重启后的恢复策略。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpNvmBlockDescriptorRef|
|描述|Reference to the Nvm block description in the Nvm module configuration.|
|描述|概述：TcpIpNvmBlockDescriptorRef 是一个配置项，用于引用网络管理向量（NVM）块描述符，该描述符定义了TCP/IP模块所需的非易失性存储数据。|
|描述|注意：在配置TcpIpNvmBlockDescriptorRef时，必须确保引用的NVM块描述符已经在系统中定义且与TCP/IP模块的存储需求相匹配；此外，需要注意NVM块的读写权限和存储时机，以确保TCP/IP配置的正确性和数据的持久性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/NvM/NvMBlockDescriptor|

### 1.6. TcpIpPhysAddrConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpPhysAddrConfig|
|描述|Specifies the physical address configuration.|
|描述|概述：TcpIpPhysAddrConfig配置项用于定义TCP/IP协议栈中网络接口的物理地址（如MAC地址）配置，包括静态或动态分配的物理地址。|
|描述|注意：物理地址应遵循网络硬件的规范和标准；在配置动态物理地址时，需确保地址的唯一性和冲突避免机制。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

#### 1.6.1. TcpIpPhysAddrChgHandler

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpPhysAddrChgHandler|
|描述|This container is a subcontainer of TcpIpPhysAddrConfig and|
|描述|概述：TcpIpPhysAddrChgHandler是一个配置项，用于指定当TCP/IP协议栈的物理地址（如MAC地址）发生变化时调用的回调函数，以便于上层软件组件能够响应这一变化。|
|描述|注意：在配置TcpIpPhysAddrChgHandler时应当考虑物理地址变更的影响范围，确保相关网络层和应用层组件能够正确处理地址变更事件；在实际部署时，还需注意硬件支持和网络管理策略，以确保物理地址变更能够被正确检测和处理。|
|描述|该配置项未使用|
|说明|specifies the configuration parameters for physical address change handler.|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpPhysAddrChgHandlerName|
|描述|This parameter defines the name of the physical address change function <Up>_PhysAddrTableChg.|
|描述|概述：TcpIpPhysAddrChgHandlerName配置项用于指定一个回调函数的名称，该函数在网络接口的物理地址（如MAC地址）发生变化时被调用，以便执行必要的更新或处理。|
|描述|注意：物理地址变化可能来源于多种原因，如网络管理策略变更，因此需要仔细设计处理逻辑；在配置此项时，应确保网络堆栈已正确初始化并且能够处理地址变更事件。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

### 1.7. TcpIpSocketOwnerConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpSocketOwnerConfig|
|描述|Specifies the upper layer modules of TcpIp using the socket API.|
|描述|概述：TcpIpSocketOwnerConfig配置项用于定义TCP/IP协议栈中的套接字所有者信息，包括所有者的标识符和其所拥有的套接字的配置。|
|描述|注意：确保每个套接字所有者的标识符在系统中是唯一的；配置时需考虑系统中所有网络通信需求，以避免资源冲突。|
|多实例个数|1 - 1|

#### 1.7.1. TcpIpSocketOwner

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

### 1.7. TcpIpTcpConfig

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

#### 1.7.1. TcpIpTcpConfigOptionFilter

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTcpConfigOptionFilter|
|描述|This container describes the white list for the filtering of TCP options, i.e. segments containing TCP options not listed here shall be silently dropped.|
|描述|概述：TcpIpTcpConfigOptionFilter 配置项用于定义TCP/IP协议栈中，对于TCP头部中的选项字段进行过滤的参数，以控制哪些选项可以被接受或者需要被忽略。|
|描述|注意：在配置TcpIpTcpConfigOptionFilter时，需要确保所选的过滤规则与系统的安全性和性能要求相匹配；不正确的过滤设置可能会导致网络通信中的安全漏洞或性能问题；此配置项应与网络通信的具体需求和网络环境紧密结合，以确保正确的TCP选项被处理。|
|描述|该配置项未使用|
|多实例个数|0 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpConfigOptionFilterEntry|
|描述|TCP option kind allowed by this filter.|
|描述|概述：TcpIpTcpConfigOptionFilterEntry 配置项用于定义TCP/IP协议栈中TCP连接的选项过滤，它决定了哪些TCP选项应当被接受或忽略，以确保网络通信的安全性和兼容性。|
|描述|注意：在配置TcpIpTcpConfigOptionFilterEntry时，需要确保所选的TCP选项与网络通信的安全策略和性能要求相匹配；此外，过滤不当的TCP选项可能会导致网络连接问题。|
|描述|该配置项未使用|
|多实例个数|0 - inf|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTcpConfigOptionFilterId|
|描述|Identification of the TCP option filter.|
|描述|None|
|多实例个数|1 - 1|
|取值范围|0 - 255|

### 1.8. TcpIpTlsConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsConfig|
|描述|Specifies the configuration parameters of the TLS (Transport Layer Security) sub module.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConfig 是用于配置传输层安全（TLS）的参数，这些参数控制着基于TCP/IP协议栈的安全通信，确保数据传输的机密性和完整性。|
|描述|注意：在配置TcpIpTlsConfig时，需要确保选择合适的加密套件和密钥交换方法以满足安全性要求；还需注意证书的管理，包括证书的存储、分发和撤销机制。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsMaxConnections|
|描述|Defines the max. number of TLS connections that can be opened at the same time.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsMaxConnections 配置项定义了TCP/IP 栈中可以同时建立的最大TLS连接数量，这个参数限制了可以进行加密通信的并发连接数。|
|描述|注意：该值应根据系统资源和应用需求进行配置，以确保既不会因资源限制导致连接失败，也不会因分配过多资源而浪费；在配置时需要考虑系统的内存和处理能力，以及预期的网络负载；超出此配置数量的TLS连接请求将被拒绝，因此需要确保此值符合系统的最大预期并发TLS连接需求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmRandomGenerateJobRef|
|描述|Reference to a CSM job to generate a random value.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmRandomGenerateJobRef 配置项用于指定用于TLS（传输层安全协议）的随机数生成的加密服务管理器（CSM）作业引用，确保TLS握手过程中的随机性和安全性。|
|描述|注意：在配置TcpIpTlsCsmRandomGenerateJobRef时，必须确保引用的CSM作业能够提供足够的随机性以满足TLS协议的安全要求；应当检查CSM作业是否已经正确配置，包括算法、密钥长度等；此配置项应与系统中的安全策略和TLS版本兼容。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

#### 1.8.1. TcpIpTlsCiphersuites

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsCiphersuites|
|描述|This container provides the information about supported ciphersuites used by TLS.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuites配置项用于定义TCP/IP协议栈中TLS(传输层安全协议)加密套件的选择，这些加密套件决定了数据传输过程中的加密算法和密钥交换方法。|
|描述|注意：在选择加密套件时，需要确保所选套件符合项目的安全要求和性能需求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

##### 1.8.1.1. TcpIpTlsCertificateIdentity

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsCertificateIdentity|
|描述|This container provides information about the certificates used for ciphersuites.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCertificateIdentity 配置项用于定义TCP/IP协议栈中TLS（传输层安全协议）的证书身份信息，这包括证书的主体名称、签名算法、密钥交换方法等，用于确保网络通信的安全性。|
|描述|注意：在配置TcpIpTlsCertificateIdentity时，需要确保证书信息与实际的TLS证书相匹配。|
|描述|该配置项未使用|
|多实例个数|1 - inf|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpTlsServerNameIdentification|
|描述|Defines a server identification name. If present, the name will be added as an extension with the "TLS client hello" handshake message. The TLS server will check for the name to identify the server certificate.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsServerNameIdentification配置项用于定义在使用TLS（传输层安全协议）进行通信时，如何识别服务器的名称，这是实现服务器名称指示（SNI）扩展的一部分，用于在同一IP地址上支持多个TLS安全域。|
|描述|注意：需要确保服务器名称匹配证书中的名称，以避免安全警告或连接失败；此配置对于支持SNI的系统尤为重要；配置时需考虑证书管理策略和安全要求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherKeyMLocalCertificate|
|描述|Reference to a KeyM certificate used to address the local certificate.|
|描述|概述：TcpIpTlsCipherKeyMLocalCertificate 配置项用于定义TCP/IP传输层安全（TLS）的本地证书密钥材料，这是实现TLS加密通信时所需的安全凭证。|
|描述|注意：必须确保使用的密钥材料与系统的安全需求相匹配；密钥材料的存储和管理应遵循严格的安全策略；配置时应注意与TcpIpTlsCipherSuite配置项的兼容性，以确保正确的加密算法和密钥长度。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherKeyMRemoteCertificate|
|描述|Reference to KeyM certificate container to reference the remote certificate.|
|描述|概述：TcpIpTlsCipherKeyMRemoteCertificate 配置项用于定义在使用传输层安全协议（TLS）时，远程通信对方的证书信息，以便于进行身份验证和加密通信。|
|描述|注意：需要确保证书格式和密钥长度符合TLS协议和系统安全要求；证书的存储和管理应遵循安全最佳实践，防止泄露；配置时需考虑证书的有效期和更新机制，以保证通信的持续安全。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate|

##### 1.8.1.2. TcpIpTlsCiphersuiteDefinition

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsCiphersuiteDefinition|
|描述|This container provides the static information of a ciphersuite used by TLS.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuiteDefinition 配置项用于定义TCP/IP协议栈中TLS(传输层安全协议)的加密套件，这些加密套件规定了加密算法、密钥交换方法、消息认证码和伪随机函数。|
|描述|注意：在配置TcpIpTlsCiphersuiteDefinition时，需要确保选择的加密套件符合相关安全标准和法规要求；应考虑到系统的性能和资源限制，选择合适的加密套件以平衡安全性和效率；还需注意加密套件的兼容性，确保与通信双方的TLS实现相匹配。|
|描述|该配置项未使用|
|多实例个数|1 - inf|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTlsUseAEADCipher|
|描述|Specifies if the ciphersuite supports AEAD for data en-/decryption.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsUseAEADCipher 配置项指定了在使用传输层安全（TLS）协议时，是否启用基于认证加密的对称加密算法（AEAD），例如GCM（Galois/Counter Mode）或CCM（Counter with CBC-MAC）。|
|描述|注意：需要支持AEAD加密算法是为了提供更高的安全性；配置时需要确保所选的加密套件与系统的安全需求相匹配；此外，使用AEAD加密算法可能需要更多的计算资源和内存，这在资源受限的嵌入式系统中需要特别考虑。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTlsUsePresharedKeys|
|描述|Defines if this ciphersuite uses pre-shared keys. If so, additional configuration or callbacks will be used for pre-shared key negotiation.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsUsePresharedKeys 配置项用于指定TCP/IP协议栈是否使用预共享密钥（PSK）机制来建立TLS（传输层安全）连接，这是一种不依赖于证书的身份验证方法。|
|描述|注意：使用预共享密钥的TLS配置必须确保密钥的安全存储和管理；此配置可能不适用于所有的安全通信场景，因为它可能不提供与证书基础结构相同的安全级别；在实施时，应考虑与其他安全措施（如密钥更新和撤销机制）的兼容性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTlsUseSecurityExtensionForceMacThenHash|
|描述|Defines if the security extension according to IETF RFC 7366 shall be supported. This is useful for ciphersuites using CBC mode.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsUseSecurityExtensionForceMacThenHash配置项用于指定在TLS（传输层安全协议）中，是否强制使用MAC-then-Hash（消息认证码后跟哈希）的安全扩展，以增强数据传输的安全性。|
|描述|注意：此配置项对于确保数据在传输过程中的完整性和认证非常关键。如果系统对安全性要求较高，建议启用此选项。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpTlsVersion|
|描述|Declares the TLS version that this ciphersuite shall be used for.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsVersion 配置项用于指定TCP/IP协议栈中TLS (Transport Layer Security) 的版本，这决定了通信安全协议的版本，以确保数据传输的安全性和兼容性。|
|描述|注意：需要确保选择的TLS版本符合当前的安全标准和兼容性要求；过时的TLS版本可能不被支持，且可能存在安全风险；在配置时，还需考虑目标硬件和软件平台对TLS版本的支持情况。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsCiphersuiteId|
|描述|ID that represents the ciphersuite according to IETF, e.g. RFC4492, Sect. 6, RFC8446, Appendix B.4 or RFC5246, Appendix A.5.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuiteId 是一个配置项，用于指定在TCP/IP协议栈中使用的TLS（传输层安全协议）加密套件的唯一标识符，以确保数据传输的安全性。|
|描述|注意：加密套件的选择应考虑到系统的安全需求和性能影响；在配置过程中，应避免使用已被认为不安全的加密套件，以维护系统的安全性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsCiphersuitePriority|
|描述|Defines the priority of the cipher. The higher the number the lower the priority.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuitePriority 配置项用于定义TLS（传输层安全协议）加密套件在AUTOSAR TCP/IP协议栈中的优先级顺序，确保通信的安全性和性能。|
|描述|注意：优先级设置应考虑到系统的安全需求和性能影响；不同的加密套件可能需要不同的硬件支持和软件资源。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpTlsCiphersuiteName|
|描述|Provides a verbal name for the ciphersuite. The name should be the one defined in the respective RFC, e.g. TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (TLS 1.2) or TLS_AES_128_GCM_SHA256 (TLS 1.3)|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuiteName 配置项用于指定在TCP/IP协议栈中用于TLS（传输层安全协议）连接的加密套件名称，以确保数据传输的安全性。|
|描述|注意：考虑到加密套件的安全性和性能影响，选择时应权衡这些因素；还需注意与硬件加速器的兼容性，如果有的话，以确保最佳性能。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

##### 1.8.1.3. TcpIpTlsCiphersuiteWorker

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsCiphersuiteWorker|
|描述|This container provides the jobs and keys necessary for TLS data transmission and reception.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuiteWorker配置项用于定义TCP/IP协议栈中TLS（传输层安全协议）加密套件的工作参数，包括加密算法、密钥交换机制等，以确保数据传输的安全性。|
|描述|注意：需确保所选加密套件与系统安全需求相匹配；加密套件的选择应考虑到性能与安全性的平衡；在配置时应注意兼容性，确保加密套件在所有目标平台上均受支持。|
|描述|该配置项未使用|
|多实例个数|1 - inf|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsCipherAEADCipherKeyLength|
|描述|Defines the key length for en- / decryption with authentication data (AEAD).|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherAEADCipherKeyLength配置项指定了在使用TLS（传输层安全协议）进行网络通信时，AEAD（Authenticated Encryption with Associated Data）密码算法所使用的密钥长度。|
|描述|注意：密钥长度必须符合选用的AEAD密码算法的要求，以确保加密的安全性；不同的密钥长度可能会影响系统的性能，需要在安全性和性能之间做出权衡。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsCipherEncryptKeyLength|
|描述|Defines the key length used for en- or decryption. The key length is valid for (symmetric) encryption and decryption.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherEncryptKeyLength配置项定义了在使用TCP/IP协议栈的TLS加密过程中，加密密钥的长度。|
|描述|注意：密钥长度直接影响加密的强度和性能，选择时需平衡安全性和系统资源消耗；在不同地区可能存在对加密技术的法律限制，选择时需注意合规性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsCipherMacKeyLength|
|描述|Specifies the length of the MAC key|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherMacKeyLength配置项定义了在使用TLS（传输层安全协议）进行TCP/IP通信时，用于消息认证码（MAC）算法的密钥长度。|
|描述|注意：该配置项的值必须与所选MAC算法的要求相匹配，以确保通信的安全性；选择不合适的密钥长度可能会导致通信失败或降低安全性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmDecryptJobRef|
|描述|Reference to a CSM job to perform the data decryption operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmDecryptJobRef配置项用于指定用于TLS解密的加密服务管理器（CSM）作业的引用，确保TLS通信的安全性。|
|描述|注意：在配置TcpIpTlsCipherCsmDecryptJobRef时，必须确保引用的CSM作业支持所需的解密算法；此配置项对于实现基于TLS的安全通信至关重要，应仔细配置以避免安全漏洞。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmDecryptKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the data decryption operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmDecryptKeyRef 配置项用于指定用于TLS解密的密钥在CryIf模块中的引用，确保安全通信协议栈在接收数据时能够正确解密信息。|
|描述|注意：在配置TcpIpTlsCipherCsmDecryptKeyRef时，需要确保引用的密钥与所使用的TLS加密套件兼容；在配置密钥引用时，应注意密钥的存储和访问权限，以保证系统的安全性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmEncryptJobRef|
|描述|Reference to a CSM job to perform the data encryption operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmEncryptJobRef 是一个配置参数，用于指定在TCP/IP协议栈中，TLS加密过程中所使用的加密作业（Crypto Service Manager Job）的引用。|
|描述|注意：在配置TcpIpTlsCipherCsmEncryptJobRef时，需要确保引用的加密作业与所需的TLS加密算法相匹配；此外，应当检查Crypto Service Manager是否支持该加密作业。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmEncryptKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the data encryption operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmEncryptKeyRef配置项用于指定TLS加密过程中，与特定加密算法相关联的密钥引用，确保数据传输的安全性。|
|描述|注意：该配置项必须引用CryIf密钥配置，以确保加密算法的正确实施；在配置时需确保密钥长度和加密算法的兼容性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmMacGenerateJobRef|
|描述|Reference to a CSM job to perform the MAC generate operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmMacGenerateJobRef配置项用于指定用于TLS会话中MAC（消息认证码）生成的加密服务管理器（CSM）作业的引用，确保数据传输的完整性和认证。|
|描述|注意：该配置项需要确保引用的CSM作业支持所需的MAC算法；在配置TLS会话参数时，应考虑与其他安全参数（如密钥长度和加密算法）的兼容性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmMacGenerateKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the MAC generate operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCipherCsmMacGenerateKeyRef配置项用于指定用于TLS（传输层安全协议）加密过程中，MAC（消息认证码）生成所需密钥的引用。|
|描述|注意：该配置项必须引用CryIf模块中定义的密钥标识符；确保所引用的密钥满足TLS协议对MAC生成所需的安全要求；在配置时需考虑密钥的安全存储和管理策略。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmMacVerifyJobRef|
|描述|Reference to a CSM job to perform the MAC verify operation|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCipherCsmMacVerifyKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the MAC verify operation|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCiphersuiteDefinitionRef|
|描述|Reference to a a ciphersuite definition container|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCiphersuiteDefinitionRef是一个配置项，用于指定TCP/IP协议栈中TLS（传输层安全协议）所使用的加密套件的引用，确保数据传输的安全性。|
|描述|注意：加密套件的选择应考虑到安全性与性能之间的平衡；在多个网络接口间共享TLS配置时，需注意加密套件的兼容性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsCiphersuites/TcpIpTlsCiphersuiteDefinition|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsConnectionHandshakeRef|
|描述|References the container that contains the jobs and keys for handshake operation.|
|描述|Tags: atp.Status=draft|
|描述|None|
|说明|引用多个握手容器可以在各个工作线程之间共享它们，并在握手过程中选择下一个尚未使用的容器。|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsCiphersuites/TcpIpTlsHandshake|

##### 1.8.1.4. TcpIpTlsHandshake

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsHandshake|
|描述|This container provides information that is needed to process a handshake. It contains the appropriate references to jobs and keys of the CSM to perform the key exchange cryptographic for the ciphersuite and involved certificates.|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpTlsCsmPRFSupportType|
|描述|Specifies how the CSM job supports the PRF operation.|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmHashVerifyJobRef|
|描述|Reference to a CSM job to perform the hash operation for the whole handshake.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmHashVerifyJobRef 配置项用于指定在TLS（传输层安全协议）上下文中，用于验证接收到的数据的完整性的加密服务管理器（CSM）哈希验证作业的引用。|
|描述|注意：在配置TcpIpTlsCsmHashVerifyJobRef时，需要确保引用的CSM哈希验证作业与所使用的TLS配置兼容；此外，必须确保CSM作业的配置满足TLS协议的安全要求。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeCalcPubValJobRef|
|描述|Reference to a CSM job to perform the DH Key Exchange algorithm operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeCalcPubValJobRef配置项用于指定在TLS（传输层安全协议）密钥交换过程中，计算公共值所使用的加密作业的引用。|
|描述|注意：该配置项需要确保引用的加密作业与所需的密钥交换算法兼容；在配置时应注意加密作业的性能，以避免影响TLS握手过程的效率。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeCalcSecretJobRef|
|描述|Reference to a CSM job to perform the Key Exchange algorithm operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeCalcSecretJobRef 配置项用于引用在TLS握手过程中负责计算预主密钥的密钥交换算法的Crypto Service Manager（CSM）作业。|
|描述|注意：在配置时，需要确保引用的CSM作业与所需的密钥交换算法相匹配；此配置项对于实现TLS安全通信至关重要，因此必须正确配置。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeDecryptJobRef|
|描述|Reference to a CSM job to perform data decryption, e.g. with RSA key exchange operation.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeDecryptJobRef 是一个配置参数，用于指定在TLS（传输层安全协议）握手过程中，用于解密密钥交换的Crypto Service Manager（CSM）作业的引用。|
|描述|注意：在配置时，需要确保引用的CSM作业支持所需的解密算法和密钥长度；此配置项必须与系统中实际可用的CSM作业相匹配，否则可能导致TLS握手失败。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeDecryptKeyRef|
|描述|Reference to a CSM key to perform data decryption, e.g. with RSA, used for exchange operation.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeDecryptKeyRef 配置项用于指定在TLS（传输层安全协议）密钥交换过程中，用于解密接收到的密钥材料的密钥引用。|
|描述|注意：在配置TcpIpTlsCsmKeyExchangeDecryptKeyRef时，必须确保引用的密钥与所使用的加密算法兼容；此外，密钥的管理应遵循AUTOSAR的密钥管理模块规范；在配置过程中还应确保密钥的安全存储和处理，以防止潜在的安全漏洞。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeEncryptJobRef|
|描述|Reference to a CSM job to perform data encryption, e.g. with RSA key exchange operation.|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeEncryptKeyRef|
|描述|Reference to a CSM key to perform data encryption, e.g. with RSA, used for exchange operation.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeEncryptKeyRef 配置项用于指定在TLS（传输层安全协议）密钥交换过程中，用于加密的密钥参考，这通常指向一个加密密钥的Crypto Key管理配置。|
|描述|注意：在配置TcpIpTlsCsmKeyExchangeEncryptKeyRef时，需要确保引用的Crypto Key符合TLS所需的安全等级和算法要求；此外，该密钥应当由合适的Crypto Service Manager模块管理。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeKeyRef|
|描述|Reference to a CSM key used for Diffie Hellman (DH) key exchange operation.|
|描述|Tags: atp.Status=draft|
|描述|None|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeSignatureGenerateJobRef|
|描述|Reference to a CSM job to perform signature generation for DH operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeSignatureGenerateJobRef 配置项用于引用在TLS握手过程中用于生成数字签名的加密服务管理器（CSM）作业。|
|描述|注意：在配置TLS时，必须确保引用的CSM作业支持所需的签名算法；此外，CSM作业配置应与TLS配置的安全要求相匹配。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeSignatureGenerateKeyRef|
|描述|Reference to a CSM key to perform signature generation for DH operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeSignatureGenerateKeyRef 配置项用于指定在TLS握手过程中，用于生成数字签名的密钥引用，确保TLS握手的安全性。|
|描述|注意：该配置项必须引用一个有效的密钥管理容器，以确保数字签名的生成过程符合预期；在配置时需确保密钥的类型和长度符合TLS协议的要求。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeSignatureVerifyJobRef|
|描述|Reference to a CSM job to perform signature verification for DH operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeSignatureVerifyJobRef 配置项用于指定在TLS握手过程中，用于验证对方发送的密钥交换消息签名的加密服务管理器（CSM）作业引用。|
|描述|注意：在配置此项时，必须确保引用的CSM作业支持签名验证操作；应当与所使用的TLS证书和密钥交换算法兼容。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmKeyExchangeSignatureVerifyKeyRef|
|描述|Reference to a CSM key to perform signature verification for DH operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmKeyExchangeSignatureVerifyKeyRef 配置项用于指定在TLS握手过程中，用于验证对方发送的数字签名的公钥引用。|
|描述|注意：在配置TLS密钥交换时，必须确保引用的公钥与通信对方使用的私钥相匹配；此配置项通常与证书管理模块（Crypto Certificate Manager）相关联，需要正确配置证书引用。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmMasterSecretKeyRef|
|描述|This is the reference to the master key that is calculated during the session.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmMasterSecretKeyRef配置项用于指定TLS（传输层安全协议）连接中使用的主密钥的引用，这是确保数据传输安全的关键配置。|
|描述|注意：在配置TcpIpTlsCsmMasterSecretKeyRef时，必须确保引用的主密钥符合安全要求；此配置项对于实现TLS加密通信至关重要，应仔细管理密钥的生命周期。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmPrfMacJobRef|
|描述|Reference to a CSM job to perform the PRF hash operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmPrfMacJobRef 是一个配置参数，用于指定在使用传输层安全（TLS）协议时，与特定的 MAC（Message Authentication Code）计算相关的加密服务管理器（CSM）作业的引用。|
|描述|注意：在配置TLS时，必须确保引用的CSM作业与所需的MAC算法兼容；CSM作业配置应与系统的安全需求相匹配，确保数据的完整性和认证。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCsmPrfMacKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the PRF hash operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCsmPrfMacKeyRef配置项用于指定TLS（传输层安全协议）中使用的MAC（消息认证码）密钥的引用，以确保数据的完整性和认证。|
|描述|注意：在配置TcpIpTlsCsmPrfMacKeyRef时，必须确保引用的密钥与所使用的TLS版本和安全要求相匹配。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

##### 1.8.1.5. TcpIpTlsPskIdentity

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsPskIdentity|
|描述|This container provides information about static definition of pre-shared keys. It is used during the handshake to negotiate pre-shared keys between a client and a server.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPskIdentity配置项用于定义在使用TLS(传输层安全协议)进行通信时，预共享密钥(PSK)认证机制中使用的身份标识符。这个标识符用于在客户端和服务器之间建立安全连接时识别和选择正确的预共享密钥。|
|描述|注意：需要确保每个TcpIpTlsPskIdentity的值是唯一的，以避免在TLS握手过程中的身份识别冲突；预共享密钥机制应仅在双方无法使用更安全的证书基础认证机制时采用；配置时需考虑密钥管理和更新策略，以维护系统的安全性。|
|描述|该配置项未使用|
|说明|预共享密钥的回调函数是静态定义的替代方案。当使用预共享密钥但没有可用的静态定义时，可通过回调在运行时定义相关密钥。容器定义则用于静态配置。|
|多实例个数|0 - inf|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpTlsPskGetClientKeyIdentityFunc|
|描述|Defines the function name for the Up_TlsClientGetPskIdentity() callback.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPskGetClientKeyIdentityFunc是一个配置项，用于定义一个回调函数，该函数负责在TLS预共享密钥(PSK)握手过程中，提供客户端的身份信息和对应的PSK。|
|描述|注意：确保提供的身份信息和PSK与服务器端预期匹配，以保证TLS握手的成功；该回调函数的实现需要考虑安全性，避免泄露敏感信息。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpTlsPskGetKeyIdentyHintFunc|
|描述|Defines the function name for the Up_TlsServerGetPskIdentityHint() callback.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPskGetKeyIdentyHintFunc是一个配置项，用于指定一个回调函数，该函数用于在TLS握手过程中获取预共享密钥（PSK）的身份提示信息。|
|描述|注意：在使用基于PSK的TLS加密通信时，此配置项必须正确设置以确保TLS握手的正确性；身份提示信息用于在服务器端提示客户端使用特定的PSK，因此需要确保该信息的准确性和一致性。|
|多实例个数|0 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpTlsPskGetServerKeyIdentityFunc|
|描述|Defines the function name for the Up_TlsServerGetPskIdentity () callback.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPskGetServerKeyIdentityFunc是一个配置项，用于定义一个回调函数，该函数负责在TLS(传输层安全协议)预共享密钥(PSK)模式下，获取服务器端的密钥标识。|
|描述|注意：在使用TLS PSK模式时，确保正确实现此回调函数以提供有效的服务器密钥标识；该功能对于确保通信双方的身份验证和数据加密至关重要。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpTlsPresharedKeyIdentity|
|描述|This item provides the key identification. The TLS client selects the pre-shared key based on the identification hint provided by the server and returns the key identification name back to the server.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPresharedKeyIdentity 配置项用于定义在使用传输层安全（TLS）协议时，预共享密钥（PSK）身份的标识符，这是TLS握手过程中用于身份验证的关键信息。|
|描述|注意：在配置预共享密钥身份时，必须确保密钥的安全性和唯一性；此配置应与系统中其他安全配置项协同工作，以确保整体的通信安全。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|TcpIpTlsPresharedKeyIdentityHint|
|描述|Provides the identity hint for a pre-shared key. This information is transmitted by the TLS Server to provide its identification to the TLS client.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPresharedKeyIdentityHint 配置项用于指定在使用TLS协议进行通信时，预共享密钥（PSK）身份提示的值，这有助于在客户端和服务器之间建立一个安全的连接。|
|描述|注意：需要确保使用的预共享密钥身份提示符合TLS协议的规范；此配置项通常与安全通信相关，因此需要确保密钥管理的安全性和合规性；在实际部署时，应避免使用硬编码的密钥，而是采用安全的密钥分发机制。|
|描述|该配置项未使用|
|说明|TLS 客户端使用相同的信息来选择预共享密钥。|
|多实例个数|0 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsPresharedKeyCsmKeyRef|
|描述|Reference to a CSM key associated to the CSM job that performs the PRF hash operation|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPresharedKeyCsmKeyRef 配置项用于指定在使用传输层安全（TLS）协议时，预共享密钥（PSK）的加密服务管理器（CSM）密钥引用，以便于在建立TLS连接时进行身份验证和加密通信。|
|描述|注意：需要确保引用的CSM密钥配置正确，以匹配预期的安全要求；预共享密钥应当保密，且其长度和复杂度应满足安全标准；在配置时应注意与其他安全配置项的兼容性和整体安全架构的一致性。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

#### 1.8.2. TcpIpTlsConnection

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsConnection|
|描述|This container defines the properties of a TLS connection|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnection配置项用于定义TCP/IP协议栈中的TLS连接参数，包括安全连接的属性和行为，以确保数据传输的安全性。|
|描述|注意：密钥交换、认证、加密和消息认证码算法应根据最新的安全要求进行选择；配置应与系统中其他安全相关组件的配置保持一致，以确保整体安全性。|
|描述|该配置项未使用|
|多实例个数|1 - inf|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTlsUseClientAuthenticationRequest|
|描述|Defines if client authentication shall be applied for this TLS connection.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsUseClientAuthenticationRequest 配置项用于指定是否在TLS握手过程中请求客户端认证，这是网络管理的一部分，用于确保通信双方的身份验证和数据安全。|
|描述|注意：需要确保此配置与系统的安全需求相匹配；如果启用客户端认证，客户端必须能够提供有效的证书；此配置可能会影响通信的性能，因为客户端认证会增加握手过程的复杂性和时间。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpTlsUseSecurityExtensionRecordSizeLimit|
|描述|Defines if the security extension for max_fragment_length shall be supported as defined in IETF RFC 8449, chapter 4.1.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsUseSecurityExtensionRecordSizeLimit 配置项用于指定是否在TLS（传输层安全协议）握手过程中使用Security Extension Record Size Limit，这可以限制TLS记录层的最大记录大小，以提高安全性。|
|描述|注意：必须确保TLS配置与标准保持一致，以便正确实现记录大小限制；此配置项的使用可能会影响通信性能，因为它可能减少了每个TLS记录的有效载荷大小；在设计系统时，应考虑与网络性能和安全性之间的平衡。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|TcpIpTlsConnectionType|
|描述|Specifies if the TLS connection is a server or a client.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionType 配置项用于定义TCP/IP协议栈中的TLS连接类型，指定是客户端还是服务器端的TLS连接，以确保安全的数据传输。|
|描述|注意：在配置TcpIpTlsConnectionType时，需要确保选择的类型与实际应用场景相匹配；TLS配置应与系统的安全需求和策略相一致，以保障通信的安全性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|TcpIpTlsConnectionGetTimeFunc|
|描述|Defines the function name for the Up_TlsGetCurrentTimeStamp() callback.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionGetTimeFunc 是一个配置项，用于指定一个回调函数，该函数由TCP/IP协议栈调用以获取当前的时间信息，通常用于TLS连接中的时间戳和超时处理。|
|描述|注意：在配置TcpIpTlsConnectionGetTimeFunc时，需要确保提供的函数能够返回符合TLS协议要求的时间格式；此外，该函数的实现必须考虑到系统的实时性和性能影响；如果系统不使用TLS或者不需要精确的时间戳，可能不需要配置此项。|
|描述|该配置项未使用|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsConnectionId|
|描述|Identifier of the connection. The set of configured identifiers shall be consecutive and gapless.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionId 是用于标识TCP/IP协议栈中的TLS连接的唯一标识符，用于区分不同的TLS安全连接。|
|描述|注意：在配置TcpIpTlsConnectionId时，必须确保每个TLS连接拥有一个唯一的标识符；在整个系统中，这个标识符应当是全局唯一的，以避免在TLS连接建立过程中的任何混淆。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsMaxFragmentLength|
|描述|Specifies the max length in bytes of a TLS fragment that is sent as a block.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsMaxFragmentLength配置项用于定义TCP/IP协议栈中TLS加密通信时，最大的片段长度，这有助于优化网络传输性能和减少内存使用。|
|描述|注意：该配置项的值必须是符合TLS标准中定义的最大片段长度枚举值之一；不正确的配置可能导致TLS通信失败或性能下降；在资源受限的系统中，合理设置此值对于内存使用优化尤为重要。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|1 - 16384|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpTlsPortAssignment|
|描述|Specifies the port address that is used for TLS communication.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsPortAssignment 配置项用于指定哪些TCP/IP端口将使用传输层安全性（TLS）进行通信，确保数据传输的安全性和完整性。|
|描述|注意：在配置TcpIpTlsPortAssignment时，需要确保指定的端口支持TLS协议；应当与网络管理和安全策略保持一致。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|取值范围|1 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsCertificateIdentityRef|
|描述|References the container that contains the certificate and identity information.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsCertificateIdentityRef 是一个配置项，用于引用存储在系统中的TLS证书标识，这个标识用于在TCP/IP栈中建立TLS安全连接时的身份验证。|
|描述|注意：在配置TcpIpTlsCertificateIdentityRef时，需要确保引用的证书标识与实际存储的TLS证书相匹配；证书应当由可信的证书颁发机构签发，以确保系统的安全性。|
|描述|该配置项未使用|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsCiphersuites/TcpIpTlsCertificateIdentity|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsConnectionCiphersuiteWorkerRef|
|描述|References the container that contains the jobs and keys to process the application data.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionCiphersuiteWorkerRef 配置项用于指定TCP/IP栈中TLS连接所使用的加密套件，它引用了一个或多个加密套件的工作定义，以确保数据传输的安全性。|
|描述|注意：在配置时需确保引用的加密套件与系统的安全需求相匹配；正确的引用是建立安全通信的关键，错误的配置可能导致通信不安全或连接失败。|
|描述|该配置项未使用|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsCiphersuites/TcpIpTlsCiphersuiteWorker|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsConnectionGroupRef|
|描述|Assigns the TLS connection to a connection group.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionGroupRef 配置项用于指定TCP/IP协议栈中的TLS连接组引用，它关联了特定的TLS配置集，以供建立安全的通信通道。|
|描述|注意：在配置TcpIpTlsConnectionGroupRef时，必须确保引用的TLS连接组在系统中已定义并且有效；此配置项对于实现基于TLS的安全通信至关重要。|
|描述|该配置项未使用|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsConnectionGroup|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsConnectionPskIdentityRef|
|描述|References the container that contains information about pre-shared keys.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionPskIdentityRef是用于指定TLS连接中预共享密钥（PSK）身份的引用，它关联到一个或多个预定义的PSK身份，以便在TLS握手过程中使用。|
|描述|注意：在配置TcpIpTlsConnectionPskIdentityRef时，必须确保引用的PSK身份已在系统中定义；此配置项对于实现基于PSK的TLS安全通信至关重要。|
|描述|该配置项未使用|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpTlsConfig/TcpIpTlsCiphersuites/TcpIpTlsPskIdentity|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|TcpIpTlsIpAddressAssignment|
|描述|Contains additional information about the endpoint IP address information. If this reference is present, the IP address of the connecting socket shall also be checked if a TLS connection shall be assigned automatically to a socket.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsIpAddressAssignment配置项用于定义TCP/IP协议栈中，通过TLS安全连接所使用的IP地址分配方式，确保网络通信的安全性和正确性。|
|描述|注意：需要确保选择的IP地址分配方式与网络架构和应用需求相匹配；此配置项对于实现基于TLS的安全通信至关重要；在配置时需考虑网络的动态性，选择静态或动态IP地址分配方式。|
|描述|该配置项未使用|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/TcpIp/TcpIpConfig/TcpIpLocalAddr/TcpIpStaticIpAddressConfig|

#### 1.8.3. TcpIpTlsConnectionGroup

| 容器属性 | 值（容器） |
|-|-|
|名称|TcpIpTlsConnectionGroup|
|描述|This optional container is used to collect all TlsConnections that belong to a TlsConnectionGroup. The intention of a TLS connection group is to share resources among TLS connections collected in a group, because only one connection of a group can be used at a time.|
|描述|Tags: atp.Status=draft|
|描述|概述：TcpIpTlsConnectionGroup配置项定义了一组TCP/IP连接的TLS（传输层安全协议）属性，用于确保数据传输的安全性和完整性。|
|描述|注意：需要为每个需要加密的TCP/IP连接指定一个唯一的TcpIpTlsConnectionGroup；配置时应注意证书和密钥管理策略，以保障通信安全。|
|描述|该配置项未使用|
|多实例个数|0 - inf|

### 1.9. TcpIpUdpConfig

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
|名称|TcpIpBufferMemory|
|描述|Memory size in bytes reserved for TCP/IP buffers.|
|描述|概述：TcpIpBufferMemory 配置项用于定义TCP/IP协议栈中用于存储网络数据的缓冲区大小，这直接影响网络通信的效率和性能。|
|描述|注意：在配置TcpIpBufferMemory时，需要确保缓冲区大小与系统的内存资源和网络通信需求相匹配；过大的缓冲区可能会浪费系统资源，而过小的缓冲区可能导致数据包丢失或通信延迟；此外，该配置项应与其他网络配置参数协同优化，以达到最佳网络性能。|
|描述|该配置项未使用|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

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
|名称|TcpIpAutoIpEnabled|
|描述|Enables (TRUE) or disables (FALSE) the Auto-IP (automatic private IP addressing) sub-module.|
|描述|概述：TcpIpAutoIpEnabled 配置项用于启用或禁用TCP/IP协议栈中的自动IP地址配置功能，这是一种无需手动配置即可为网络接口分配临时IP地址的机制。|
|描述|注意：在没有DHCP服务器的网络环境中，自动IP可以提供一种替代的IP地址配置方法；确保网络中的其他节点不使用相同的自动IP地址范围，以避免地址冲突；在启用自动IP时，还需考虑与其他网络配置和服务的兼容性。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpDhcpClientEnabled|
|描述|Enables (TRUE) or disables (FALSE) the DHCP (Dynamic Host Configuration Protocol) Client.|
|描述|概述：TcpIpDhcpClientEnabled 配置项用于启用或禁用TCP/IP协议栈中的DHCP客户端功能，允许网络接口自动获取IP地址和其他网络配置。|
|描述|注意：在使用静态IP地址配置的系统中，应禁用此功能以避免地址冲突；确保在需要动态IP分配的网络环境中启用此功能；在配置此项时，还需考虑网络启动时间和可能的DHCP服务器响应延迟。|
|描述|该配置项未使用|
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

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|TcpIpPathMtuDiscoveryEnabled|
|描述|Enables (TRUE) or disables (FALSE) the discovery of the maximum transmission unit on a path according to IETF RfC 1191.|
|描述|概述：TcpIpPathMtuDiscoveryEnabled配置项用于启用或禁用TCP/IP协议栈中的路径最大传输单元（Path MTU）发现机制，该机制允许网络设备发现并使用最有效的数据包大小，以避免在网络路径中的分片。|
|描述|注意：需要确保网络配置与实际网络环境相匹配，以免导致数据传输效率低下或通信失败；过大的MTU值可能导致数据包在网络中被分片，影响性能；过小的MTU值可能导致利用率低下。|
|描述|该配置项未使用|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|TcpIpLocalAddrIpv4EntriesMax|
|描述|Maximum number of LocalAddr table entries for IPv4.|
|描述|概述：TcpIpLocalAddrIpv4EntriesMax定义了系统中可配置的IPv4本地地址的最大数量，用于限制可分配给TCP/IP协议栈的IPv4地址数量。|
|描述|注意：在设计网络配置时，需要确保此值足够容纳预期的网络接口数量；超出此限制的地址配置可能会被忽略；该参数的设置应考虑系统的扩展性和未来的网络需求。|
|多实例个数|1 - 1|
|取值范围|0 - 255|



