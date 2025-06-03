# CanNm 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|CanNm|
|描述|Configuration Parameters for the Can Nm module.|
|描述|概述：CanNm是AUTOSAR网络管理模块的配置项，用于定义控制器局域网络（CAN）网络管理策略，包括网络请求和释放机制，以及节点的唤醒和睡眠行为。|
|描述|注意：在配置CanNm时，需要确保其参数与网络的实际需求相匹配，例如网络唤醒和睡眠策略；CanNm配置应与其他网络管理模块（如ComM和Nm）协同工作，以保证网络管理的一致性；AUTOSAR CP 4.4标准可能引入了新的属性或者对旧属性有所调整，因此在配置时应参考最新的标准文档。|
|多实例个数|0 - 1|

## 1. CanNmGlobalConfig

|容器属性|值（容器）|
|---|---|
|名称|CanNmGlobalConfig|
|描述|This container contains the global configuration parameter of the CanNm. The parameters and the parameters of the sub containers shall be mapped to the C data type CanNm_ConfigType (for parameters where it is possible) which is passed to the CanNm_Init function.|
|描述|概述：CanNmGlobalConfig是用于配置CAN网络管理（CAN Network Management）全局参数的配置项，包括网络管理策略、消息周期等关键参数，以确保网络的稳定性和高效通信。|
|描述|注意：在配置CanNmGlobalConfig时，需要确保所选参数与网络的实际需求相匹配，避免因配置不当导致网络通信效率低下或不稳定；此外，AUTOSAR CP 4.4标准中对于某些参数有明确的取值范围或条件限制，需要仔细遵守；最后，考虑到网络的可扩展性和兼容性，应当谨慎选择静态配置与动态配置的比例。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmBusLoadReductionEnabled|
|描述|Pre-processor switch for enabling busload reduction support.|
|描述|概述：CanNmBusLoadReductionEnabled是一个配置项，用于启用或禁用CAN网络管理（CAN NM）中的总线负载减少功能，以降低网络上的数据传输量。|
|描述|注意：在配置此项时，需要确保网络的带宽和性能要求得到满足；此功能的使用可能会影响到网络节点之间的通信效率和响应时间；在启用此功能前，应当评估网络的负载情况和各节点的通信需求。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmBusSynchronizationEnabled|
|描述|Pre-processor switch for enabling bus synchronization support. This feature is required for gateway nodes only.|
|描述|概述：CanNmBusSynchronizationEnabled是一个配置项，用于启用或禁用CAN网络管理（CAN NM）的总线同步功能，该功能允许节点在没有主节点的情况下同步到网络上的其他节点。|
|描述|注意：在使用此配置时，需要确保网络中的其他节点也支持总线同步功能；如果网络配置不正确，可能会导致网络同步失败；此功能在某些特定的网络配置中可能不被支持，需参考具体的AUTOSAR CP版本和网络管理需求。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmComControlEnabled|
|描述|Pre-processor switch for enabling the Communication Control support.|
|描述|概述：CanNmComControlEnabled是一个配置项，用于启用或禁用网络管理（Network Management）通过CAN通信控制器的通信能力。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用此配置项时考虑网络的需求和特定的应用场景；此配置项的启用或禁用会直接影响到网络节点的通信行为和性能；在配置时需确保与系统中其他网络管理配置项的兼容性和一致性。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmComUserDataSupport|
|描述|Preprocessor switch for enabling the Tx path of Com User Data.|
|描述|概述：CanNmComUserDataSupport配置项用于指定网络管理是否支持通过CAN网络传输用户数据，这允许在网络管理消息中携带额外的用户数据。|
|描述|注意：在启用此功能时，需要确保网络带宽足以支持额外的用户数据传输，且不会影响网络管理消息的实时性和可靠性；此配置项的使用应与网络设计和需求紧密相关，确保网络的稳定性和性能；在AUTOSAR CP 4.4标准中，此配置项的使用应遵循相关的网络管理通信规范。|
|说明|Use case: Setting of NMUserData via SWC.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmCoordinatorSyncSupport|
|描述|Enables/disables the coordinator synchronization support.|
|描述|概述：CanNmCoordinatorSyncSupport配置项用于指定网络管理协调器（Nm Coordinator）是否支持同步功能，这有助于在多个网络管理器之间同步状态和控制信息。|
|描述|注意：该配置项对于实现跨多个网络通信的系统尤为重要；确保在设计阶段明确是否需要该同步功能，以便正确配置；AUTOSAR CP 4.4标准中，对于网络管理的同步机制有明确的规范，需要遵循这些规范以保证系统的兼容性和稳定性。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：CanNmDevErrorDetect是一个配置参数，用于启用或禁用CAN网络管理模块中的开发错误检测功能，这有助于在开发和测试阶段发现潜在的错误。|
|描述|注意：在生产代码中通常会禁用此功能以节省资源和避免不必要的性能开销；确保在开发和测试阶段根据需要启用此功能以进行适当的错误检测；在最终交付的产品中，应根据项目要求和优化策略来配置此参数。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmGlobalPnSupport|
|描述|Pre-processor switch for enabling partial networking support globally.|
|描述|概述：CanNmGlobalPnSupport是一个配置项，用于全局定义网络管理是否支持部分网络功能（Partial Networking），即是否允许网络管理模块控制ECU进入或退出低功耗模式。|
|描述|注意：在使用CanNmGlobalPnSupport时，需要确保所有网络节点都支持部分网络功能；如果部分网络未在整个网络中得到支持，则该配置可能不会生效；此配置项对于降低网络空闲时的能耗至关重要。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmImmediateRestartEnabled|
|描述|Pre-processor switch for enabling the immediate transmission of a NM PDU upon bus-communication request in Prepare-Bus-Sleep mode.|
|描述|概述：CanNmImmediateRestartEnabled 是一个布尔配置参数，用于启用或禁用CAN网络管理（CAN NM）中的立即重启功能，该功能允许在网络管理控制器检测到网络释放后立即重新加入网络。|
|描述|注意：在配置此参数时，需要确保它与系统的网络管理需求一致；如果启用，可能会影响网络的稳定性和带宽，因为节点可能会频繁地尝试重新加入网络；在禁用时，节点在网络释放后可能会有更长的延迟才能重新加入网络。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmImmediateTxconfEnabled|
|描述|Enable/disable the immediate tx confirmation.|
|描述|概述：CanNmImmediateTxconfEnabled是一个配置项，用于启用或禁用CAN网络管理中立即传输确认的功能，这有助于在需要快速响应的场景下提高通信效率。|
|描述|注意：在启用此功能时，需要确保网络的负载和带宽可以支持增加的传输频率；此配置可能会影响到网络的整体性能，特别是在高负载情况下；根据AUTOSAR CP 4.4标准，确保与网络管理需求和策略相一致。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPassiveModeEnabled|
|描述|Pre-processor switch for enabling support of the Passive Mode.|
|描述|概述：CanNmPassiveModeEnabled 是一个配置参数，用于启用或禁用CAN网络管理（CAN NM）的被动模式，这种模式下节点不会主动发送NM消息，但仍然能够接收和处理它们。|
|描述|注意：在被动模式下，节点不会参与网络管理的主动行为，如发送NM消息；这可能影响网络的管理和节点的唤醒能力；确保在不需要节点参与网络管理决策时使用此模式。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPduRxIndicationEnabled|
|描述|Pre-processor switch for enabling the PDU Rx Indication.|
|描述|概述：CanNmPduRxIndicationEnabled配置项用于启用或禁用CAN网络管理接收PDU（协议数据单元）的指示功能，这决定了是否通知上层软件接收到新的PDU。|
|描述|注意：在使用此配置时，确保与网络管理需求相匹配；如果禁用，可能会影响网络管理的性能和功能；此配置项在AUTOSAR CP 4.4中应保持与网络管理策略的一致性。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPnEiraCalcEnabled|
|描述|Specifies if CanNm calculates the PN request information for internal an external requests. (EIRA)|
|描述|概述：CanNmPnEiraCalcEnabled 配置项用于启用或禁用对 EIRA（Extended Identifier Reception Allocation）的计算，这是网络管理中用于识别远程唤醒请求的功能。|
|描述|注意：在使用部分网络管理功能时，确保此配置与系统需求一致；如果不需要远程唤醒功能，可以禁用以节省资源；AUTOSAR CP 4.4 标准中此配置应正确设置以保证网络管理的正确实现。|
|说明|true: PN request are calculated false: PN request are not calculated|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmRemoteSleepIndEnabled|
|描述|Pre-processor switch for enabling remote sleep indication support. This feature is required for gateway nodes only.|
|描述|概述：CanNmRemoteSleepIndEnabled配置项用来表示CAN网络管理远程睡眠指示是否启用。|
|描述|注意：在使用部分网络管理功能时，确保此配置与系统需求一致；如果不需要远程睡眠功能，可以禁用以节省资源；AUTOSAR CP 4.4 标准中此配置应正确设置以保证网络管理的正确实现。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmStateChangeIndEnabled|
|描述|Pre-processor switch for enabling the CAN NM state change notification.|
|描述|概述：CanNmStateChangeIndEnabled配置项用来表示是否启用了CAN网络管理中的状态改变指示功能。|
|描述|注意：在使用部分网络管理功能时，确保此配置与系统需求一致；如果不需要状态改变通知功能，可以禁用以节省资源；AUTOSAR CP 4.4 标准中此配置应正确设置以保证网络管理的正确实现。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmUserDataEnabled|
|描述|Pre-processor switch for enabling user data support.|
|描述|概述：CanNmUserDataEnabled配置项用来表示是否启用了CAN网络管理中的用户数据传输功能。|
|描述|注意：在使用部分网络管理功能时，确保此配置与系统需求一致；如果不需要用户数据设置功能，可以禁用以节省资源；AUTOSAR CP 4.4 标准中此配置应正确设置以保证网络管理的正确实现。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmVersionInfoApi|
|描述|Pre-processor switch for enabling version info API support.|
|描述|概述：CanNmVersionInfoApi配置项用于访问CAN网络管理模块版本信息的应用程序接口。 通过调用这个接口，应用程序可以获取CAN网络管理模块的版本信息，例如主版本号、次版本号、补丁版本号等。|
|描述|注意：在使用部分网络管理功能时，确保此配置与系统需求一致；如果不需要版本信息功能，可以禁用以节省资源；AUTOSAR CP 4.4 标准中此配置应正确设置以保证网络管理的正确实现。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|CanNmTransmitCalloutFunc|
|描述|If the CanNmTransmitCalloutFunc parameter exist the CanNm module shall call the configured callback function. (It is not needed to specify a service port to the CanNm service component.)|
|描述|概述：CanNmTransmitCalloutFunc是一个回调函数，由网络管理模块调用，用于处理CAN网络管理消息的发送请求。|
|描述|注意：确保该回调函数的实现符合CAN网络管理的要求；在实现时考虑消息发送的优先级和时序；该配置项在AUTOSAR CP 4.4中应当与网络管理策略和配置一致，避免与其他网络管理回调函数冲突。|
|说明|If the CanNmTransmitCalloutFunc parameter does not exist the CanNm module shall use a none mode.|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmPnResetTime|
|描述|Specifies the runtime of the reset timer in seconds. This reset time is valid for the reset of PN requests in the EIRA and in the ERA. The value shall be the same for every channel. Thus it is a global config parameter.|
|描述|概述：CanNmPnResetTime是用于定义在局部网络管理（Partial Networking）场景下，CAN网络管理模块在检测到网络请求后，等待重新激活局部网络功能的时间。|
|描述|注意：该参数的设置应考虑网络唤醒和休眠策略，以确保不会过早地重置局部网络功能；在配置时应参照具体的车辆网络需求和ECU性能，以确保系统的稳定性和响应性；在AUTOSAR CP 4.4标准中，该参数的单位和取值范围应符合规范要求，否则可能会导致不兼容或功能异常。|
|多实例个数|0 - 1|
|取值范围|0.001 - 65.535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmPnEiraRxNSduRef|
|描述|Reference to a Pdu in the COM-Stack.|
|描述|概述：CanNmPnEiraRxNSduRef是一个配置项，用于表示在CAN网络管理的局部网络功能中，接收全网请求的网络服务数据单元的索引。它是一个指向包含接收到的EIRA请求的网络服务数据单元的索引。|
|描述|注意：在配置CanNm模块时，必须确保CanNmPnEiraRxNSduRef正确映射到相应的索引；在配置过程中，应避免句柄重复或不一致，以免导致通信问题。|
|说明|Only one SduRef is required for CanNm because the EIRA is the aggregation over all Can Channels.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.1. CanNmChannelConfig

|容器属性|值（容器）|
|---|---|
|名称|CanNmChannelConfig|
|描述|This container contains the channel specific configuration parameter of the CanNm.|
|描述|概述：CanNmChannelConfig是用于配置CAN网络管理（CAN NM）通道特定参数的配置项，它包含了控制CAN网络行为的多个属性，如消息发送周期、超时时间等。|
|描述|注意：在配置CanNmChannelConfig时，需要确保参数值符合CAN网络的实际需求和规范要求；此外，参数设置应考虑到网络的带宽和节点的处理能力，以避免网络拥塞或节点过载；最后，应当检查配置的一致性，确保与AUTOSAR CP 4.4标准相匹配，避免不兼容的情况发生。|
|多实例个数|1 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmActiveWakeupBitEnabled|
|描述|Enables/Disables the handling of the Active Wakeup Bit in the CanNm module.|
|描述|概述：CanNmActiveWakeupBitEnabled是一个配置项，用于启用或禁用在CAN网络管理消息中使用主动唤醒位的功能，这有助于节点在网络上表明其活跃状态。|
|描述|注意：在使用此配置项时，需要确保网络管理需求是否需要节点通过主动唤醒位来表明其活跃状态；此配置项的使用可能会受到具体车辆网络拓扑和协议规范的限制；在配置时应参照具体的CAN网络管理协议标准，确保与整个系统的网络管理策略一致。|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmAllNmMessagesKeepAwake|
|描述|Specifies if CanNm drops irrelevant NM PDUs.|
|描述|概述：CanNmAllNmMessagesKeepAwake配置项用于定义在CAN网络管理中，是否所有的网络管理消息都能阻止ECU进入睡眠状态。|
|描述|注意：在配置此项时，需要确保它与ECU的睡眠策略和网络管理需求相匹配；如果设置为true，任何网络管理消息都将阻止ECU进入睡眠，这可能会影响车辆的能耗管理；在实际应用中，应仔细评估是否需要所有NM消息都保持唤醒状态，以避免不必要的能源消耗。|
|说明|false: Only NM PDUs with a PNI bit = true and containing a PN request for this ECU triggers the standard RX indication handling true: Every NM PDU triggers the standard RX indication handling|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmBusLoadReductionActive|
|描述|This parameter defines if bus load reduction for the respective NM channel is active or not.|
|描述|概述：CanNmBusLoadReductionActive是一个配置项，用于启用或禁用CAN网络管理（CAN NM）中的总线负载减少功能，以降低网络上的通信负载。|
|描述|注意：在配置此项时，需要确保网络的通信需求与负载减少策略相匹配；此功能可能会影响网络上的消息传输时效性；在启用此功能时，应详细测试以确保网络性能不会受到不利影响。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmCarWakeUpFilterEnabled|
|描述|If CWU filtering is supported, only the CWU bit within the NM PDU with source node identifier CanNmCarWakeUpFilterNodeId is considered as CWU request.|
|描述|概述：CanNmCarWakeUpFilterEnabled配置项用于启用或禁用车辆唤醒过滤功能，该功能决定了网络管理是否响应来自CAN网络的唤醒信号。|
|描述|注意：在使用此配置项时，确保与车辆的具体唤醒需求和策略相匹配；不正确的配置可能导致车辆在不应该唤醒的时候唤醒，或者在需要唤醒时无法正确响应；此配置项在AUTOSAR CP 4.4中应正确设置以保证网络管理的正确性和车辆的能效。|
|说明|FALSE - CWU filtering is not supported TRUE - CWU filtering is supported|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmCarWakeUpRxEnabled|
|描述|Enables or disables support of CarWakeUp bit evaluation in received NM PDUs.|
|描述|概述：CanNmCarWakeUpRxEnabled用于配置是否启用车辆网络管理（CAN NM）接收唤醒消息的功能，以便在接收到特定的CAN消息时唤醒网络或ECU。|
|描述|注意：在设计低功耗或休眠模式的网络管理策略时，此配置项非常关键；确保此功能与车辆的整体唤醒策略一致；在AUTOSAR CP 4.4标准中，此配置项应正确集成在Nm模块中，遵循标准的配置和实现指南。|
|说明|FALSE - CarWakeUp not supported TRUE - CarWakeUp supported|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmNodeDetectionEnabled|
|描述|Precompile time switch to enable the node detection feature.|
|描述|概述：CanNmNodeDetectionEnabled是一个布尔配置参数，用于启用或禁用CAN网络管理（CAN NM）中的节点检测功能，该功能允许节点检测网络中其他节点的存在或丢失。|
|描述|注意：在配置此参数时，需要确保它与网络管理策略和系统需求相匹配；如果启用节点检测，应考虑其对网络带宽和系统资源的影响；在不需要节点检测功能的情况下应禁用此功能，以优化性能和减少不必要的网络流量。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmNodeIdEnabled|
|描述|Pre-processor switch for enabling the source node identifier.|
|描述|概述：CanNmNodeIdEnabled用于启用或禁用CAN网络管理中的节点标识符功能，这决定了节点是否在网络管理消息中发送其节点ID。|
|描述|注意：在配置时需确保与网络的设计和安全要求相符合；不正确的配置可能导致网络管理的功能不正常或节点间的通信故障；AUTOSAR CP 4.4 标准支持此配置项，无特殊兼容性问题。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPnEnabled|
|描述|Enables or disables support of partial networking.|
|描述|概述：CanNmPnEnabled是一个配置项，用于启用或禁用局部网络管理（Partial Networking）功能，这是CAN网络管理模块的一个特性，允许节点仅在需要时激活，以减少网络上的通信和能耗。|
|描述|注意：在配置CanNmPnEnabled时，需要确保车辆网络的其他节点也支持局部网络功能；此外，该功能的使用必须符合ISO 11898-6标准；在实施时还需考虑与诊断通信的兼容性。|
|说明|false: Partial networking Range not supported true: Partial networking supported|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPnEraCalcEnabled|
|描述|Specifies if CanNm calculates the PN request information for external requests. (ERA)|
|描述|概述：CanNmPnEraCalcEnabled是一个配置项，用于启用或禁用局部网络管理（Partial Networking）的扩展路由请求属性（Era）计算功能。|
|描述|注意：在使用局部网络功能时，确保此配置与网络管理需求一致；如果不使用局部网络功能，则不应启用此选项；在配置时，应考虑网络拓扑和相关节点的支持能力。|
|说明|false: PN request are not calculated true: PN request are calculated|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmPnHandleMultipleNetworkRequests|
|描述|Specifies if CanNm performs an additional transition from Network Mode to Repeat Message State (true) or not (false).|
|描述|概述：CanNmPnHandleMultipleNetworkRequests配置项用于定义CAN网络管理是否能够处理来自不同网络请求的多个唤醒原因，确保网络管理能够在接收到多个网络请求时正确响应。|
|描述|注意：在使用部分唤醒功能时，需要确保该配置项被正确设置以支持多个网络请求；如果网络仅需响应单一唤醒源，可能不需要启用此功能；AUTOSAR CP 4.4标准中对于处理多个网络请求的具体实现细节可能有所不同，需要参考具体的网络管理模块实现。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmFirstPduFailedRetry|
|描述|Specifies of CanNm retry first NM Message request.|
|描述|概述：CanNmRetryFirstMessageRequest是一个配置项，用于定义在CAN网络管理中，当首次发送消息请求失败后，是否应该重试发送该消息。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项的使用应当符合网络管理的策略和时间要求；重试机制可能会影响网络的带宽和性能，因此需要谨慎配置；确保重试策略与其他网络参与者的行为兼容，避免潜在的冲突。|
|多实例个数|0 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|CanNmRepeatMsgIndEnabled|
|描述|Enable/disable the notification that a RepeatMessageRequest bit has been received.|
|描述|概述：CanNmRepeatMsgIndEnabled配置项用于启用或禁用CAN网络管理中重复消息指示的功能，这允许节点在接收到重复的网络管理消息时采取特定行动。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项的使用应根据项目的具体需求来决定；如果启用，需要确保网络管理的实现能正确处理重复消息的情况；不正确的配置可能会影响网络的稳定性和性能。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanNmPduCbvPosition|
|描述|Defines the position of the control bit vector within the NM PDU.|
|描述|概述：CanNmPduCbvPosition配置项用于定义控制位矢量（Control Bit Vector, CBV）在网络管理PDU（Protocol Data Unit）中的位置，这对于正确解析和构建NM消息至关重要。|
|描述|注意：在配置CanNmPduCbvPosition时，需要确保其值与实际CAN帧中CBV的位置相匹配；此外，该配置应与网络上其他节点的配置保持一致，以确保网络管理通信的互操作性；最后，如果使用的是某种特定的CAN网络管理协议，如ISO或者OSEK NM，应参考该协议规定的CBV位置。|
|说明|The value of the parameter represents the location of the Control Bit Vector in the NM PDU (CanNmPduByte0 means byte 0, CanNmPduByte1 means byte 1, CanNmPduOff means source node identifier is not part of the NM PDU) ImplementationType: CanNm_PduPositionType|
|多实例个数|1 - 1|
|默认值|CANNM_PDU_BYTE_1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|CanNmPduNidPosition|
|描述|Defines the position of the source node identifier within the NM PDU.|
|描述|概述：CanNmPduNidPosition 定义了在 CAN NM PDU (Protocol Data Unit) 中节点标识符（Node Identifier, NID）的位置。|
|描述|注意：在配置CanNmPduNidPosition时，必须确保其位置不会与PDU中其他重要数据字段冲突；此配置项应符合网络管理需求，确保正确的网络节点识别；在不同的CAN网络配置中，NID位置可能需要调整以适应特定的网络协议要求。|
|说明|The value of the parameter represents the location of the source node identifier in the NM PDU (CANNM_PDU_BYTE_0 means byte 0, CANNM_PDU_BYTE_1 means byte 1, CANNM_PDU_OFF means source node identifier is not part of the NM PDU) ImplementationType: CanNm_PduPositionType|
|多实例个数|1 - 1|
|默认值|CANNM_PDU_BYTE_0|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmImmediateNmCycleTime|
|描述|Defines the immediate NM PDU cycle time in seconds which is used for CanNmImmediateNmTransmissions NM PDU transmissions.|
|描述|概述：CanNmImmediateNmCycleTime定义了在CAN网络管理中，立即网络管理周期的时间间隔，用于控制在特定条件下发送即时NM消息的频率。|
|描述|注意：该时间值应小于或等于CanNmMainFunctionPeriod，以确保即时NM消息能够按预期频率发送；配置值应考虑网络负载和性能要求，避免对网络造成过大压力；在AUTOSAR CP 4.4标准中，该配置项的单位通常是毫秒（ms），确保单位的一致性。|
|多实例个数|0 - 1|
|默认值|0.02|
|取值范围|0.001 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmMsgCycleOffset|
|描述|Time offset in the periodic transmission node. It determines the start delay of the transmission. Specified in seconds.|
|描述|概述：CanNmMsgCycleOffset是用于定义CAN网络管理消息发送的相对偏移时间，它指定了周期性消息发送的起始时间点，以确保消息在预定的时间窗口内发送。|
|描述|注意：该值应小于CanNmMsgCycleTime以避免时间窗口溢出；在配置时需要考虑网络上其他节点的消息发送时间，以减少冲突和网络拥塞；在多节点系统中，应确保每个节点的CanNmMsgCycleOffset有所区分，以优化网络带宽利用率。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmMsgCycleTime|
|描述|Period of a NM PDU in seconds. It determines the periodic rate in the "periodic transmission mode with bus load reduction" and is the basis for transmit scheduling in the "periodic transmission mode without bus load reduction".|
|描述|概述：CanNmMsgCycleTime定义了CAN网络管理消息的发送周期，即两次相同网络管理消息之间的时间间隔。|
|描述|注意：该值需要根据网络的带宽和系统的实时性要求谨慎设置；过短的周期可能导致网络拥塞，过长的周期可能影响网络管理的效率和响应速度；在AUTOSAR CP 4.4标准中，确保该配置与网络管理需求一致。|
|多实例个数|1 - 1|
|默认值|0.5|
|取值范围|0.001 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmMsgReducedTime|
|描述|Node specific bus cycle time in the periodic transmission mode with bus load reduction. Specified in seconds.|
|描述|概述：CanNmMsgReducedTime配置项用于定义在网络管理通信中，CAN网络消息的减少时间间隔，即在特定条件下减少发送网络管理消息的频率以降低网络负载。|
|描述|注意：该配置项的值需要根据网络的实际负载和性能要求谨慎设置，以避免影响网络管理的效率和可靠性；在设置时应考虑到不同网络节点的处理能力和响应时间，确保网络稳定性；AUTOSAR CP 4.4标准中，该配置项的具体数值范围和默认值可能有所不同，需要参考具体的标准文档。|
|多实例个数|1 - 1|
|默认值|0.05|
|取值范围|0.001 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmMsgTimeoutTime|
|描述|When using Partial Network and this timeout is defined then CanNm monitors that a NM-PDU is transmitted successfully within this Transmission Timeout Time and provides an error notification otherwise.|
|描述|概述：CanNmMsgTimeoutTime定义了网络管理消息在CAN网络上的超时时间，用于监控网络管理消息的接收，确保网络的稳定性和可靠性。|
|描述|注意：该参数的设置需要根据网络的实际情况和要求进行调整，以避免过于频繁的网络管理消息导致的网络拥堵或过于宽松导致的网络不稳定；在AUTOSAR CP 4.4中，确保该配置项与网络管理需求和其他相关配置项（如CanNmTimeoutTime）协调一致；不同的网络可能需要不同的超时时间设置。|
|多实例个数|0 - 1|
|默认值|0.06|
|取值范围|0.001 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmRemoteSleepIndTime|
|描述|Timeout for Remote Sleep Indication.|
|描述|概述：CanNmRemoteSleepIndTime定义了在CAN网络管理中，从接收到最后一个NM消息到认为网络节点处于远程睡眠状态所需的时间。|
|描述|注意：该时间参数应根据网络的具体需求和节点的响应特性来配置；过短的时间可能导致误判，过长的时间可能延迟睡眠状态的识别；确保该配置与网络中其他节点的远程睡眠时间设置保持一致。|
|说明|It defines the time in seconds how long it shall take to recognize that all other nodes are ready to sleep.|
|多实例个数|0 - 1|
|默认值|0.5|
|取值范围|0.001 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmRepeatMessageTime|
|描述|Timeout for Repeat Message State.|
|描述|概述：CanNmRepeatMessageTime配置项定义了在CAN网络管理中，节点处于Repeat Message状态时发送重复消息的时间间隔。|
|描述|注意：该时间间隔必须根据网络的具体需求和性能进行配置，以确保网络的稳定性和通信效率；配置值应遵循AUTOSAR CP 4.4标准中对时间参数的规定，确保与其他节点的兼容性；过短的重复消息时间可能导致网络拥塞，过长则可能影响到网络管理的及时性。|
|说明|It defines the time in seconds how long the NM shall stay in the Repeat Message State.|
|多实例个数|1 - 1|
|默认值|1.5|
|取值范围|0 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmTimeoutTime|
|描述|Network Timeout for NM PDUs.|
|描述|概述：CanNmTimeoutTime是用于定义网络管理通信超时时间的配置项，它指定了CAN网络管理协议中等待网络管理消息的最大时间。|
|描述|注意：该值必须根据网络的具体需求和性能来配置，以确保网络稳定性；超时时间设置过短可能导致误判网络故障，过长则可能延迟故障检测；应与其他网络参与者和诊断需求保持一致。|
|说明|It denotes the time in seconds how long the NM shall stay in the Ready Sleep State before transition into the Prepare Bus-Sleep Mode is initiated.|
|多实例个数|1 - 1|
|默认值|2|
|取值范围|0.002 - 65.535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmWaitBusSleepTime|
|描述|Timeout for bus calm down phase.|
|描述|概述：CanNmWaitBusSleepTime是一个配置参数，用于定义网络管理在进入总线睡眠状态之前等待的时间，这个时间是在最后一条NM消息发送后开始计算的。|
|描述|注意：该参数的值需要根据具体的网络需求和ECU的性能来设定；过短的等待时间可能导致网络管理过早进入睡眠状态，而过长的等待时间可能会导致不必要的电源消耗；在配置此参数时，应确保它与网络上其他节点的相应参数相协调，以避免网络同步问题。|
|说明|It denotes the time in seconds how long the NM shall stay in the Prepare Bus-Sleep Mode before transition into Bus-Sleep Mode shall take place.|
|多实例个数|1 - 1|
|默认值|5|
|取值范围|0.001 - 65.535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmCarWakeUpBitPosition|
|描述|Specifies the Bit position of the CWU within the NM PDU.|
|描述|概述：CanNmCarWakeUpBitPosition配置项用于定义在CAN网络管理消息中，用于唤醒车辆的特定位的位置。|
|描述|注意：该配置项的值必须在CAN消息的有效数据长度范围内；确保不与其他网络管理或诊断功能使用的位冲突；在配置时应考虑网络上所有节点的唤醒逻辑一致性。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 7|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmCarWakeUpBytePosition|
|描述|Specifies the Byte position of the CWU within the NM PDU.|
|描述|概述：CanNmCarWakeUpBytePosition配置项用于定义网络管理中唤醒报文的字节位置，这是为了在车辆网络中检测到唤醒信号时能够正确地识别和处理。|
|描述|注意：该配置项的值必须与实际唤醒报文中唤醒字节的位置相匹配；在配置时需要确保不与其他网络管理功能的报文字段冲突；在多个ECU共用唤醒报文的情况下，需要协调一致以避免解析错误。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 7|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmCarWakeUpFilterNodeId|
|描述|Source node identifier for CWU filtering. If CWU filtering is supported, only the CWU bit within the NM PDU with source node identifier CanNmCarWakeUpFilterNodeId is considered as CWU request.|
|描述|概述：CanNmCarWakeUpFilterNodeId用于定义在车辆网络管理（CAN NM）中，哪些节点的唤醒信号会被当前节点接受和处理，以便实现网络管理策略。|
|描述|注意：该配置项应仅包括网络中负责唤醒功能的节点ID；确保配置的节点ID在网络中是存在的；在配置此项时，应考虑网络的整体唤醒策略和节点的功能角色。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmImmediateNmTransmissions|
|描述|Defines the number of immediate NM PDUs which shall be transmitted. If the value is zero no immediate NM PDUs are transmitted. The cycle time of immeditate NM PDUs is defined by CanNmImmediateNmCycleTime.|
|描述|概述：CanNmImmediateNmTransmissions配置项用于定义在网络管理中，CAN网络管理模块（CanNm）发送立即NM消息的次数，这些消息用于快速通知网络上的其他节点有关当前节点状态的变化。|
|描述|注意：该值必须根据网络的具体需求进行配置，以确保网络的稳定性和性能；过高的立即传输次数可能会导致网络拥塞；该配置项的值应当符合AUTOSAR标准中对于网络管理的规定，以保证与其他模块的兼容性。|
|多实例个数|1 - 1|
|默认值|15|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmNodeId|
|描述|Node identifier of local node.|
|描述|概述：CanNmNodeId是用于定义CAN网络管理中某个节点的唯一标识符，它指定了该节点在CAN网络中的地址。|
|描述|注意：NodeId的值必须在网络中唯一，以避免地址冲突；在配置时需确保符合CAN网络的地址分配规则；在AUTOSAR CP 4.4中，确保该配置与网络设计文档保持一致，避免配置错误导致网络通信失败。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmComMNetworkHandleRef|
|描述|This reference points to the unique channel defined by the ComMChannel and provides access to the unique channel index value in ComMChannelId.|
|描述|概述：CanNmComMNetworkHandleRef配置项用于定义CAN网络管理模块（CanNm）与通信管理器（ComM）之间的网络句柄引用，确保正确的网络层次关系和通信控制。|
|描述|注意：在配置CanNm模块时，必须确保CanNmComMNetworkHandleRef正确映射到相应的ComM网络句柄；此引用是实现CanNm与ComM之间通信的关键；在配置过程中，应避免句柄重复或不一致，以免导致通信问题。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmPnEraRxNSduRef|
|描述|Reference to a Pdu in the COM-Stack. The SduRef is required for every CanNm Channel, because ERA is reported per channel.|
|描述|概述：CanNmPnEraRxNSduRef是一个配置项，用于引用接收网络管理部分唤醒消息的PDU（协议数据单元），这在使用部分网络功能时是必要的。|
|描述|注意：在配置CanNmPnEraRxNSduRef时，需要确保引用的PDU与实际接收的唤醒消息相匹配；此配置项仅在启用了部分网络功能时适用；在配置过程中，应注意与其他网络管理配置的一致性和兼容性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.1.1. CanNmRxPdu

|容器属性|值（容器）|
|---|---|
|名称|CanNmRxPdu|
|描述|This container is used to configure the Rx PDU properties that are used for the CanNm Channel.|
|描述|概述：CanNmRxPdu配置项定义了网络管理接收PDU（协议数据单元）的属性，这些属性包括PDU的标识符、数据长度和与之关联的CAN网络通道。|
|描述|注意：在配置CanNmRxPdu时，必须确保PDU标识符的唯一性，以避免在同一CAN网络上的冲突；数据长度应与实际CAN帧的DLC匹配，以确保正确的数据解析；还需确保正确的关联到相应的CAN网络通道，以实现正确的网络管理功能。|
|多实例个数|1 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmRxPduId|
|描述|This parameter defines the Rx PDU ID of the CanIf L-PDU range that is associated with this CanNm channel.|
|描述|概述：CanNmRxPduId是一个配置项，用于标识网络管理接收的CAN网络管理PDU（协议数据单元）的唯一标识符。|
|描述|注意：该标识符必须是系统内唯一的，以确保正确识别接收到的网络管理消息；在配置时应确保与CAN驱动和CAN接口模块中定义的PDU ID相匹配；在整个系统中，不同的网络管理通道应该有不同的CanNmRxPduId配置，以避免通道间的冲突。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmRxPduRef|
|描述|Reference to the global PDU that is used by this CanNm channel.|
|描述|概述：CanNmRxPduRef是一个配置项，用于引用接收到的CAN网络管理PDU（协议数据单元），它将接收到的PDU与网络管理功能相关联。|
|描述|注意：在配置CanNmRxPduRef时，需要确保引用的PDU与CAN网络管理的要求相匹配；此配置项通常与CAN网络管理的PDU ID一致；在配置过程中，应注意PDU的唯一性和正确性，避免与其他网络管理或通信功能的PDU发生冲突。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.1.2. CanNmTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CanNmTxPdu|
|描述|This container contains the CanNmTxConfirmationPduId and the CanNmTxPduRef.|
|描述|概述：CanNmTxPdu是用于定义网络管理传输协议数据单元（PDU）的配置，这些PDU用于CAN网络管理通信。|
|描述|注意：确保CanNmTxPdu的ID与网络上其他PDU的ID不冲突；配置的PDU大小应符合网络的数据传输要求；在配置时需遵循CAN网络的标准和限制。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmTxConfirmationPduId|
|描述|Handle Id to be used by the Lower Layer to confirm the transmission of the CanNmTxPdu to the LowerLayer.|
|描述|概述：CanNmTxConfirmationPduId用于标识网络管理发送确认的PDU（协议数据单元）ID，这是在CAN网络管理中用于确认数据发送状态的重要参数。|
|描述|注意：确保此PDU ID与网络上其他PDU ID不冲突；此ID应配置为有效的CAN ID，且符合网络的数据传输规范；在AUTOSAR CP 4.4中，此配置项应正确映射以确保网络管理功能的正确实现。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmTxPduRef|
|描述|The reference to the common PDU structure.|
|描述|概述：CanNmTxPduRef是一个配置参数，用于引用网络管理模块发送的CAN网络管理PDU（协议数据单元）。|
|描述|注意：在配置CanNm模块时，必须确保CanNmTxPduRef正确引用了对应的PDU；此PDU应该在PDU Router配置中定义；确保PDU的属性与网络管理的要求一致，例如PDU类型和长度。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

#### 1.1.3. CanNmUserDataTxPdu

|容器属性|值（容器）|
|---|---|
|名称|CanNmUserDataTxPdu|
|描述|This optional container is used to configure the UserNm PDU. This container is only available if CanNmComUserDataSupport is enabled.|
|描述|概述：CanNmUserDataTxPdu是用于定义CAN网络管理中传输用户数据的PDU（协议数据单元）的标识符。|
|描述|注意：确保该PDU的标识符在整个网络中是唯一的；该配置项应与网络管理需求严格对应，避免数据传输错误；在配置时需考虑数据的安全性和实时性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmTxUserDataPduId|
|描述|This parameter defines the Handle ID of the NM User Data I-PDU.|
|描述|概述：CanNmTxUserDataPduId是用于标识网络管理传输用户数据的PDU（协议数据单元）标识符。|
|描述|注意：确保此PDU ID在系统中是唯一的，以避免数据传输冲突；PDU ID应与CAN网络的配置相匹配，保证正确的数据传输和接收；在AUTOSAR CP 4.4中，此配置项应正确集成在Nm模块中，确保网络管理功能的正确实现。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|CanNmTxUserDataPduRef|
|描述|Reference to the NM User Data I-PDU in the global PDU collection.|
|描述|概述：CanNmTxUserDataPduRef是一个配置项，用于引用网络管理模块（Network Management, NM）发送用户数据所使用的PDU（协议数据单元）。|
|描述|注意：在配置CanNm模块时，必须确保引用的PDU与实际的CAN网络上的用户数据PDU相匹配；如果PDU配置错误，可能会导致网络管理通信失败；AUTOSAR CP 4.4标准中，该配置项应正确地映射到相应的Com层配置，以确保数据的正确发送。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.2. CanNmPnInfo

|容器属性|值（容器）|
|---|---|
|名称|CanNmPnInfo|
|描述|PN information configuration|
|描述|概述：CanNmPnInfo是一个配置项，用于定义CAN网络管理（CAN NM）中的部分网络请求和释放信息，这些信息与车辆网络中的偏好节点（Partial Networking, PN）功能相关。|
|描述|注意：在配置CanNmPnInfo时，需要确保其与车辆中实际使用的偏好节点功能相匹配；此外，该配置项的属性应符合AUTOSAR CP 4.4标准中对CAN NM的规定；在多节点网络中，还需考虑不同节点间的PN信息一致性和兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmPnInfoLength|
|描述|Specifies the length of the PN request information in the NM PDU.|
|描述|概述：CanNmPnInfoLength配置项定义了部分网络管理信息（Partial Networking）的长度，即在CAN网络管理消息中，用于识别节点是否需要唤醒的数据长度。|
|描述|注意：该配置项的值必须与实际网络设计中定义的部分网络唤醒标识符长度一致；在配置时需要确保与相关的CanNmPnFilterMask配置项相匹配；超出AUTOSAR CP 4.4标准定义的长度范围可能导致不兼容或功能异常。|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|1 - 7|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmPnInfoOffset|
|描述|Specifies the offset of the PN request information in the NM PDU.|
|描述|概述：CanNmPnInfoOffset 定义了在CAN帧中，局部网络管理信息（Partial Networking）的起始字节偏移量。|
|描述|注意：确保偏移量设置不会与其他数据域冲突；在配置时需考虑CAN帧的总大小，避免超出帧边界；该配置项必须与车辆网络的实际需求和规范一致。|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|1 - 7|

#### 1.2.1. CanNmPnFilterMaskByte

|容器属性|值（容器）|
|---|---|
|名称|CanNmPnFilterMaskByte|
|描述|PN information configuration|
|描述|概述：CanNmPnFilterMaskByte配置项用于定义CAN网络管理的局部网络请求过滤掩码，它决定了哪些位在PN消息中被考虑用于唤醒网络的决策。|
|描述|注意：在配置CanNmPnFilterMaskByte时，需要确保掩码与实际的局部网络请求匹配；掩码的设置应遵循网络设计和诊断需求；不正确的掩码设置可能导致网络唤醒行为不符合预期。|
|多实例个数|0 - 7|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmPnFilterMaskByteIndex|
|描述|Index of the filter mask byte. Specifies the position within the filter mask byte array.|
|描述|概述：CanNmPnFilterMaskByteIndex用于定义在 CAN 网络管理的局部网络请求中，过滤掩码字节的索引位置。|
|描述|注意：该配置项的索引应正确对应于CAN帧中的特定字节位置；索引值应在有效范围内，避免超出数据帧的字节大小；确保配置与网络的实际需求和规范一致。|
|多实例个数|1 - 1|
|取值范围|0 - 6|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CanNmPnFilterMaskByteValue|
|描述|Parameter to configure the filter mask byte.|
|描述|概述：CanNmPnFilterMaskByteValue用于定义在局部网络管理（Partial Networking）中，CAN网络消息标识符过滤器的字节掩码值，以便过滤和识别特定的网络管理消息。|
|描述|注意：该配置项的值必须与网络上的其他节点协调一致，以确保网络管理消息的正确识别和处理；在配置时需考虑网络的实际需求，避免过滤掉必要的通信；该配置项在AUTOSAR CP 4.4中应确保与PDU的配置相匹配，以保证正确的消息处理。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

### 1.3. CanNmMainFunction

|容器属性|值（容器）|
|---|---|
|名称|CanNmMainFunction|
|描述|Contains the configuration parameters of the AUTOSAR CanNm module's CanNmMainFunction.|
|描述|概述：CanNmMainFunction是一个配置项，用于定义CAN网络管理（CAN NM）中的主函数，这些主函数用于taskmapping。|
|描述|注意：在配置CanNmMainFunction时，需要确保其与taskmapping功能相匹配；此外，该配置项的属性应符合AUTOSAR CP 4.4标准中对CAN NM的规定。|
|多实例个数|0 - 255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|CanNmMainFunctionPeriod|
|描述|Call cycle in seconds of CanNm_MainFunction.|
|描述|概述：CanNmMainFunctionPeriod配置项指定了CAN网络管理主函数（CanNm_MainFunction）的调用周期，这个周期决定了CAN网络管理功能的执行频率。|
|描述|注意：该值必须与系统定时器和OS任务调度配置相匹配，以确保准确的时间行为；过小的周期可能导致系统过载，而过大的周期可能导致网络管理响应不及时；在配置时需要考虑到ECU的性能和网络的实时性要求。|
|多实例个数|0 - 1|
|默认值|0.005|
|取值范围|0 - 65.535|
