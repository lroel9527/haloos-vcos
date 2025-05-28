# EcuC 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|EcuC|
|描述|Virtual module to collect ECU Configuration specific / global configuration information.|
|描述|概述：EcuC是AUTOSAR中的一个模块，用于配置ECU的硬件和软件资源，确保各模块之间的配置一致性和集成性。它通过定义各模块的参数和依赖关系来支持ECU的整体配置管理。|
|描述|注意：EcuC配置项必须与具体的ECU硬件和软件架构相匹配；确保所有模块的配置参数正确且一致，以避免集成问题；在配置过程中应遵循AUTOSAR标准，以确保兼容性和可移植性。|
|多实例个数|0 - 1|

## 1. EcucConfigSet

|容器属性|值（容器）|
|---|---|
|名称|EcucConfigSet|
|描述|This container contains the configuration parameters and sub containers of the global PduCollection.|
|描述|概述：EcucConfigSet是AUTOSAR中用于定义ECU配置的集合，包含多个容器和参数，用于描述ECU的具体配置细节。它是ECU配置描述文件的核心部分，确保ECU的配置数据结构化和一致性。|
|描述|注意：EcucConfigSet是一个ECU配置集；需确保其包含所有必要的配置参数，以满足系统需求；在配置工具中正确设置以避免配置不一致或缺失。|
|多实例个数|0 - 1|

### 1.1. EcucPduCollection

|容器属性|值（容器）|
|---|---|
|名称|EcucPduCollection|
|描述|Collection of all Pdu objects flowing through the Com-Stack.|
|描述|概述：EcucPduCollection用于定义一组PDU（Protocol Data Unit），这些PDU可以在不同的通信模块之间传输，以实现数据的交换和管理。它帮助组织和管理PDU的传输和接收过程，以确保通信的有效性和可靠性。|
|描述|注意：确保EcucPduCollection中的每个PDU具有唯一标识，以避免数据冲突；正确配置PDU的传输属性以满足系统的通信需求；注意与其他通信模块的兼容性和集成性，以确保系统的整体功能和性能。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|PduIdTypeEnum|
|描述|The PduIdType is used within the entire AUTOSAR Com Stack except for bus drivers. The size of this global type depends on the maximum number of PDUs used within one software module. If no software module deals with more PDUs that 256, this type can be set to uint8. If at least one software module handles more than 256 PDUs, this type must be set to uint16. See AUTOSAR_SWS_CommunicationStackTypes for more details.|
|描述|概述：PduIdTypeEnum用于定义PDU（Protocol Data Unit）标识符的数据类型。|
|描述|注意：选择合适的标识符类型以满足系统性能和内存使用要求；在配置时注意与其他通信参数的一致性和兼容性。|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|PduLengthTypeEnum|
|描述|The PduLengthType is used within the entire AUTOSAR Com Stack except for bus drivers. The size of this global type depends on the maximum length of PDUs to be sent by an ECU. If no segmentation is used the length depends on the maximum payload size of a frame of the underlying communication system (for FlexRay maximum size is 255 bytes, therefore uint8). If segmentation is used it depends on the maximum length of a segmented N-SDU (in general uint16 is used). See AUTOSAR_SWS_CommunicationStackTypes for more details.|
|描述|概述：PduLengthTypeEnum用于定义PDU（Protocol Data Unit）长度的数据类型，确保在通信中正确处理和传输数据长度信息。|
|多实例个数|1 - 1|

#### 1.1.1. MetaDataType

|容器属性|值（容器）|
|---|---|
|名称|MetaDataType|
|描述|Meta data serves to transport information through the AUTOSAR layers. It is transported by the PduInfoType structure via a separate pointer to a byte array alongside the length of and a pointer to the payload of the PDU. This container defines the content of the meta data.|
|描述|概述：MetaDataType用于定义数据元素的元数据类型，描述数据的属性和结构信息，以支持数据的正确处理和交换。|
|描述|注意：确保MetaDataType与实际数据类型一致，以避免数据处理错误；合理定义元数据以支持数据的可扩展性和兼容性；在跨系统数据交换时注意元数据的一致性和标准化。|
|多实例个数|0 - inf|

##### 1.1.1.1. MetaDataItem

|容器属性|值（容器）|
|---|---|
|名称|MetaDataItem|
|描述|The content of meta data in a Pdu consists of an ordered list of meta data items.|
|描述|概述：MetaDataItem用于在AUTOSAR模型中存储附加的、非标准化的信息，这些信息可以是关于模型元素的注释、标签或其他元数据，以支持工具链的特定需求。|
|描述|注意：MetaDataItem的使用应遵循工具供应商的指导，以确保兼容性；避免在MetaDataItem中存储关键的系统配置数据；确保MetaDataItem的内容不会影响AUTOSAR模型的标准化部分。|
|说明|这个容器（Container）表示一个元数据项，包含在PDU的元数据集合中。|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|MetaDataItemType|
|描述|This parameter defines the type of a meta data item.|
|描述|概述：MetaDataItemType用于定义与AUTOSAR模型中的元素相关的元数据类型，帮助在模型中附加额外的信息以支持工具链的处理和扩展功能。|
|描述|注意：确保MetaDataItemType的定义符合AUTOSAR标准的命名和类型约定；在使用工具链时，确保工具对自定义的MetaDataItemType具有兼容性。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|MetaDataItemLength|
|描述|This parameter defines the length of a meta data item in bytes.|
|描述|概述：MetaDataItemLength用于定义在AUTOSAR系统中元数据项的长度，确保元数据在系统中被正确解析和处理。|
|描述|注意：MetaDataItemLength的值应与实际元数据项的长度一致，以避免数据截断或溢出；配置时需考虑系统的内存限制和性能要求；确保与其他相关配置项的兼容性以维持系统的稳定性。|
|多实例个数|1 - 1|
|取值范围|1 - 64|

#### 1.1.2. Pdu

|容器属性|值（容器）|
|---|---|
|名称|Pdu|
|描述|One Pdu flowing through the COM-Stack.|
|描述|概述：Pdu（Protocol Data Unit）是AUTOSAR中用于描述通信数据的基本单位，定义了数据的结构和传输属性，以支持不同协议数据在通信栈模块之间的数据交换。|
|说明|该PDU被所有通信栈模块共同使用，以确保它们引用的是同一个PDU。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DynamicLength|
|描述|This parameter defines whether the Pdu has dynamic length (true) or not (false). Please note that the usage of this attribute is restricted by [constr_3448].|
|描述|概述：DynamicLength用于定义某个数据元素或信号的动态长度属性，通常用于处理变长数据以适应不同的应用需求。它允许在运行时根据实际需要调整数据的长度，从而提高系统的灵活性和资源利用效率。|
|描述|注意：确保动态长度的配置与系统的内存管理策略兼容，避免内存泄漏或溢出；在设计时考虑数据长度变化对系统性能的影响；在多节点通信中，确保发送和接收双方对动态长度的处理一致。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|J1939Requestable|
|描述|Pdu can be triggered by the J1939 request message.|
|描述|概述：J1939Requestable配置项用于定义某个ECU是否可以请求J1939网络上的特定参数组（PGN），以便从其他节点获取所需数据，从而实现节点间的数据交换和通信。|
|描述|注意：确保配置的PGN在网络中是可请求的，以避免通信失败；配置时需遵循J1939协议的规定，确保请求的合法性和有效性；注意网络负载，避免频繁请求导致的网络拥堵。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|PduLength|
|描述|Length of the Pdu in bytes. It should be noted that in former AUTOSAR releases (Rel 2.1, Rel 3.0, Rel 3.1, Rel 4.0 Rev. 1) this parameter was defined in bits.|
|描述|概述：PduLength用于定义协议数据单元（PDU）的长度，以字节为单位，确保数据传输的完整性和有效性。它是通信协议中重要的参数，影响数据打包和解包的过程。|
|描述|注意：PduLength的值必须在协议规定的最小和最大长度范围内；配置时需考虑网络带宽和性能要求；确保发送端和接收端的PduLength配置一致以避免数据传输错误。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|SysTPduToFrameTriggeringRef|
|描述|Reference to the FrameTriggering from the SystemTemplate which this Pdu belongs to.|
|描述|概述：SysTPduToFrameTriggeringRef用于在系统中定义PDU（协议数据单元）与帧触发机制之间的映射关系，确保数据在通信总线上传输时能够正确地被触发和识别。|
|说明|SysTPduToFrameTriggeringRef适用于不经过Pdu Router（PDU路由器）的PDU，如UserDefinedPdus（用户自定义PDU）、NmPdus（网络管理PDU）和 NPdus（网络协议PDU）。若已存在SysTPduToPduTriggeringRef，则不得使用此引用。|
|多实例个数|0 - 1|
|目标类型|FRAME-TRIGGERING|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|SysTPduToPduTriggeringRef|
|描述|Reference to the PduTriggering from the SystemTemplate which this Pdu represents.|
|描述|概述：SysTPduToPduTriggeringRef用于定义系统传输协议数据单元（SysTPdu）与PDU触发机制之间的引用关系，确保数据单元在正确的触发条件下被发送或接收。|
|说明|SysTPduToPduTriggeringRef适用经过PDU Router的PDU。但是不适用于UserDefinedPdus（用户自定义PDU）、NmPdus（网络管理PDU）和 NPdus（网络协议PDU）等这些不经过PDU Router的PDU；对于这些PDU，应使用 SysTPduToFrameTriggeringRef。|
|多实例个数|0 - 1|
|目标类型|PDU-TRIGGERING|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|MetaDataTypeRef|
|描述|Reference to meta data that is transported in the Pdu through the AUTOSAR layers.|
|描述|概述：MetaDataTypeRef用于引用特定的元数据类型，确保在配置中使用一致的元数据定义，以支持数据的类型安全和一致性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/MetaDataType|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcucPduDefaultCoreRef|
|描述|Reference to EcucCoreDefinition, where the according Pdu is assigned to.|
|描述|概述：EcucPduDefaultCoreRef用于指定默认的处理核心（Core），以便在多核环境中处理特定的PDU（Protocol Data Unit），确保数据在正确的核心上进行处理和传输。|
|描述|注意：确保指定的核心在系统配置中有效且可用；在多核系统中，合理分配PDU到不同核心以优化性能；避免频繁的核间通信。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucHardware/EcucCoreDefinition|

## 2. EcucHardware

|容器属性|值（容器）|
|---|---|
|名称|EcucHardware|
|描述|Hardware definition of this Ecu.|
|描述|概述：EcucHardware用于描述ECU（电子控制单元）中硬件相关的配置参数，定义了硬件资源的使用和分配，以确保软件组件能够正确地与硬件交互。|
|描述|注意：确保硬件配置与实际物理硬件一致，避免配置错误导致系统故障；在进行硬件配置时，需考虑系统的性能和资源限制；在多供应商环境中，确保硬件配置的兼容性和一致性。|
|多实例个数|0 - 1|

### 2.1. EcucCoreDefinition

|容器属性|值（容器）|
|---|---|
|名称|EcucCoreDefinition|
|描述|Definition of one Core on this Ecu.|
|描述|概述：EcucCoreDefinition用于定义ECU的核心配置，包括核心的数量、类型以及与之相关的资源分配等信息，以支持ECU的多核架构和优化资源使用。|
|描述|注意：确保核心定义与实际硬件架构一致，避免资源分配错误；核间通信和同步机制需根据核心定义进行合理设计；在多核系统中，注意核间任务调度和负载均衡。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|EcucCoreId|
|描述|ID of the core.|
|描述|概述：EcucCoreId用于标识ECU配置中某个特定核心的唯一标识符，以便在多核系统中进行正确的配置和资源分配。|
|描述|注意：确保每个核心的EcucCoreId在整个ECU配置中是唯一的，以避免资源冲突；在多核环境下，合理分配资源和任务以优化性能；配置时需与硬件架构保持一致，避免不必要的复杂性。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|EcucCoreHwRef|
|描述|Optional reference to the HwElement of HwCategory ProcessingUnit that represents this Core in the ECU Resource Template.|
|描述|概述：EcucCoreHwRef用于指定ECU配置中某个核心（Core）所关联的硬件引用，确保软件配置与硬件架构的一致性和兼容性。该配置项在多核系统中尤为重要，以正确映射每个核心到其对应的硬件资源。|
|描述|注意：确保EcucCoreHwRef与实际硬件配置一致，避免因配置错误导致系统不稳定；在多核环境中，仔细核对每个核心的硬件引用，防止资源冲突；定期更新配置以适应硬件变更或升级。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsPublishedInformation/OsDerivativeInformation/OsPhysicalCore|

## 3. EcucPartitionCollection

|容器属性|值（容器）|
|---|---|
|名称|EcucPartitionCollection|
|描述|Collection of Partitions defined for this ECU.|
|描述|概述：EcucPartitionCollection用于定义一组EcucPartition，这些分区用于将ECU配置划分为多个逻辑部分，以便于管理和隔离。它帮助组织和管理复杂的ECU配置，确保各个分区之间的独立性和模块化。|
|描述|注意：确保每个EcucPartition在集合中具有唯一标识，以避免冲突；合理划分分区以优化资源利用和系统性能；在进行分区配置时，注意各分区之间的依赖关系和交互，以确保系统的整体一致性和功能正确性。|
|多实例个数|0 - 1|

### 3.1. EcucPartition

|容器属性|值（容器）|
|---|---|
|名称|EcucPartition|
|描述|Definition of one Partition on this ECU.|
|描述|概述：EcucPartition用于定义AUTOSAR系统中软件组件的隔离单元，确保不同组件在运行时的内存和资源隔离，以提高系统的安全性和稳定性。通过配置EcucPartition，可以实现对软件组件的分区管理和资源分配。|
|描述|注意：EcucPartition的配置需要与系统的安全和资源管理策略一致；确保每个分区的资源分配合理，避免资源冲突；在多核系统中，需特别注意跨核分区的资源隔离和通信机制。|
|说明|一个Partition只能被一个Os-Application引用.|
|多实例个数|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|ASIL|
|描述|This parameter defines the ASIL of a meta data item.|
|描述|概述：ASIL（Automotive Safety Integrity Level）是用于评估汽车系统中功能安全的风险等级，确保系统在发生故障时不会对乘客或环境造成不可接受的风险。ASIL分为四个等级：A、B、C、D，其中D级表示最高的安全要求。|
|描述|注意：ASIL的确定需要经过详细的风险评估过程，包括危害分析和风险评估；不同的ASIL等级要求不同的开发流程和验证措施；在系统设计中，必须确保所有安全相关的功能满足其对应的ASIL等级要求。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcucPartitionBswModuleExecution|
|描述|Denotes that this partition will execute BSW Modules. BSW Modules can only be executed in such partitions.|
|描述|概述：EcucPartitionBswModuleExecution用于定义在特定ECU分区中执行的BSW模块，确保BSW模块在正确的分区中运行以满足系统的隔离和资源管理需求。|
|描述|注意：确保每个BSW模块分配到正确的ECU分区以避免资源冲突；在多核系统中，注意跨分区通信的性能影响；配置时需遵循系统架构设计以确保模块间的正确交互。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|EcucPartitionQmBswModuleExecution|
|描述|Denotes that this partition will execute QM BSW.|
|描述|概述：EcucPartitionQmBswModuleExecution用于定义在特定ECU分区中执行的基本软件模块，确保这些模块在分区内的执行符合系统的隔离和资源管理要求。|
|描述|注意：确保分区内的模块执行不影响其他分区的功能和性能；合理配置以满足系统的安全和资源隔离需求；在多分区系统中注意模块间的通信和数据一致性。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|PartitionCanBeRestarted|
|描述|Specifies the requirement whether the Partition can be restarted. If set to true all software executing in this partition shall be capable of handling a restart.|
|描述|概述：PartitionCanBeRestarted用于定义在AUTOSAR系统中某个分区是否支持重新启动功能，确保系统在发生故障或需要更新时能够恢复到正常运行状态。|
|描述|注意：确保分区的状态和数据在重启后能够正确恢复；考虑重启对系统整体性能和实时性的影响；在设计时需考虑分区重启的依赖关系和可能的副作用。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcucPartitionBswModuleDistinguishedPartition|
|描述|This maps the abstract partition of the Bsw Module to a concrete Partition existing in the ECU.|
|描述|概述：EcucPartitionBswModuleDistinguishedPartition用于标识一个特殊的ECU分区，该分区中的BSW模块具有特定的执行或资源分配要求，以确保系统的安全性和功能性。|
|描述|注意：确保该分区的配置符合系统的安全和性能需求；避免在不必要的情况下使用此配置，以免增加系统复杂性；在多分区系统中，注意分区间的资源隔离和通信。|
|多实例个数|0 - inf|
|目标类型|BSW-DISTINGUISHED-PARTITION|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|EcucPartitionSoftwareComponentInstanceRef|
|描述|References the SW Component instances from the Ecu Extract that shall be executed in this partition.|
|描述|概述：EcucPartitionSoftwareComponentInstanceRef用于引用特定ECU分区中的软件组件实例，以便在配置中明确组件实例与ECU分区的关联。|
|描述|注意：确保引用的组件实例在指定的ECU分区中有效存在；引用应保持一致性，以避免配置错误；在多分区系统中，注意组件实例的跨分区引用是否符合系统设计要求。|
|多实例个数|0 - inf|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE|
|目标类型|SW-COMPONENT-PROTOTYPE|

## 4. EcucPostBuildVariants

|容器属性|值（容器）|
|---|---|
|名称|EcucPostBuildVariants|
|描述|Collection of toplevel PostBuildSelectable variants. The PredefinedVariants linked inside this container will determine how many PostBuildSelectableVariants exist. If this container exist the name pattern for initialization of BSW modules will be \<Mip\>_Config_\<PredefinedVariant.shortName\>. If this container does not exist the name pattern for initialization of BSW modlues will be \<Mip\>_Config.|
|描述|概述：EcucPostBuildVariants用于定义ECU配置的后期构建变体，允许在不重新编译的情况下通过不同的配置变体来调整ECU的行为，以适应不同的应用场景和需求。|
|描述|注意：确保每个变体的配置数据完整且一致，以避免运行时错误；变体的选择应在系统初始化时进行，并且不能在运行时动态更改；在配置工具中正确设置和管理变体，以确保生成的配置数据符合系统需求。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcucPostBuildVariantRef|
|描述|Reference to a PredefinedVariant that defines one toplevel postBuild configuration set (covering all post-build capable BSW modules). PredefinedVariants that are referenced here shall contain only PostBuildVariantCriterionValueSets.|
|描述|概述：EcucPostBuildVariantRef用于引用ECU配置的后期构建变体，允许在系统构建后选择不同的配置变体以适应不同的运行环境或需求。|
|描述|注意：确保引用的变体在构建后可用且有效；变体选择应与系统需求和运行环境相匹配；变体的管理和选择应遵循项目的版本控制和配置管理策略。|
|多实例个数|0 - inf|
|目标类型|PREDEFINED-VARIANT|

## 5. EcucUnitGroupAssignment

|容器属性|值（容器）|
|---|---|
|名称|EcucUnitGroupAssignment|
|描述|Collection of UnitGroup references to support the generation of ASAM MCD file.|
|描述|概述：EcucUnitGroupAssignment用于将ECU配置单元（EcucUnit）分配到特定的组中，以便进行模块化管理和配置，确保系统的灵活性和可维护性。|
|描述|注意：确保每个EcucUnit仅分配到一个组中以避免配置冲突；合理设计组结构以便于管理和更新；在配置工具中进行分配时，注意保持一致性和完整性。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|EcucUnitGroupRef|
|描述|Optional reference to the UnitGroup to support the generation of ASAM MCD file. These UnitGroups are selecting a set of units for a specific country.|
|描述|概述：EcucUnitGroupRef用于引用一个或多个Ecuc模块配置单元组，以便在配置过程中对这些单元组进行统一管理和操作。它帮助实现模块配置的组织和分组，简化配置管理。|
|描述|注意：确保引用的Ecuc模块配置单元组在系统中已定义；引用的单元组应具有一致的配置目标和用途；避免循环引用以防止配置冲突和复杂性增加。|
|多实例个数|0 - inf|
|目标类型|UNIT-GROUP|

## 6. EcucVariationResolver

|容器属性|值（容器）|
|---|---|
|名称|EcucVariationResolver|
|描述|Collection of PredefinedVariant elements containing definition of values for SwSystemconst which shall be applied when resolving the variability during ECU Configuration.|
|描述|概述：EcucVariationResolver用于处理ECU配置中的变体解析，确保在不同配置变体之间进行正确的选择和应用，以满足特定的系统需求和约束。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|PredefinedVariantRef|
|多实例个数|0 - inf|
|目标类型|PREDEFINED-VARIANT|
