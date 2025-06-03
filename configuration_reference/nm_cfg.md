# Nm 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Nm|
|描述|The Generic Network Management Interface module|
|描述|概述：Nm (Network Management) 配置项用于定义网络管理策略，包括网络节点的控制策略和网络唤醒策略，以确保网络的稳定性和节点的正确唤醒。|
|描述|注意：在配置Nm时，必须确保与车辆的网络拓扑和其他网络参与者兼容；应遵循AUTOSAR CP 4.4标准中对于网络管理的具体要求和协议；配置错误可能导致网络通信故障或节点响应不当。|
|多实例个数|0 - 1|

## 1. NmChannelConfig

|容器属性|值（容器）|
|---|---|
|名称|NmChannelConfig|
|描述|This container contains the configuration (parameters) of the bus channel(s). The channel parameter shall be harmonized within the whole communication stack.|
|描述|概述：NmChannelConfig 是用于配置网络管理通道的参数，包括网络管理策略、节点标识符和通道特定的属性，以便控制网络节点的行为。|
|描述|注意：在配置NmChannelConfig时，需要确保通道的参数与网络的拓扑结构和节点的需求相匹配；AUTOSAR CP 4.4标准可能对某些参数的取值范围或者默认值有特定要求，需要参照标准文档进行配置；在多通道网络管理系统中，每个NmChannelConfig必须有唯一的标识符，以避免配置冲突。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmActiveCoordinator|
|描述|This parameter indicates whether a NM channel - part of a Nm Coordination cluster - will be coordinated actively (NmActiveCoordinator = TRUE) or passively (NmActiveCoordinator = FALSE).|
|描述|概述：NmActiveCoordinator 配置项用于定义网络管理中的主节点，该节点负责协调网络上的通信和管理任务。|
|描述|注意：确保在网络配置中只指定一个活跃的协调器节点，以避免管理冲突；该节点应具备足够的资源和优先级来处理网络管理任务；在分布式系统中，选择合适的节点作为协调器非常关键，以保证网络的稳定性和效率。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmChannelSleepMaster|
|描述|This parameter shall be set to indicate if the sleep of this network can be absolutely decided by the local node only and that no other nodes can oppose that decision.|
|描述|概述：NmChannelSleepMaster配置项用于定义网络管理通道（NmChannel）进入睡眠状态的条件，确保网络在不需要通信时能够有效地进入低功耗模式。|
|描述|注意：该配置项需要与网络唤醒和睡眠逻辑紧密配合，确保网络状态转换的正确性；在配置时需考虑网络的实际使用场景和功耗要求；AUTOSAR CP 4.4标准中未明确列出此配置项，可能属于特定实现或版本的扩展。|
|说明|If this parameter is set to TRUE, the Nm shall assume that the channel is always ready to go to sleep and that no calls to Nm_RemoteSleepIndication or Nm_RemoteSleepCancellation will be made from the \<BusNm\> representing this channel. If this parameter is set to FALSE, the Nm shall not assume that the network is ready to sleep until a call has been made to Nm_RemoteSleepCancellation.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmComUserDataSupport|
|描述|This parameter indicates whether on a NM channel user data is accessed via Com signals or by SetUserData API.|
|描述|概述：NmComUserDataSupport配置项用于指定网络管理通信是否支持用户数据的传输，这允许在网络管理消息中传递额外的用户定义数据。|
|描述|注意：在使用此配置项时，需要确保网络管理框架和通信堆栈支持用户数据的传输；用户数据的大小和格式应符合网络协议和AUTOSAR标准的要求；在设计用户数据传输时，应考虑数据的安全性和隐私保护。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmPassiveModeEnabled|
|描述|This parameter indicates whether a NM channel is active,e.g. can request communication and keep the bus awake, or passive, e.g. can just be woken up and kept awake by other ECUs.|
|描述|概述：NmPassiveModeEnabled是一个配置项，用于指定网络管理（Network Management）是否在被动模式下运行，这意味着节点可以接收但不会主动发送网络管理消息。|
|描述|注意：在设计网络管理策略时，确保该配置与网络的需求和其他节点的配置兼容；被动模式下的节点不会对网络管理请求主动响应，可能影响网络的性能和诊断；AUTOSAR CP 4.4标准支持此配置，但实现时需考虑与具体的网络管理协议的兼容性。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmStateReportEnabled|
|描述|Specifies if the NMS shall be set for the corresponding network.|
|描述|概述：NmStateReportEnabled 用于配置网络管理（Network Management）状态报告功能的启用或禁用，控制是否生成和发送网络状态的报告。|
|描述|注意：在设计网络管理策略时，应根据系统需求和资源限制考虑是否启用此功能；启用状态报告可能会增加网络负载和处理开销；确保与系统中其他网络管理配置的兼容性。|
|说明|false: No NMS shall be set true: The NMS shall be set|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmSynchronizingNetwork|
|描述|If this parameter is true, then this network is a synchronizing network for the NM coordination cluster which it belongs to. The network is expected to call Nm_SynchronizationPoint() at regular intervals.|
|描述|概述：NmSynchronizingNetwork配置项用于指定网络管理（Network Management）模块是否负责同步网络上的通信节点，以确保网络时间同步和数据一致性。|
|描述|注意：在配置NmSynchronizingNetwork时，需要确保网络上所有节点的时间同步机制兼容；此配置项对于实现确定性网络通信特别重要；在AUTOSAR CP 4.4标准中，不所有的通信堆栈都支持网络时间同步功能，因此需要根据具体的通信协议栈特性来配置。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|NmCoordClusterIndex|
|描述|If this parameter is undefined for a channel, the corresponding bus does not belong to an NM coordination cluster.|
|描述|概述：NmCoordClusterIndex是用于标识网络管理(Nm)中协调器所属的网络群集的索引，确保网络管理协调器能够正确地识别并管理其所负责的网络群集。|
|描述|注意：该索引必须唯一地对应于一个网络群集，以避免网络管理的混乱；在配置时需确保索引与实际网络群集的对应关系准确无误；AUTOSAR CP 4.4标准中对NmCoordClusterIndex的具体数值范围没有特殊限制，但应根据实际项目需求合理分配。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|NmComMChannelRef|
|描述|Reference to the corresponding ComM Channel.|
|描述|概述：NmComMChannelRef 是一个配置参数，用于将网络管理（Nm）模块与通信管理（ComM）模块的通道相关联，确保网络管理能够控制相应的通信通道状态。|
|描述|注意：在配置时需确保Nm模块和ComM模块的通道正确对应，以便于正确的网络状态管理；不正确的配置可能导致网络管理功能异常；在多通道系统中，每个Nm通道应该映射到唯一的ComM通道。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|NmStateReportSignalRef|
|描述|Reference to the signal for setting the NMS by calling Com_SendSignal for the respective channel.|
|描述|概述：NmStateReportSignalRef配置项用于引用网络管理状态报告信号，它指定了用于报告网络管理（Nm）状态的信号，以便在车辆网络中传递节点的网络管理状态信息。|
|描述|注意：确保引用的信号与实际的网络管理状态报告需求相匹配；在配置时需注意信号的大小和格式是否符合AUTOSAR标准；在多网络环境中，应确保每个网络的NmStateReportSignalRef配置不会相互冲突。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Com/ComConfig/ComSignal|

### 1.1. NmBusType

|容器属性|值（容器）|
|---|---|
|名称|NmBusType|
|多实例个数|1 - 1|

#### 1.1.1. NmGenericBusNmConfig

|容器属性|值（容器）|
|---|---|
|名称|NmGenericBusNmConfig|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|NmGenericBusNmShutdownTime|
|描述|This parameter shall be|
|描述|概述：NmBusType配置项用于指定网络管理（Network Management）所使用的总线类型，如CAN、FR（FlexRay）或者LIN等，以确保网络管理策略与所使用的总线技术兼容。|
|描述|注意：在AUTOSAR CP 4.4中，必须确保NmBusType与项目中实际使用的总线类型一致；不同的总线类型可能需要不同的网络管理策略和配置；更改总线类型可能需要重新配置网络管理相关的参数和策略。|
|说明|used to calculate shutdown delay time.|
|多实例个数|1 - 1|
|取值范围|0 - Inf|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|NmGenericBusNmPrefix|
|描述|The prefix which identifies the generic \<BusNm\>. This will be used to determine the API name to be called by Nm for the provided interfaces of the \<BusNm\>. This string will used for the module prefix before the "_" character in the API call name.|
|描述|概述：NmGenericBusNmConfig是用于配置网络管理（Network Management）中通用总线网络管理模块的参数，这些参数决定了网络管理策略和行为，如网络唤醒和休眠策略。|
|描述|注意：在配置NmGenericBusNmConfig时，需要确保所选参数与车辆网络的实际需求相匹配；AUTOSAR CP 4.4标准中对于网络管理的配置和实现提供了详细的指导，需要仔细遵循；特别注意与具体总线类型（如CAN, LIN等）相关的配置参数，以确保网络管理模块的正确集成和操作。|
|多实例个数|1 - 1|

#### 1.1.2. NmStandardBusNmConfig

|容器属性|值（容器）|
|---|---|
|名称|NmStandardBusNmConfig|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|NmGenericBusNmPduRxIndication|
|描述|Function called to notify the reception of a NmPdu.|
|描述|概述：NmGenericBusNmPduRxIndication是一个配置项，用于指定网络管理（Network Management, NM）接收到通用总线网络管理PDU（Protocol Data Unit）时的指示函数。|
|描述|注意：在配置时需要确保该指示函数与实际的网络管理接收回调函数相匹配；该配置项通常由网络管理模块的开发者提供，需要与具体实现的网络协议栈保持一致；在AUTOSAR CP 4.4标准中，应当遵循相应的模块接口规范来实现该指示函数。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|NmStandardBusType|
|描述|Identifies the bus type of the channel for standard AUTOSAR \<BusNm\>s and is used to determine which set of API calls to be called by Nm for the \<BusNm\>s.|
|描述|概述：NmStandardBusType 定义了网络管理系统中使用的标准总线类型，如CAN, LIN, 或者 FlexRay。|
|描述|注意：选择正确的总线类型对于网络管理的配置和性能至关重要；确保总线类型与实际硬件和网络设计相匹配；在AUTOSAR CP 4.4中，总线类型应详细定义以避免配置错误。|
|说明|Note: The Ethernet bus' NM is UdpNm !|
|多实例个数|1 - 1|

## 2. NmGlobalConfig

|容器属性|值（容器）|
|---|---|
|名称|NmGlobalConfig|
|描述|This container contains all global configuration parameters of the Nm Interface.|
|描述|概述：NmGlobalConfig 是网络管理（Network Management）的全局配置参数，用于定义网络管理模块的全局属性，如网络管理策略、超时时间等。|
|描述|注意：在配置NmGlobalConfig时，需要确保其参数与网络的实际需求相匹配，以避免网络稳定性问题；此外，应当注意与其他网络管理相关配置项的一致性，如NmChannelConfig；AUTOSAR CP 4.4标准中可能对某些参数的取值范围或默认值有特定要求，需要遵守这些规定以保证兼容性。|
|多实例个数|1 - 1|

### 2.1. NmGlobalConstants

|容器属性|值（容器）|
|---|---|
|名称|NmGlobalConstants|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|NmNumberOfChannels|
|描述|Number of NM channels allowed within one ECU.|
|描述|概述：NmGlobalConstants 定义了网络管理（Network Management）模块全局常量，这些常量用于整个AUTOSAR项目中网络管理的配置和行为控制。|
|描述|注意：确保这些常量的值符合项目的网络协议规范和需求；修改这些常量可能会影响网络管理的性能和功能；在多网络配置中，应考虑不同网络对常量值的可能不同需求。|
|多实例个数|1 - 1|
|取值范围|1 - 255|

### 2.2. NmGlobalFeatures

|容器属性|值（容器）|
|---|---|
|名称|NmGlobalFeatures|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmBusSynchronizationEnabled|
|描述|Pre-processor switch for enabling bus synchronization support of the \<BusNm\>s. This feature is required for NM Coordinator nodes only.|
|描述|概述：NmNumberOfChannels 配置项指定了网络管理（Network Management, Nm）模块中通道的数量，这是用于管理车辆网络中不同通信通道的网络管理实例的数量。|
|描述|注意：在配置NmNumberOfChannels时，需要确保该值与实际在车辆网络中使用的通信通道数量相匹配；超出实际通道数量的配置可能会导致资源浪费；如果配置的通道数量少于实际使用的通道，可能会导致某些通道无法被正确管理。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmCarWakeUpRxEnabled|
|描述|Enables or disables CWU detection.|
|描述|概述：NmGlobalFeatures 配置项定义了网络管理全局特性，包括网络管理策略和协议的全局参数。|
|描述|注意：确保配置与网络协议和车辆项目要求一致；在多网络配置中，注意各网络间的特性兼容性；遵循AUTOSAR CP 4.4标准中对网络管理特性的具体要求。|
|说明|FALSE - CarWakeUp not supported TRUE - CarWakeUp supported|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmComControlEnabled|
|描述|Pre-processor switch for enabling the Communication Control support.|
|描述|概述：NmComControlEnabled 是一个配置项，用于启用或禁用网络管理通信控制功能，该功能允许控制节点是否参与网络管理通信。|
|描述|注意：在配置时需确保该选项与系统的网络管理需求一致；如果禁用，节点将不会参与到网络管理的通信中，可能影响网络的稳定性和节点的可达性；在多节点网络中，每个节点的此配置应根据其角色和需求单独考虑。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmCoordinatorSupportEnabled|
|描述|Pre-processor switch for enabling NM Coordinator support.|
|描述|概述：NmCoordinatorSupportEnabled 是一个配置项，用于启用或禁用网络管理协调器的支持，这有助于在多个网络管理器之间协调网络管理消息和状态。|
|描述|注意：在配置时，需要确保网络管理需求是否需要协调器支持；如果启用，必须确保系统中所有网络管理器都兼容协调器机制；在不需要复杂网络管理协调的简单系统中，可以禁用以节省资源。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmCoordinatorSyncSupport|
|描述|Enables/disables the coordinator synchronisation support.|
|描述|概述：NmCoordinatorSyncSupport 配置项用于定义网络管理协调器是否支持同步机制，以确保网络中不同节点的状态同步。|
|描述|注意：在配置时需确保网络中所有节点的兼容性和支持性；不正确的配置可能导致网络同步问题；AUTOSAR CP 4.4标准中对此项的具体实现细节有严格规定，需遵守标准指导。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmPduRxIndicationEnabled|
|描述|Pre-processor switch for enabling the PDU Rx Indication.|
|描述|概述：NmPduRxIndicationEnabled 是一个配置项，用于启用或禁用网络管理PDU（协议数据单元）接收指示，这决定了是否在接收到网络管理PDU时通知相应的网络管理模块。|
|描述|注意：在配置时需确保该选项与网络管理的需求一致；如果网络管理模块需要知道何时接收到PDU以执行相应的动作，则应启用此选项；在不需要此通知的情况下，禁用可以节省系统资源。|
|多实例个数|1 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|NmPduRcvIndCallback|
|描述|Define the callback function that shall be invoked in case of NM pdu indication.|
|描述|概述：NmPduRcvIndCallback 是一个配置项，用于定义当网络管理PDU（协议数据单元）被接收时触发的回调函数。|
|描述|注意：确保回调函数的实现符合网络管理的要求和时间敏感性；回调函数应避免执行长时间或复杂的操作，以免影响系统性能；在配置时需确保回调函数与接收的PDU类型正确匹配。|
|多实例个数|0 - 1|
|IMPLEMENTATION-CONFIG-CLASSES|
                            |

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmRemoteSleepIndEnabled|
|描述|Pre-processor switch for enabling Remote Sleep Indication support. This feature is required for a Gateway or Nm Coordinator functionality.|
|描述|概述：NmRemoteSleepIndEnabled是一个配置项，用于启用或禁用网络管理（Network Management, NM）中远程睡眠指示的功能，该功能允许节点检测到网络上其他节点是否进入了睡眠状态。|
|描述|注意：在配置NmRemoteSleepIndEnabled时，需要确保它与网络上其他节点的配置兼容；如果网络中的某些节点需要使用远程睡眠指示功能，那么所有相关节点都应相应地配置此选项；此外，开启此功能可能会影响网络的功耗和唤醒策略，因此在设计时应考虑到这些因素。|
|说明|Note that this feature should not be used if all NM channels have Passive Mode enabled.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmStateChangeIndEnabled|
|描述|Pre-processor switch for enabling the Network Management state change notification.|
|描述|概述：NmStateChangeIndEnabled 配置项用于启用或禁用网络管理状态变更指示功能，允许系统在网络管理状态发生变化时接收通知。|
|描述|注意：在使用此配置时，确保相关的网络管理模块已正确配置以支持状态变更通知；不恰当的使用可能导致系统响应不及时或错误的状态信息传递；此配置项应与系统的实际需求和网络管理策略相匹配。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmUserDataEnabled|
|描述|Pre-processor switch for enabling User Data support.|
|描述|概述：NmUserDataEnabled是一个配置项，用于指定网络管理（Network Management）消息中是否启用用户数据字段，允许在网络管理消息中传输额外的用户定义数据。|
|描述|注意：在AUTOSAR CP 4.4标准中，启用用户数据需要确保网络协议支持用户数据字段；用户数据的大小和格式应符合网络协议规范；在设计用户数据时，需考虑网络带宽和性能影响。|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|NmGlobalCoordinatorTime|
|描述|This parameter defines the maximum shutdown time of a connected and coordinated NM-Cluster.|
|描述|概述：NmGlobalCoordinatorTime配置项用于定义网络管理全局协调器的时间参数，这些参数控制网络唤醒和休眠的时间行为。|
|描述|注意：在配置NmGlobalCoordinatorTime时，需要确保其值满足网络管理的时间要求，并且与其他网络参与者的时间设置保持一致；此外，该配置项的值应当符合AUTOSAR CP 4.4标准中对于时间参数的规定；不正确的时间配置可能导致网络管理功能异常，如唤醒和休眠机制失效。|
|说明|Note:This includes nested connections.|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|NmCarWakeUpCallout|
|描述|Name of the callout function to be called if Nm_CarWakeUpIndication() is called. If this parameter is not configured, the Nm will call BswM_Nm_CarWakeUpIndication.|
|描述|概述：NmCarWakeUpCallout 是一个配置项，用于定义网络管理（Network Management, NM）模块在车辆唤醒事件发生时调用的回调函数。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该回调函数与系统唤醒策略一致；回调函数需要在系统设计时确定，并在实现时遵循AUTOSAR的规范；在配置时应注意与其他唤醒源的协调和冲突管理。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|NmStateChangeIndCallback|
|描述|Define the callback function that shall be invoked in case of NM state changes.|
|描述|概述：NmStateChangeIndCallback配置项用于定义网络管理（Network Management）状态变化时的回调函数，该函数会在网络状态发生变化时被调用，以便执行相应的处理逻辑。|
|描述|注意：确保回调函数的实现遵循AUTOSAR标准中对于时间和资源消耗的限制；在设计回调逻辑时，考虑网络状态变化的频繁程度，避免产生过大的系统开销；AUTOSAR CP 4.4标准中对于NmStateChangeIndCallback的使用和配置有详细规定，确保配置的一致性和正确性。|
|多实例个数|0 - 1|
|IMPLEMENTATION-CONFIG-CLASSES|
                            |

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|NmCallbacksPrototypeHeader|
|描述|This parameter describes the SectionInitializationPolicys for which a particular RTE initialization strategy applies.|
|描述|概述：NmCallbacksPrototypeHeader 用于定义网络管理（Network Management）模块中的回调函数原型的头文件，这些回调函数用于处理网络状态变化和错误处理。|
|描述|注意：确保回调函数符合AUTOSAR标准中定义的原型和参数列表；回调函数的实现需要保证高效且不阻塞网络通信；在多网络配置中，正确区分和处理各网络的回调。|
|说明|NmCallbacksPrototypeHeader|
|多实例个数|0 - inf|

### 2.3. NmGlobalProperties

|容器属性|值（容器）|
|---|---|
|名称|NmGlobalProperties|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：NmGlobalProperties配置项定义了网络管理（Network Management）全局属性，包括网络管理策略、通信控制策略等，适用于整个系统的网络管理配置。|
|描述|注意：在AUTOSAR CP 4.4中，确保网络管理策略与系统需求相匹配；全局属性应与各个ECU的局部配置协调一致；修改全局属性可能会影响系统内所有网络管理参与者的行为。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|NmVersionInfoApi|
|描述|Pre-processor switch for enabling Version Info API support.|
|描述|概述：NmDevErrorDetect 是一个配置参数，用于启用或禁用网络管理（Network Management）模块中的开发错误检测功能。|
|描述|注意：在生产环境中通常禁用此功能以优化性能；开发和测试阶段建议启用以便捕捉潜在错误；确保与系统的诊断策略和错误处理机制一致。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|NmCycletimeMainFunction|
|描述|The period between successive calls to the Main Function of the NM Interface in seconds.|
|描述|概述：NmVersionInfoApi 用于提供网络管理模块的版本信息，使得软件模块能够查询和显示其实现的版本。|
|描述|注意：在AUTOSAR CP 4.4中，确保该API的实现符合标准的版本信息格式；通常该API不应该被频繁调用以避免性能影响；应当在模块初始化时调用以记录版本信息。|
|多实例个数|0 - 1|
|取值范围|0 - Inf|
