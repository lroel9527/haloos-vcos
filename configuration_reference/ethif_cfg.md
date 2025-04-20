#  EthIf 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIf|
|描述|Configuration of the EthIf (Ethernet Interface) module.|
|描述|概述：EthIf是以太网接口模块，它提供了AUTOSAR软件架构中的通用以太网通信接口，用于抽象底层的以太网驱动和控制器。|
|描述|注意：在配置EthIf模块时，需要确保它与底层的Eth驱动和硬件控制器的配置相匹配；此外，还要考虑与上层通信管理和网络管理模块的交互；AUTOSAR CP 4.4标准中可能引入了新的配置参数或者对现有参数的解释有所更新，需要参照最新的标准文档进行配置。|
|多实例个数|0 - 1|

## 1. EthIfConfigSet

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfConfigSet|
|描述|Collecting container for all parameters with post-build configuration classes.|
|描述|概述：EthIfConfigSet 是一个配置容器，它包含了以太网接口模块（EthIf）的配置集合，用于定义网络接口层的参数，如控制器引用、缓冲区大小和过滤器设置等。|
|描述|注意：在配置EthIfConfigSet时，需要确保其参数与底层以太网控制器和物理传输媒介的特性相匹配；此外，配置集合中的每个参数都应符合AUTOSAR CP 4.4标准中定义的数据类型和取值范围；在多配置集环境中，还需注意配置集之间的切换逻辑和一致性。|
|多实例个数|1 - 1|

### 1.1. EthIfController

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfController|
|描述|This container contains the configuration of EthIfController.|
|描述|概述：EthIfController 配置项定义了以太网接口控制器的属性，包括其物理控制器引用和相关的配置参数。|
|描述|注意：确保每个EthIfController配置项正确映射到相应的硬件控制器；在配置时需注意与网络管理功能的兼容性；配置参数应符合AUTOSAR CP 4.4标准，以保证网络通信的正确性和效率。|
|多实例个数|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfCtrlIdx|
|描述|This parameter provides a zero-based consecutive index of the Ethernet Communication Controllers. Upper layer BSW modules and the EthIf itself use this index to identify a Ethernet CC.|
|描述|概述：EthIfCtrlIdx是用于标识以太网接口控制器的唯一索引，它关联特定的以太网控制器与上层以太网接口配置。|
|描述|注意：在配置时需确保每个EthIfCtrlIdx与唯一的以太网控制器相对应，避免索引重复；该索引值通常由系统自动生成，手动修改可能导致系统配置不一致；在多控制器系统中，正确的索引映射对于网络通信的正确性至关重要。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfCtrlMtu|
|描述|Specifies the maximum transmission unit (MTU) of the EthIfCtrl in [bytes].|
|描述|概述：EthIfCtrlMtu 是一个配置项，用于定义以太网接口控制器（Ethernet Interface Controller）的最大传输单元（Maximum Transmission Unit, MTU），即可以通过网络接口发送的最大数据包大小。|
|描述|注意：MTU值必须与网络的实际能力相匹配，避免数据包过大导致分片；在配置MTU时，应考虑网络协议栈的要求和硬件能力；AUTOSAR CP 4.4标准中，确保MTU值的配置与通信控制器和网络驱动的能力相一致。|
|说明|Note: In case a VLAN tag is used for the EthIfCtrl, the frame length of the Ethernet frame will increase by 4 bytes.|
|多实例个数|1 - 1|
|取值范围|64 - 9000|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfMaxTxBufsTotal|
|描述|Limits the total number of transmit buffers.|
|描述|概述：EthIfMaxTxBufsTotal配置项定义了以太网接口(EthIf)模块可用于发送操作的最大传输缓冲区总数，这个参数直接影响网络通信的效率和性能。|
|描述|注意：该配置项的值需要根据网络通信量和系统资源合理设置，以避免缓冲区溢出或资源浪费；在AUTOSAR CP 4.4中，确保该值与网络堆栈和硬件资源相匹配；过低的配置可能导致发送队列满，影响数据发送效率。|
|多实例个数|1 - 1|
|取值范围|1 - 4294967295|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfVlanId|
|描述|A virtual-LAN is identified by this attribute according to IEEE 802.1Q.|
|描述|概述：EthIfVlanId 配置项用于定义以太网接口（Ethernet Interface）的虚拟局域网（VLAN）标识符，这是一个在以太网帧中用于区分不同虚拟网络的标签。|
|描述|注意：VLAN ID的取值范围通常是0到4095，其中0和4095是保留值；在配置VLAN ID时，需要确保它在网络中是唯一的，以避免VLAN间的冲突；在AUTOSAR CP 4.4标准中，应当确保EthIfVlanId与网络配置和硬件支持相匹配。|
|多实例个数|1 - 1|
|取值范围|0 - 4095|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfLinkAggrThreshold|
|描述|Threshold when a link is issued on EthIf controller level.|
|描述|概述：EthIfLinkAggrThreshold 配置项用于定义以太网接口链路聚合中的阈值，该阈值决定何时触发链路聚合或解聚操作。|
|描述|注意：在配置此参数时，需确保阈值设置符合网络的带宽和流量需求；不正确的阈值可能导致网络性能下降或不稳定；此配置项在AUTOSAR CP 4.4中未明确定义，需要根据具体实现或供应商的指导进行配置。|
|多实例个数|1 - 1|
|取值范围|1 - 255|

| 配置项属性 | 值（选择引用配置项） |
|-|-|
|名称|EthIfSwitchRefOrPortGroupRef|
|描述|The choice reference allows to configure either the EthIfController references an EthIfSwitch or an EthIfSwitchPortGroup.|
|说明|Reference to a EthIfSwitchPortGroup. In case port groups are controlled by PNC EthIfSwitchPortGroupRefSemantics shall have the value ETHIF_SWITCH_PORT_GROUP_LINK_INFO. In case port groups are controlled by the EhtIfController EthIfSwitchPortGroupRefSemantics shall have the value ETHIF_SWITCH_PORT_GROUP_CONTROL.|
|多实例个数|0 - 1|
|目标引用|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfSwitch/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfSwitchPortGroup|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfEthTrcvRef|
|描述|Reference to an Ethernet transceiver, which is handled by the Ethernet Interface.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfTransceiver|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfPhysControllerRef|
|描述|Reference to a physical Ethernet controller, which is handled by the Ethernet Interface.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfPhysController|

### 1.2. EthIfFrameOwnerConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfFrameOwnerConfig|
|描述|Configuration of Ethernet frame owner|
|描述|概述：EthIfFrameOwnerConfig配置项用于定义以太网帧的所有者信息，包括哪些上层模块（如DoIP, SOME/IP等）可以接收或发送特定的以太网帧。|
|描述|注意：确保每个以太网帧的所有者配置正确，避免帧处理的冲突；在配置时需考虑网络带宽和处理能力，以免影响通信性能；AUTOSAR CP 4.4中对以太网帧的处理和所有权有明确规范，需遵守相关规定以保证兼容性。|
|多实例个数|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfFrameType|
|描述|Selects the Ethernet frame type.|
|描述|概述：EthIfFrameType配置项用于定义以太网接口支持的帧类型，确保网络层与数据链路层之间正确的数据交换。|
|描述|注意：在配置EthIfFrameType时，必须确保所选帧类型与网络层协议兼容；不同的以太网控制器可能支持不同的帧类型，需要根据硬件规范进行选择；AUTOSAR CP 4.4标准中对帧类型的支持可能有特定的限制或要求，需要仔细检查标准文档。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfOwner|
|描述|Selects the owner of an Ethernet frame type. The owner is a zero based index into the callback function configuration 'EthIfRxIndicationConfig'. I.e. an Ethernet frame of type IPv4 (0x800) at index 0 will call the first callback function configured in 'EthIfRxIndicationConfig'.|
|描述|概述：EthIfOwner配置项用于指定以太网接口控制器（Ethernet Interface Controller）的所有者，这通常是指定了哪个上层模块（如TCP/IP协议栈）拥有和控制该以太网接口。|
|描述|注意：在配置EthIfOwner时，需要确保它与实际的系统架构和网络管理策略一致；此外，每个以太网接口应该只有一个所有者，避免所有权冲突；根据AUTOSAR CP 4.4标准，确保配置项的属性与标准定义的参数匹配，以保证系统的兼容性和正确性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

### 1.3. EthIfPhysController

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfPhysController|
|描述|This container contains the configuration of EthIfPhysController.|
|描述|概述：EthIfPhysController配置项定义了以太网接口物理控制器的属性，这些属性包括控制器的索引、关联的硬件资源以及其他特定的控制器参数，用于管理网络层与物理层之间的交互。|
|描述|注意：在配置EthIfPhysController时，需要确保其索引与实际硬件资源相匹配；此外，应当注意与网络管理和驱动层的兼容性；在多控制器系统中，还需注意控制器之间的优先级和资源共享策略。|
|说明|The usage of EthIfEthCtrlRef and EthIfWEthCtrlRef is exclusive OR.|
|多实例个数|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfPhysControllerIdx|
|描述|This parameter provides a zero-based consecutive index of the physical Ethernet controllers. Upper layer BSW modules and the Ethernet Interface itself use this index to identify a physical Ethernet controller.|
|描述|概述：EthIfPhysControllerIdx 用于指定以太网接口物理控制器的索引，这是连接网络硬件与软件配置的关键参数。|
|描述|注意：确保索引与实际硬件配置相匹配，避免配置错误导致网络通信失败；在多控制器系统中，每个控制器的索引必须是唯一的；在配置时参考硬件设计文档以确保正确性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfEthCtrlRef|
|描述|Reference to a physical Ethernet controller, which is handled by a specific Ethernet controller driver.|
|描述|概述：EthIfEthCtrlRef 是一个配置参数，用于引用以太网接口模块（EthIf）中的特定以太网控制器（EthCtrl）实例，确保数据传输可以通过正确的网络控制器进行。|
|描述|注意：在配置时必须确保引用的EthCtrl实例已经定义在系统中；EthIfEthCtrlRef的值应与EthCtrl的标识符相匹配；在多控制器系统中，正确的控制器引用对于网络管理和通信性能至关重要。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Eth/EthConfigSet/EthCtrlConfig|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfWEthCtrlRef|
|描述|Reference to a physical Wireless Ethernet controller, which is handled by a specific Wireless Ethernet controller driver.|
|描述|概述：EthIfWEthCtrlRef 是一个配置项，用于引用以太网接口模块（EthIf）中的特定以太网控制器（EthCtrl）的配置。|
|描述|注意：在配置EthIfWEthCtrlRef时，需要确保引用的EthCtrl配置已经存在并且正确配置；此配置项是连接以太网接口和底层以太网驱动的关键，错误的配置可能导致通信失败；在AUTOSAR CP 4.4标准中，确保该引用符合模块间通信和配置的规范要求。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/WEth/WEthConfigSet/WEthCtrlConfig|

#### 1.3.1. EthIfPhysCtrlRxMainFunctionPriorityProcessing

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfPhysCtrlRxMainFunctionPriorityProcessing|
|描述|Configuration of ingress FIFO based main function processing.|
|描述|概述：EthIfPhysCtrlRxMainFunctionPriorityProcessing配置项用于定义以太网接口物理控制器接收主函数的优先级处理，确保数据接收处理的优先级顺序符合系统要求。|
|描述|注意：在配置时需确保优先级设置不会导致数据处理的延迟或丢失，特别是在高数据吞吐量的网络环境中；优先级配置应遵循AUTOSAR CP 4.4标准中对于任务调度和优先级管理的相关规定；在多物理控制器的系统中，需要综合考虑各控制器间的优先级设置，以保证整体系统的性能和稳定性。|
|多实例个数|0 - 65535|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfPhysCtrlRxMainFunctionPeriod|
|描述|Specifies the period of main function in seconds.|
|描述|概述：EthIfPhysCtrlRxMainFunctionPeriod 定义了以太网接口物理控制器接收主函数的调用周期，用于控制数据接收处理的时间间隔。|
|描述|注意：该周期值应根据网络通信的实时性和带宽要求进行配置；配置值过大可能导致数据延迟，过小可能增加CPU负载；确保配置的周期与系统的任务调度策略相匹配。|
|多实例个数|1 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfPhysCtrlRxIndicationIterations|
|描述|Max number of Ethernet frames polled per main function invocation.|
|描述|概述：EthIfPhysCtrlRxIndicationIterations 配置项定义了物理控制器接收到帧后，上层以太网接口模块（EthIf）调用RxIndication回调函数的迭代次数，用于处理接收到的帧。|
|描述|注意：在配置此项时，需要确保迭代次数与实际的帧处理能力相匹配，避免过多迭代导致处理延迟；迭代次数不宜设置过低，以免无法及时处理所有接收到的帧；此配置项的设置应考虑到系统的实时性要求和网络负载情况。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfPhysCtrlRxIngressFifoRef|
|描述|Reference to the reception FIFO.|
|描述|概述：EthIfPhysCtrlRxIngressFifoRef配置项用于指定以太网接口物理控制器接收入口的FIFO引用，确保数据包能够被正确地接收并按顺序处理。|
|描述|注意：在配置时需确保引用的FIFO与物理控制器兼容且存在；正确配置此项对于网络性能和数据包处理的实时性至关重要；AUTOSAR CP 4.4标准中未明确列出此配置项，需根据具体实现和硬件支持情况进行适配。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Eth/EthConfigSet/EthCtrlConfig/EthCtrlConfigIngress/EthCtrlConfigIngressFifo|

### 1.4. EthIfRxIndicationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfRxIndicationConfig|
|描述|Configuration of receive callback functions.|
|描述|概述：EthIfRxIndicationConfig 是一个配置项，用于定义以太网接口模块（EthIf）接收到帧时的行为，包括如何处理和通知上层协议栈。|
|描述|注意：在配置时需确保与网络层协议的需求相匹配；考虑到性能影响，应优化处理流程以减少延迟；在多帧接收场景下，应确保正确的帧排序和缓冲管理。|
|多实例个数|1 - 255|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfRxIndicationFunction|
|描述|Specifies receive indication callback function.|
|描述|概述：EthIfRxIndicationFunction是一个配置项，用于指定当以太网接口（Ethernet Interface）接收到一个新的帧时，应当调用的回调函数，以便上层协议或应用能够处理接收到的数据。|
|描述|注意：在配置EthIfRxIndicationFunction时，需要确保回调函数与接收任务的优先级和执行时间相匹配，以避免数据处理延迟或丢失；此外，回调函数应当能够高效地处理数据，避免阻塞以太网接口的接收过程；在AUTOSAR CP 4.4标准中，应当遵循定义的接口规范来实现回调函数，确保其兼容性和正确性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|FrameOwnerRef|
|描述|Reference to the frame owner to assign the RxIndication function.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfFrameOwnerConfig|

### 1.5. EthIfSwitch

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfSwitch|
|描述|This container contains the configuration of EthIfSwitches.|
|描述|概述：EthIfSwitch 配置项用于定义以太网交换机。|
|描述|注意：在AUTOSAR CP 4.4标准中，网络管理功能需要确保网络接口的状态能够根据系统需求动态调整；配置时需考虑系统的安全和隔离需求；此配置项应与其他网络管理配置项协同工作，以保证网络的稳定性和效率。|
|多实例个数|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfSwitchIdx|
|描述|This parameter provides a zero-based consecutive index of the Ethernet Interface Switches. Upper layer BSW modules and the EthIf itself use this index to identify a Ethernet Switch.|
|描述|概述：EthIfSwitchIdx 用于标识以太网接口所连接的交换机的索引，这有助于在配置网络时识别和管理不同的网络交换机。|
|描述|注意：在配置EthIfSwitchIdx时，确保索引与实际物理或虚拟网络拓扑中的交换机对应正确；避免索引重复，以免造成网络配置错误；在AUTOSAR CP 4.4中，每个以太网接口必须有一个唯一的交换机索引。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfSwitchRef|
|描述|Reference to a Ethernet Switch, which is handled by a specific Ethernet Switch driver.|
|描述|概述：EthIfSwitchRef 是一个配置项，用于在以太网接口配置中引用一个以太网交换机，它建立了以太网接口和特定以太网交换机之间的关联。|
|描述|注意：在配置EthIfSwitchRef时，需要确保引用的以太网交换机已经在系统中定义且配置正确；此配置项对于实现虚拟局域网（VLAN）和交换机管理功能至关重要；在配置过程中，应注意与其他网络配置项的一致性和兼容性，以确保网络通信的正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthSwt/EthSwtConfig|

### 1.6. EthIfSwitchMgmtInfoIndicationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfSwitchMgmtInfoIndicationConfig|
|描述|Configuration of Switch Management callback function.|
|描述|概述：EthIfSwitchMgmtInfoIndicationConfig配置项用于定义以太网交换机管理信息指示的配置参数，这些参数控制着交换机管理信息如何被指示给上层软件。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与网络管理和诊断需求相匹配；配置参数必须与实际硬件和网络拓扑一致；如果项目不使用以太网交换机或不需要管理信息指示，该配置项可能不需要。|
|多实例个数|0 - 65535|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfSwitchMgmtInfoIndicationFunction|
|描述|Enables/Disables the ingress Switch management info indication redirected call to upper layers who registered for the call.|
|描述|概述：EthIfSwitchMgmtInfoIndicationFunction 配置项用于指定一个回调函数，该函数在以太网交换机管理信息（如链路状态变化）发生时被调用，以通知上层软件组件。|
|描述|注意：在配置此回调函数时，需要确保它与实际的以太网驱动和硬件支持的功能相匹配；此外，该回调函数的实现应避免执行长时间的操作或调用可能导致阻塞的API，以免影响网络通信的实时性；最后，确保该函数在系统中被正确注册，以便在交换机管理信息发生变化时能够被正确调用。|
|多实例个数|1 - 1|

### 1.7. EthIfSwitchPortGroup

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfSwitchPortGroup|
|描述|This container contains the configuration of EthIfSwitchPortGroups.|
|描述|概述：EthIfSwitchPortGroup 配置项用于定义以太网接口的交换端口组，这有助于管理和优化网络流量。|
|描述|注意：确保每个端口组配置正确的端口成员和属性，以避免网络冲突；在配置端口组时，应考虑网络的拓扑结构和流量需求；AUTOSAR CP 4.4中对于交换端口组的管理和配置提供了详细的指导，应遵循标准以确保兼容性和性能。|
|说明|If EthIfSwitchPortGroups are controlled by PNC one EthIfSwitchPortGroup per PNC shall exist. The host port shall be part of all EthIfSwitchPortGroups. The up link port of a master switch and the up link port of the slave switch shall be part of all EthIfSwitchPortGroups that contain EthSwtPorts belonging to the slave switch.|
|多实例个数|0 - 65535|

#### 1.7.1. EthIfSwtPort

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfSwtPort|
|描述|Configuration of one Ethernet Switch Port.|
|描述|概述：EthIfSwtPort 配置项定义了以太网接口与交换端口之间的映射关系，用于管理网络通信中的数据路由和转发。|
|描述|注意：确保每个EthIfSwtPort配置正确映射到相应的物理端口，避免数据传输错误；在配置时需考虑网络的拓扑结构以及交换机的性能和容量；此配置项应与网络设计和实际物理连接紧密相关，以保证网络的稳定性和效率。|
|多实例个数|1 - inf|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|EthIfSwtPortRole|
|描述|Set a special role of the Ethernet switch port. It is either a host port or a up link port. If not configured it is a standard port.|
|描述|概述：EthIfSwtPortRole配置项定义了以太网接口交换机端口的角色，用于区分端口功能，如管理端口或普通网络端口，以支持网络的配置和管理。|
|描述|注意：在配置EthIfSwtPortRole时，需要确保端口角色与网络设计和交换机配置相匹配；不正确的端口角色配置可能导致网络通信故障；AUTOSAR CP 4.4标准中对于以太网交换机的支持和配置有详细规定，需要遵守相关规范。|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfSwtPortIdx|
|描述|Specifies the instance ID of the configured Ethernet Switch Port.|
|描述|概述：EthIfSwtPortIdx是用于标识以太网接口交换机端口的索引，它指定了网络通信中以太网帧从哪个交换机端口发送或接收。|
|描述|注意：在配置时需确保EthIfSwtPortIdx与实际物理或虚拟交换机端口相匹配；不同的EthIfSwtPortIdx应对应不同的交换机端口，避免配置冲突；AUTOSAR CP 4.4标准中对于以太网交换机的管理和配置提供了详细规范，需要遵循相关规定以保证网络通信的正确性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfSwtIdx|
|描述|Specifies the instance ID of the configured Ethernet Switch.|
|描述|概述：EthIfSwtIdx 是一个配置参数，用于指定交换机的索引，确保网络通信的正确路由。|
|描述|注意：在配置时需确保EthIfSwtIdx 的值与实际的硬件架构和网络设计相匹配；每个以太网接口应该有一个唯一的索引与之对应；在配置过程中应参照AUTOSAR的网络管理和通信矩阵来正确设置此参数。|
|多实例个数|1 - 1|
|取值范围|0 - 255|
|默认值|0|

| 配置项属性 | 值（枚举参数配置项） |
|-|-|
|名称|EthIfSwitchPortGroupRefSemantics|
|描述|Defines how the EthIfSwitchRefOrPortGroupRef refering to a EthIfSwitchPortGroup shall be interpreted.|
|描述|概述：EthIfSwitchPortGroupRefSemantics 配置项定义了以太网接口模块中交换端口组引用的语义，这通常涉及到如何处理交换端口组的引用，以及它们如何关联到底层的硬件端口。|
|描述|注意：在配置时需要确保引用的端口组与实际的硬件端口配置相匹配；此配置项对于网络管理和以太网交换机的配置至关重要，因此需要仔细检查以避免通信问题；AUTOSAR CP 4.4标准中可能有具体的约束和规则来指导如何设置这一配置项，需要遵循标准以确保兼容性和正确性。|
|多实例个数|0 - 1|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfSwitchPortGroupIdx|
|描述|This parameter provides a zero-based consecutive index of the Ethernet Switch Port Groups. Upper layer BSW modules and the EthIf itself use this index to identify an Ethernet Switch Port Group.|
|描述|概述：EthIfSwitchPortGroupIdx 用于标识以太网接口在交换机端口组中的索引，这有助于管理和配置网络中的端口组。|
|描述|注意：确保索引与实际硬件和网络拓扑结构相匹配；在配置时避免索引重复，以防止网络配置错误；此配置项应与实际的网络管理策略和安全策略相协调。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfPortRef|
|描述|Reference to an Ethernet Switch Port.|
|描述|概述：EthIfPortRef是一个配置项，用于指定以太网接口（Ethernet Interface）模块中交换机某个端口的引用，确保数据的传输和接收可以通过正确的物理或虚拟网络接口进行。|
|描述|注意：在配置EthIfPortRef时，必须确保引用的端口已在系统中定义且与所需的通信需求相匹配；此配置项对于网络管理和通信性能优化至关重要；在多网络接口的系统设计中，正确的端口引用对于避免数据传输错误和网络冲突尤为重要。|
|多实例个数|0 - 65535|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthSwt/EthSwtConfig/EthSwtPort|

### 1.8. EthIfSwitchTimeStampIndicationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfSwitchTimeStampIndicationConfig|
|描述|Configuration of Switch timestamp indications.|
|描述|概述：EthIfSwitchTimeStampIndicationConfig 用于配置以太网接口的时间戳指示，这有助于网络时间同步和性能分析。|
|描述|注意：确保网络硬件支持时间戳功能；配置应与网络的时间同步策略一致；在AUTOSAR CP 4.4中，此配置项的具体属性应详细检查以符合标准规范。|
|多实例个数|0 - 65535|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfSwitchEgressTimeStampIndicationFunction|
|描述|Enables/Disables to upper layers an egress timestamp indication function.|
|描述|概述：EthIfSwitchEgressTimeStampIndicationFunction 配置项用于指定当以太网接口的交换机端口发送帧时，用于指示出口时间戳的回调函数。|
|描述|注意：在配置以太网交换机支持时，需要确保该回调函数与硬件和底层驱动兼容；此配置项通常与时间敏感网络（如IEEE 802.1AS）相关，需要特别注意时间同步和精确度要求；在AUTOSAR CP 4.4标准中，确保此配置项的使用与标准定义的接口和行为一致。|
|多实例个数|1 - 1|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfSwitchIngressTimeStampIndicationFunction|
|描述|Enables/Disables to upper layers an ingress timestamp indication function.|
|描述|概述：EthIfSwitchIngressTimeStampIndicationFunction 配置项用于指定以太网接口模块在接收到带有时间戳的帧时调用的回调函数，以便应用层可以处理这些时间戳信息。|
|描述|注意：在使用此配置项时，需要确保网络管理器或应用层已经实现了相应的回调函数；此外，该功能通常与精确时间协议（如 IEEE 1588 PTP）相关，因此需要硬件和软件均支持该协议；最后，AUTOSAR CP 4.4标准中对于时间戳的处理可能有特定的要求，需要遵守这些要求以确保兼容性。|
|多实例个数|1 - 1|

### 1.9. EthIfTransceiver

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfTransceiver|
|描述|This container contains the configuration of EthIfTransceiver.|
|描述|概述：EthIfTransceiver配置项用于定义以太网接口传输器的属性，包括其标识符、所支持的速率以及与之关联的控制器信息等，以确保网络通信的正确配置和优化性能。|
|描述|注意：在配置EthIfTransceiver时，必须确保其标识符与实际硬件或虚拟接口相匹配；支持的速率应与网络需求和硬件能力相一致；正确配置关联的控制器信息，以保证网络层与物理层的有效通信。|
|说明|The usage of EthIfEthTrcvRef and EthIfWEthTrcvRefis exclusive OR.|
|多实例个数|0 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfTransceiverIdx|
|描述|This parameter provides a zero-based consecutive index of the Ethernet transceivers. Upper layer BSW modules and the Ethernet Interface itself use this index to identify an Ethernet tranceiver.|
|描述|概述：EthIfTransceiverIdx 是一个配置项，用于指定以太网接口控制器（Ethernet Interface Controller）与物理传输设备（Transceiver）之间的索引关系，确保数据能夠正确地在网络层和物理层之间传输。|
|描述|注意：在配置时需要确保EthIfTransceiverIdx与实际硬件连接的物理传输设备相匹配；索引值应在有效范围内，且不应与其他设备的索引冲突；在AUTOSAR CP 4.4标准中，此配置项应与其他网络配置参数一起被正确地集成和管理。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfEthTrcvRef|
|描述|Reference to an Ethernet transceiver, which is handled by a specific Ethernet transceiver driver.|
|描述|概述：EthIfEthTrcvRef是一个配置项，用于指定以太网接口（EthIf）与其所连接的以太网收发器（EthTrcv）之间的关联关系，确保数据能够在物理层正确传输。|
|描述|注意：在配置EthIfEthTrcvRef时，必须确保引用的以太网收发器已在系统中定义且配置正确；该配置项对于实现网络层与物理层之间的通信至关重要；在AUTOSAR CP 4.4标准中，确保该配置项与网络管理和诊断功能的兼容性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthTrcv/EthTrcvConfigSet/EthTrcvConfig|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|EthIfWEthTrcvRef|
|描述|Reference to an Wireless Ethernet transceiver, which is handled by a specific Wireless Ethernet transceiver driver.|
|描述|概述：EthIfWEthTrcvRef配置项用于定义以太网接口模块（EthIf）与特定的以太网收发器（Transceiver）之间的关联，确保数据能够在物理层正确传输。|
|描述|注意：确保每个EthIf模块正确地引用了对应的以太网收发器组件；在配置时需注意收发器的兼容性和支持的功能；对于使用多个网络接口的系统，正确的收发器引用对于网络性能和稳定性至关重要。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/WEthTrcv/WEthTrcvConfigSet/WEthTrcvConfig|

### 1.10. EthIfTxConfirmationConfig

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfTxConfirmationConfig|
|描述|Configuration of transmit indication callback functions.|
|描述|概述：EthIfTxConfirmationConfig 是一个配置项，用于定义以太网接口模块（EthIf）在传输帧成功后是否需要调用确认回调函数（TxConfirmation）。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保该配置与网络管理和诊断通信的需求相一致；如果网络管理不需要传输确认，可能会禁用此功能以减少开销；在配置时应考虑系统的实时性和性能要求。|
|多实例个数|0 - 255|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfTxConfirmationFunction|
|描述|Specifies transmit indication callback function|
|描述|概述：EthIfTxConfirmationFunction 是用于配置以太网接口传输确认的函数，该函数在数据包成功发送后被调用，用于通知上层协议数据传输的状态。|
|描述|注意：确保该函数的实现符合网络通信的实时性要求；函数应避免执行复杂或耗时的操作，以免影响网络性能；在配置时需确保与网络驱动和上层协议的兼容性。|
|多实例个数|1 - 1|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|FrameOwnerRef|
|描述|Reference to the frame owner to assign the TxIndication function.|
|描述|概述：FrameOwnerRef 是一个配置项，用于指定网络帧（如CAN帧、Ethernet帧等）的所有者，通常是指定哪个ECU或网络控制器负责处理该帧。|
|描述|注意：确保FrameOwnerRef正确指向负责处理特定帧的ECU或网络控制器；不正确的配置可能导致网络通信故障；在多ECU系统中，配置必须明确区分各ECU的责任和帧所有权。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EthIf/EthIfConfigSet/EthIfFrameOwnerConfig|

## 2. EthIfGeneral

| 容器属性 | 值（容器） |
|-|-|
|名称|EthIfGeneral|
|描述|This container contains the general configuration parameters of the Ethernet Interface.|
|描述|概述：EthIfGeneral 是一个配置容器，包含了以太网接口模块（EthIf）的通用配置参数，例如是否启用特定功能或者定义全局参数。|
|描述|注意：在配置EthIfGeneral时，需要确保所选参数与AUTOSAR CP 4.4标准中定义的参数一致；此外，配置时应考虑与其他网络层组件的兼容性；最后，对于启用的功能，必须确保底层硬件和驱动支持这些功能。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：EthIfDevErrorDetect 是一个配置参数，用于启用或禁用以太网接口模块（EthIf）的开发错误检测功能，以便在运行时监测和报告内部错误。|
|描述|注意：在生产环境中通常禁用此功能以优化性能；开发和测试阶段建议启用以便于问题诊断；确保此配置与系统的诊断策略和性能要求相一致。|
|说明|* true: detection and notification is enabled. * false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfEnableRxInterrupt|
|描述|Enables / Disables receive interrupt.|
|描述|概述：EthIfEnableRxInterrupt 是一个配置项，用于启用或禁用以太网接口（Ethernet Interface）的接收（Rx）中断，这有助于控制网络消息的接收时机。|
|描述|注意：在配置此项时，需要考虑实际的硬件能力和系统的实时性要求；不恰当的启用或禁用接收中断可能会影响系统的性能和响应时间；在AUTOSAR CP 4.4标准中，确保与其他网络管理配置项协同工作，避免配置冲突。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfEnableSignalQualityApi|
|描述|Enable/disable the APIs read and clear the signal quality.|
|描述|概述：EthIfEnableSignalQualityApi 用于启用或禁用以太网接口的信号质量检测API，允许软件获取网络信号质量相关信息。|
|描述|注意：在AUTOSAR CP 4.4中，默认情况下此API可能未启用，需要在系统配置中明确启用；确保硬件和底层驱动支持信号质量检测功能；使用此API可能会增加系统资源消耗，应评估性能影响。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfEnableTxInterrupt|
|描述|Enables / Disables the transmit interrupt.|
|描述|概述：EthIfEnableTxInterrupt 是一个配置项，用于启用或禁用以太网接口传输（Tx）中断，这有助于控制数据发送过程中的中断行为。|
|描述|注意：在配置此项时，需要考虑实际的硬件能力和系统的实时性要求；不恰当的中断配置可能会导致性能瓶颈或响应时间延迟；在AUTOSAR CP 4.4标准中，确保与通信堆栈的其他部分（如Eth驱动和中断管理模块）的配置保持一致。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfEnableWEthApi|
|描述|Enables / Disables API's for WEth / WEthTrcv|
|描述|概述：EthIfEnableWEthApi 配置项用于启用或禁用无线以太网接口。|
|描述|注意：在使用此配置项时，必须确保硬件和底层驱动支持无线功能；此配置项在AUTOSAR CP 4.4中应正确与底层网络管理模块集成；不当的使用可能导致系统行为不符合预期。|
|多实例个数|0 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetAndResetMeasurementDataApi|
|描述|Enables / Disables the Get and Reset Measurement Data API|
|描述|概述：EthIfGetAndResetMeasurementDataApi是一个配置项，用于启用或禁用以太网接口模块（EthIf模块）中的一个API，该API允许获取和重置网络接口的测量数据。|
|描述|注意：在使用此API时，需要确保它与系统的诊断和性能监控需求相匹配；如果启用，必须实现相应的回调函数来处理获取的数据；在AUTOSAR CP 4.4标准中，此API的使用应当遵循以太网接口模块的规范。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetBaudRate|
|描述|Enables / Disables GetBaudRate API.|
|描述|概述：EthIfGetBaudRate用于获取以太网接口的当前波特率，这是网络通信中的一个关键参数，影响数据传输速率。|
|描述|注意：在配置时需确保所设置的波特率与硬件和网络设计相匹配；AUTOSAR CP 4.4中并未直接定义此API，而是通过EthIf模块的配置参数间接影响；在实际应用中，需考虑网络的实际带宽和延迟要求。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetCounterState|
|描述|Enables / Disables GetCounterState API.|
|描述|概述：EthIfGetCounterState 是一个配置项，用于获取以太网接口的计数器状态，这可能包括帧计数、错误计数等，以监控网络接口的性能和问题。|
|描述|注意：在AUTOSAR CP 4.4中，确保使用此配置项时，已经定义了相应的计数器类型和错误状态；此配置项的使用可能需要硬件支持，因此需要检查底层以太网控制器是否提供了相应的计数器；在设计系统时，应考虑如何合理地利用这些计数器信息来优化网络性能和故障诊断。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetCtrlIdxList|
|描述|Enables / Disables GetCtrlIdxList API.|
|描述|概述：EthIfGetCtrlIdxList配置项定义了以太网接口模块（EthIf）可以访问的以太网控制器索引列表，用于映射以太网接口到底层的网络控制器。|
|描述|注意：在配置EthIfGetCtrlIdxList时，需要确保列表中的控制器索引与实际的以太网控制器硬件资源和底层驱动配置相匹配；索引值应该是唯一的，不应该有重复；在多控制器系统中，正确的控制器索引对于网络通信的正确性至关重要。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetTransceiverWakeupModeApi|
|描述|Enables / Disables EthIf_GetTransceiverWakeupMode API|
|描述|概述：EthIfGetTransceiverWakeupModeApi 是一个配置项，用于启用或禁用以太网接口模块中的API，该API允许获取网络唤醒模式的当前状态。|
|描述|注意：在AUTOSAR CP 4.4中，需要确保 EthIf 模块的配置与底层的网络硬件支持的功能相匹配；如果硬件不支持唤醒功能，则不应启用此API；此配置项的使用应与 ECU 的低功耗需求和网络管理策略保持一致。|
|多实例个数|0 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGetVlanIdSupport|
|描述|Enables / Disables GetVlanId API.|
|描述|概述：EthIfGetVlanIdSupport配置项用于指定以太网接口是否支持获取VLAN ID的功能，这使得软件能够识别和处理不同VLAN上的数据包。|
|描述|注意：在使用此配置项时，需要确保底层以太网驱动支持VLAN处理功能；如果项目不涉及VLAN的使用，此配置可以不启用以简化系统配置；AUTOSAR CP 4.4标准中对VLAN的支持可能受限于具体的硬件和软件平台，需仔细评估兼容性。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfGlobalTimeSupport|
|描述|Enables/Disables the Global Time APIs used amongst others by Global Time Synchronization over Ethernet.|
|描述|概述：EthIfGlobalTimeSupport 配置项用于指定以太网接口模块是否支持全局时间同步功能，这通常与 IEEE 802.1AS 或者其他时间同步协议的实现相关。|
|描述|注意：在配置时需确保硬件和底层驱动支持时间同步功能；如果项目不需要时间同步功能，则不应启用此配置项以避免不必要的资源消耗；AUTOSAR CP 4.4标准中，此配置项应与网络管理和时间同步相关的其他配置项保持一致性。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfSetForwardingModeApi|
|描述|Enables /disables EthIf_SetForwardingMode API.|
|描述|概述：EthIfSetForwardingModeApi 配置项用于启用或禁用以太网接口的转发模式设置API，允许上层软件根据需要动态地改变网络帧的转发行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该API与网络管理和诊断需求兼容；如果不需要动态改变转发模式，可以不启用此API以节省资源；在配置时应考虑系统安全性，防止未授权的访问或修改网络行为。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfStartAutoNegotiation|
|描述|Enables / Disables StartAutoNegotiation API.|
|描述|概述：EthIfStartAutoNegotiation 是一个配置项，用于指定以太网接口是否启动自动协商过程，以便自动选择最佳的数据速率和双工模式。|
|描述|注意：在配置此项时，需要确保硬件支持自动协商功能；如果网络环境不支持或存在兼容性问题，可能需要禁用自动协商；在静态配置的网络环境中，固定速率和双工模式可能更为适宜。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfSwitchManagementSupport|
|描述|Enables/Disables the Switch management APIs to support a Switch-port specific communication attribute access.|
|描述|概述：EthIfSwitchManagementSupport 配置项用于指定以太网接口是否支持交换管理功能，这涉及到对以太网交换机的配置和管理。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保网络管理功能与所使用的以太网驱动和硬件支持相匹配；如果项目不涉及以太网交换机或不需要交换管理功能，该配置项应设置为不支持；在配置时应考虑系统的网络拓扑和性能要求。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfVerifyConfigApi|
|描述|Enables /disables EthIf_VerifyConfig API.|
|描述|概述：EthIfVerifyConfigApi 是一个配置项，用于启用或禁用以太网接口模块（EthIf）中的配置验证API，该API用于在运行时检查PDU头部的配置参数是否与预期设置匹配。|
|描述|注意：在AUTOSAR CP 4.4标准中，配置验证API通常用于开发和测试阶段，以确保配置的正确性；在生产代码中，可能会因性能考虑而禁用此API；如果启用，需确保对性能影响有足够的理解和评估。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfVersionInfoApi|
|描述|Enables / Disables version info API|
|描述|概述：EthIfVersionInfoApi 是一个配置项，用于启用或禁用以太网接口模块（EthIf）的版本信息API，该API允许软件组件获取模块的版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，应当确保如果启用了版本信息API，那么必须实现相应的函数以返回正确的版本信息；如果不需要该功能，可以禁用以节省资源；在配置时应遵循项目的规范和需求，确保一致性和兼容性。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfVersionInfoApiMacro|
|描述|Enables / Disables version info API macro implementation.|
|描述|概述：EthIfVersionInfoApiMacro 是一个宏定义，用于启用或禁用以太网接口模块（EthIf）的版本信息API，该API提供模块的版本信息，如主版本号、次版本号和补丁版本号。|
|描述|注意：在AUTOSAR CP 4.4标准中，通常通过模块的配置参数来启用或禁用版本信息API，而不是直接使用宏定义；如果项目需要遵循严格的AUTOSAR标准，应通过配置参数而非宏定义来控制版本信息API的可用性；在实际应用中，需要确保如果启用了版本信息API，相应的函数实现应当提供准确的版本信息。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|EthIfWakeUpSupport|
|描述|Configures if wakeup is supported or not.|
|描述|概述：EthIfWakeUpSupport配置项用于指定以太网接口（Ethernet Interface）是否支持唤醒功能，这使得网络接口能够在接收到特定的网络唤醒信号时唤醒系统。|
|描述|注意：在配置EthIfWakeUpSupport时，需要确保硬件和底层驱动支持唤醒功能；此配置项对于实现低功耗网络通信场景至关重要；在AUTOSAR CP 4.4标准中，确保与网络管理需求和策略一致。|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfMainFunctionPeriod|
|描述|Specifies the period of main function EthIf_MainFunctionRx and EthIf_MainFunctionTx in seconds. Ethernet Interface does not require this information but the BSW scheduler.|
|描述|概述：EthIfMainFunctionPeriod 配置项定义了以太网接口模块（EthIf）主函数的调用周期，即主函数多久被调度执行一次。|
|描述|注意：该值需要与系统定时器和任务调度策略相匹配，以确保网络通信的时效性和性能；不正确的配置可能导致网络通信延迟或者资源利用不当；在配置时应考虑到与其他网络堆栈（如TCP/IP）的交互和依赖关系。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfMainFunctionStatePeriod|
|描述|Specifies the period of main function ethif_mainfunction_state in seconds. Ethernet Interface does not require this information but the BSW scheduler.|
|描述|概述：EthIfMainFunctionStatePeriod配置项指定了以毫秒为单位的周期时间，该时间用于调度以太网接口模块（EthIf）的主函数状态机，以处理不同的网络状态和控制命令。|
|描述|注意：该周期值应当与系统的实时性要求相匹配，确保网络状态能够及时更新；配置的周期值需要考虑到CPU的负载和以太网控制器的性能；在配置时应确保该值符合AUTOSAR的时间规范，不得低于模块的最小周期时间要求。|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfPortStartupActiveTime|
|描述|Denote the time delay after the mode "ETHTRCV_MODE_ACTIVE" of all EthIfSwitchPorts are requested via EthIf_StartAllPorts.|
|描述|概述：EthIfPortStartupActiveTime 配置项定义了以太网接口在启动时的活跃时间，这是接口在能够正常传输数据之前必须保持活跃的最小时间。|
|描述|注意：此参数的设置应考虑网络的启动时间和稳定性需求；过短的活跃时间可能导致网络连接不稳定；此配置项应与网络硬件和驱动程序的规格相匹配。|
|说明|This is only used for ports in EthIfSwtPortGroups which are not referenced by any EthIfController.|
|多实例个数|0 - 1|
|取值范围|0.001 - 65.535|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfSignalQualityCheckPeriod|
|描述|Specifies the period in units of seconds in which the signal quality it polled in the context of EthIf_MainfunctionState. The value shall be an integral multiple of EthIfMainFunctionStatePeriod.|
|描述|概述：EthIfSignalQualityCheckPeriod 配置项用于定义以太网接口模块（EthIf）检查网络信号质量的周期时间，通常以时间单位（如毫秒）表示。|
|描述|注意：该配置项的值应当根据网络的实际需求和性能指标来设置；过于频繁的检查可能会增加系统的开销，而检查周期过长可能导致信号质量问题不能及时被发现和处理；在设置此值时，还需考虑到硬件能力和系统中其他任务的调度策略。|
|多实例个数|0 - 1|

| 配置项属性 | 值（浮点型参数配置项） |
|-|-|
|名称|EthIfSwitchOffPortTimeDelay|
|描述|Denote the time delay after the mode "ETHTRCV_MODE_DOWN" of a EthIfSwitchPortGroup will be executed.|
|描述|概述：EthIfSwitchOffPortTimeDelay 配置项用于定义以太网接口在关闭端口后，延迟一定时间再进行物理层的断电，以确保所有在途数据包的处理。|
|描述|注意：该延迟时间应根据网络的具体需求和性能指标来设置，以避免数据丢失；过长的延迟时间可能会影响系统的能耗效率；在AUTOSAR CP 4.4标准中，此配置项的具体数值需要根据实际硬件和网络环境来调整。|
|说明|This is only used for EthIfSwtPortGroups which are not referenced by any EthIfController. The time delay shall be greater than the UdpNm timings, because UdpNm shall finish its shutdown handling. (Repeat Message State, Prepare Bus-Sleep state, Bus-Sleep state).|
|多实例个数|0 - 1|
|取值范围|0.001 - 65.535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfMaxTrcvsTotal|
|描述|Limits the total number of transceivers.|
|描述|概述：EthIfMaxTrcvsTotal 定义了以太网接口模块中可以配置的最大传输接收器（Transceiver）数量。|
|描述|注意：此参数的设置应考虑硬件能力和系统需求，以避免资源浪费或不足；在配置时需确保不超过AUTOSAR规范所支持的最大值；适当的配置可以优化网络性能和资源使用效率。|
|多实例个数|1 - 1|
|取值范围|1 - 255|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfRxIndicationIterations|
|描述|Maximum number of Ethernet frames per Ethernet controller polled from the Ethernet driver within EthIf_MainFunctionRx.|
|描述|概述：EthIfRxIndicationIterations配置项定义了以太网接口(EthIf)接收到帧后，上层回调函数(ethif_rxindication)被调用的次数，用于控制接收到的网络帧处理的迭代次数。|
|描述|注意：在配置此项时，需要确保迭代次数与系统的处理能力和实时性要求相匹配；过多的迭代可能会导致系统资源的过度消耗；此配置项在AUTOSAR CP 4.4中可能不直接存在，需根据实际的AUTOSAR版本和网络管理需求谨慎设置。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|EthIfTrcvLinkStateChgMainReload|
|描述|Specifies the frequency of transceiver link state change checks in each|
|描述|概述：EthIfTrcvLinkStateChgMainReload 配置项用于定义以太网接口传输器（Transceiver）链接状态变化时的主要重新加载行为，确保网络连接的稳定性和数据传输的连续性。|
|描述|注意：在AUTOSAR CP 4.4中，此配置项应确保与网络管理和诊断机制兼容；重载策略应考虑系统的实时性和安全要求；配置应通过专业的配置工具进行，以避免人为错误。|
|说明|period of main function EthIf_MainFunctionTx.|
|多实例个数|1 - 1|
|取值范围|1 - 255|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfMapMcalApiPrefix|
|描述|This configuration item maps the driver interfaces of different chips|
|描述|概述：EthIfMapMcalApiPrefix配置项用于定义以太网接口模块(EthIf)调用底层MCAL驱动API时使用的前缀，确保API调用的一致性和正确性。|
|描述|注意：前缀必须与实际MCAL驱动API的命名一致，以避免编译错误；该配置项对于实现模块间的解耦和模块化编程至关重要；在多个网络接口共存的系统中，正确的API前缀有助于区分不同的底层驱动调用。|
|说明|This configuration item maps the driver interfaces of different chips|
|多实例个数|1 - 1|

| 配置项属性 | 值（字符串参数配置项） |
|-|-|
|名称|EthIfPublicCddHeaderFile|
|描述|Defines header files for callback functions which shall be included in case of CDDs. Range of characters is 1.. 32.|
|描述|概述：EthIfPublicCddHeaderFile配置项用于指定以太网接口模块(EthIf)的公共复杂设备驱动(CDD)头文件的名称，该文件包含了CDD所需的公共类型定义和API原型。|
|描述|注意：文件名应确保与实际的头文件名一致，以便正确地包含在源代码中；路径应正确设置以确保编译器可以找到该头文件；在多供应商环境中，需确保头文件的命名不会导致命名冲突。|
|多实例个数|0 - 65535|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfEthSetCorrectionTimeApi|
|描述|This parameter defines the existence and the name of a callout function for adjusting the local ETH Reference clock in HW.|
|描述|概述：EthIfEthSetCorrectionTimeApi配置项用于启用或禁用以太网接口(EthIf)模块中的校正时间API，该API允许调整和同步以太网控制器的时间戳。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该API的使用与以太网控制器的硬件支持和时间敏感网络需求相匹配；如果不需要时间同步功能，可以禁用此API以节省资源；在配置时应考虑与其他网络管理功能的兼容性。|
|说明|This parameter defines the existence and the name of a callout function for adjusting the local ETH Reference clock in HW.|
|多实例个数|0 - 1|
|默认值|EthIf_Eth_SetCorrectionTime|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfEthSetGlobalTimeApi|
|描述|This parameter defines the existence and the name of a callout function for adjusting the global ETH Reference clock in HW.|
|描述|概述：EthIfEthSetGlobalTimeApi配置项用于启用或禁用以太网接口模块（EthIf）中的全局时间设置API，该API允许设置以太网控制器的内部时钟。|
|描述|注意：在使用此配置项时，需要确保底层的以太网控制器支持时间同步功能；此外，如果启用了全局时间API，应当确保与网络时间同步协议（如PTP）的集成兼容；在AUTOSAR CP 4.4标准中，此配置项应与其他与时间同步相关的配置项保持一致性。|
|说明|This parameter defines the existence and the name of a callout function for adjusting the global ETH Reference clock in HW.|
|多实例个数|0 - 1|
|默认值|EthIf_Eth_SetGlobalTime|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfTrcvGetLinkStateApi|
|描述|This parameter defines the existence and the name of a callout function for getting linkstate of transceiver.|
|描述|概述：EthIfTrcvGetLinkStateApi是一个配置项，用于定义是否启用以太网接口传输层的链路状态获取API，允许软件检查网络接口的当前链路状态。|
|描述|注意：在AUTOSAR CP 4.4标准中，启用此API可能需要额外的硬件支持和驱动实现；如果不需要实时监控链路状态，可以考虑不启用以节省资源；确保与底层驱动和硬件的兼容性。|
|说明|This parameter defines the existence and the name of a callout function for getting linkstate of transceiver.|
|多实例个数|0 - 1|
|默认值|ethif_ethtrcv_get_linkstate|

| 配置项属性 | 值（函数名配置项） |
|-|-|
|名称|EthIfSwtGetLinkStateApi|
|描述|This parameter defines the existence and the name of a callout function for getting linkstate of switch port.|
|描述|概述：EthIfSwtGetLinkStateApi 是一个配置项，用于定义以太网接口模块是否支持通过API获取交换机端口的链路状态。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此API的使用与以太网交换机模块的配置一致；如果不需要此功能，应禁用以节省资源；在设计网络管理策略时，考虑链路状态变化对通信的影响。|
|说明|This parameter defines the existence and the name of a callout function for getting linkstate of switch port.|
|多实例个数|0 - 1|
|默认值|EthIf_Swt_GetLinkState|

