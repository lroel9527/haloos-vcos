# Dcm 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Dcm|
|描述|Configuration of the Dcm (Diagnostic Communications Manager) module.|
|描述|概述：Dcm（Diagnostic Communication Manager）是AUTOSAR中负责管理车辆诊断通信的模块，它支持不同的诊断协议并处理来自外部测试设备的诊断请求。|
|描述|注意：在配置Dcm模块时，需要确保其与ECU的诊断需求和支持的诊断协议相匹配；Dcm配置参数必须符合AUTOSAR CP 4.4标准中定义的属性和结构；在多ECU系统中，应注意Dcm的网络管理和会话控制策略，以保证诊断通信的正确性和高效性。|
|多实例个数|0 - 1|

## 1. DcmConfigSet

|容器属性|值（容器）|
|---|---|
|名称|DcmConfigSet|
|描述|This container contains the configuration parameters and sub containers of the DCM module supporting multiple configuration sets.|
|描述|概述：DcmConfigSet是用于定义诊断通信管理器（Diagnostic Communication Manager）的配置集，包括诊断服务、会话控制、安全访问等相关参数的设置，以支持车辆的诊断通信需求。|
|描述|注意：在配置DcmConfigSet时，需要确保所有诊断服务的参数与车辆的诊断需求相匹配；对于安全访问和会话控制的配置，应考虑其对车辆安全性的影响；AUTOSAR CP 4.4标准中对诊断服务的配置和管理提供了详细的指导，应遵循这些指导以确保配置的正确性和有效性。|
|多实例个数|1 - 1|

### 1.1. DcmDsd

|容器属性|值（容器）|
|---|---|
|名称|DcmDsd|
|描述|These parameters configure the Diagnostic Service Dispatcher submodule.|
|描述|概述：DcmDsd（Diagnostic Session Dictionary）是AUTOSAR诊断通信管理器（Diagnostic Communication Manager）的配置项，用于定义诊断服务表，包括服务标识符、子功能以及对应的处理函数。|
|描述|注意：在配置DcmDsd时，必须确保每个诊断服务的标识符和子功能的组合是唯一的，以避免在诊断会话中的冲突；应当根据实际的车辆诊断需求来配置DcmDsd，确保所有必要的诊断服务都被正确定义；在AUTOSAR CP 4.4标准中，DcmDsd的配置应当遵循模块的最新规范，包括对服务处理函数的引用和诊断服务的权限管理。|
|多实例个数|1 - 1|

#### 1.1.1. DcmDsdServiceRequestManufacturerNotification

|容器属性|值（容器）|
|---|---|
|名称|DcmDsdServiceRequestManufacturerNotification|
|描述|The name of this container is used to define the name of the R-Port through which the DCM accesses the interface ServiceRequestNotification.|
|描述|概述：DcmDsdServiceRequestManufacturerNotification配置项用于定义在执行诊断服务请求时，如何通知制造商特定的软件模块。|
|描述|注意：在配置此项时，需要确保通知机制与制造商的软件模块兼容；此配置项应与诊断服务表（DSD）中的其他配置保持一致；在实施时应注意不同OEM的特定要求和标准。|
|说明|The R-Port is named ServiceRequestManufacturerNotification_{Name} where {Name} is the name of the container DcmDsdServiceRequestManufacturerNotification. The lowerMultiplicity is 0: If container DcmDsdServiceRequestManufacturerNotification does not exist the Indication API is not available.|
|多实例个数|0 - inf|

#### 1.1.2. DcmDsdServiceRequestSupplierNotification

|容器属性|值（容器）|
|---|---|
|名称|DcmDsdServiceRequestSupplierNotification|
|描述|The name of this container is used to define the name of the R-Port through which the DCM accesses the interface ServiceRequestNotification.|
|描述|概述：DcmDsdServiceRequestSupplierNotification配置项用于定义诊断服务分发（DSD）模块在接收到服务请求后，如何通知供应商（即服务处理模块）。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保通知机制与诊断服务处理模块的实现相兼容；通知策略应当支持同步和异步两种模式，以适应不同的服务处理需求；配置时应注意不同服务请求对通知时序和性能的影响。|
|说明|The R-Port is named ServiceRequestSupplierNotification_\<SWC\> where \<SWC\> is the name of the container DcmDsdServiceRequestSupplierNotification. The lowerMultiplicity is 0: If the container DcmDsdRequestSupplierNotification does not exist the Indication API is not available.|
|多实例个数|0 - inf|

#### 1.1.3. DcmDsdServiceTable

|容器属性|值（容器）|
|---|---|
|名称|DcmDsdServiceTable|
|描述|This container contains the configuration (DSD parameters) for a Service Identifier Table.|
|描述|概述：DcmDsdServiceTable配置项用于定义诊断服务分发表，它指定了哪些诊断服务（通过服务标识符）被分配到哪个诊断服务分发器（DSD）下，以及它们对应的处理函数。|
|描述|注意：确保每个服务标识符在DcmDsdServiceTable中唯一，以避免服务处理的冲突；在配置服务处理函数时，需考虑其执行时间，以满足系统的实时性要求；AUTOSAR CP 4.4标准中对服务的分发有明确规范，需要确保配置与标准一致。|
|说明|Note: It is allowed to add OBD services to a DcmDsdServiceTable related to a UDS Protocol. But it is not allowed to add UDS services to a DcmDsdServiceTable related to an OBD Protocol.|
|多实例个数|1 - 256|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDsdSidTabId|
|描述|Due to using possibly more service tables, the unique DcmDsdSidTabId can be used to identify them.|
|描述|概述：DcmDsdSidTabId 是用于标识诊断服务表（Diagnostic Service Table）的唯一标识符，它关联了一组特定的服务识别符（Service Identifier, SID）和对应的诊断服务处理程序。|
|描述|注意：在配置DcmDsdSidTabId时，必须确保每个诊断服务表的标识符是唯一的，以避免在诊断会话中的冲突；此外，该标识符通常由诊断配置工具自动生成，应避免手动修改以防止潜在的配置错误；在整个诊断系统中，应保持对应关系的一致性，确保诊断请求能够被正确解析和处理。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.1.3.1. DcmDsdService

|容器属性|值（容器）|
|---|---|
|名称|DcmDsdService|
|描述|This container contains the configuration (DSD parameters) for a Service.|
|描述|概述：DcmDsdService配置项定义了诊断服务调度层（Diagnostic Service Dispatcher）中的一个诊断服务，包括服务标识符（Service Identifier）和该服务所关联的子功能。|
|描述|注意：在配置DcmDsdService时，需要确保服务标识符的唯一性，避免与其他诊断服务冲突；还需关联正确的诊断服务处理器（Service Handler）和子功能，以保证诊断请求能够被正确处理；此外，应考虑服务的安全访问权限，确保只有在适当的诊断会话和安全等级下才能访问该服务。|
|多实例个数|1 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDsdServiceUsed|
|描述|Allows to activate or deactivate the usage of a Service. This parameter can be used for multi-purpose ECUs.|
|描述|概述：DcmDsdServiceUsed是一个配置参数，用于定义诊断服务调度器（Diagnostic Service Dispatcher）中所使用的诊断服务。|
|描述|注意：在配置DcmDsdServiceUsed时，需要确保只有在DcmDsd中声明的服务才能被使用；此外，每个服务应当与正确的子功能和请求长度匹配；最后，确保服务的安全访问权限设置符合项目的安全需求。|
|说明|true - service is available false - service is not available|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDsdSidTabSubfuncAvail|
|描述|Information about whether the service has subfunctions or not. This parameter is used for the handling of the "suppressPosRspMsgIndicationBit" as defined in ISO 14229-1, which can be used as a reference for the configuration.|
|描述|概述：DcmDsdSidTabSubfuncAvail配置项用于定义在诊断服务表中，特定服务标识符（SID）下支持的子功能的可用性。|
|描述|注意：在配置子功能可用性时，需要确保只有那些确实由ECU支持的子功能被标记为可用；不正确的配置可能导致诊断工具无法正确与ECU通信；在AUTOSAR CP 4.4标准中，应当遵循相关的诊断协议标准（如ISO 14229）来配置子功能的可用性。|
|说明|true - service has subfunctions, suppressPosRspMsgIndicationBit is available false - service has no subfunctions, suppressPosRspMsgIndicationBit is not available|
|多实例个数|1 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDsdSidTabFnc|
|描述|Callback function of the ECU Supplier specific component for the particular service. The function's prototype is as described for \<Module\>_\<DiagnosticService\>. If this parameter is not configured, the service is handled Dcm-internally.|
|描述|概述：DcmDsdSidTabFnc配置项用于定义诊断服务表中服务标识符（SID）对应的功能处理函数，它指定了当接收到特定SID时，应当调用的函数。|
|描述|注意：在配置DcmDsdSidTabFnc时，需要确保每个服务标识符对应一个唯一的功能处理函数；处理函数需要符合AUTOSAR标准中定义的接口要求；在配置多个服务标识符时，要注意避免SID之间的冲突。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDsdServiceRole|
|描述|Bitfield were each bit represents one dedicated role. A diagnostic service is granted access if the bit value is 1. If a bit value is 0, the service is not allowed to be executed for that role.|
|描述|概述：DcmDsdServiceRole配置项定义了诊断服务在诊断服务调度器（DSD）中的角色，用于指定该服务是供应商特定的服务还是标准服务，以及它是否需要会话控制或安全访问控制。|
|描述|注意：在配置DcmDsdServiceRole时，必须确保服务角色与实际的服务需求相匹配；对于需要会话控制或安全访问的服务，应正确配置相关属性以确保服务的安全性和有效性；AUTOSAR CP 4.4标准中对服务角色的定义和使用有明确规范，需要遵循这些规范以保证诊断服务的正确实现。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDsdSidTabServiceId|
|描述|Identifier of the service.|
|描述|概述：DcmDsdSidTabServiceId配置项用于定义诊断服务表中的服务标识符（Service Identifier, SID），它指定了哪些服务ID将被诊断会话层处理。|
|描述|注意：在配置DcmDsdSidTabServiceId时，需要确保服务ID与实际的诊断服务匹配，并且在同一诊断服务表中服务ID是唯一的；此外，服务ID应遵循ISO 14229和OEM特定的诊断服务ID规范；在配置过程中还应注意与DcmDsdSubServiceId的关联性，确保子服务ID的正确配置和使用。|
|说明|The possible service identifiers are defined in ISO 14229-1 and ISO 15031-5.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSidTabModeRuleRef|
|描述|Reference to a DcmDspModeRule which controls the execution of the service. If there is no reference configured, no mode rule check shall be performed.|
|描述|概述：DcmDsdSidTabModeRuleRef配置项用于引用特定的诊断会话控制模式规则，这些规则定义了在哪些诊断会话模式下，特定的服务标识符（SID）是有效的。|
|描述|注意：在配置DcmDsdSidTabModeRuleRef时，需要确保引用的模式规则与诊断服务表中定义的服务兼容；引用的模式规则必须在Dcm配置中预先定义；正确配置模式规则对于确保诊断服务的正确访问权限至关重要。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSidTabSecurityLevelRef|
|描述|Reference to a Security Level in which the service is allowed to be executed. Multiple references are allowed for a service.|
|描述|概述：DcmDsdSidTabSecurityLevelRef配置项用于将特定的诊断服务标识符（SID）表与相应的安全等级关联起来，确保只有在满足特定安全条件时才能访问和执行这些服务。|
|描述|注意：在配置时需确保引用的安全等级已经在Dcm的安全策略中定义；每个SID表应该引用至少一个安全等级，以保证服务的安全访问；在实施配置时，应考虑与诊断会话控制的安全等级配合使用，以实现更细粒度的访问控制。|
|说明|Please refer to ISO 14229-1, ISO 15031-5 and chapter "Verification of the Service Security Access levels." If there is no reference configured, no service security verification shall be performed.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSidTabSessionLevelRef|
|描述|Reference to a Session Level in which the service is allowed to be executed. Multiple references are allowed for a service.|
|描述|概述：DcmDsdSidTabSessionLevelRef配置项用于定义诊断服务标识符（SID）表中的服务可以在哪些诊断会话级别下被访问。|
|描述|注意：确保配置的会话级别与服务的实际需求相匹配；不同的服务可能需要在不同的诊断会话级别下可用；在配置时要考虑到诊断会话控制逻辑，以确保服务在适当的会话级别下被正确地授权或限制。|
|说明|Please refer to ISO 14229-1, ISO 15031-5 and chapter "Verification of the Diagnostic Session". If there is no reference configured, no diagnostic session verification shall be performed.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

###### 1.1.3.1.1. DcmDsdSubService

|容器属性|值（容器）|
|---|---|
|名称|DcmDsdSubService|
|描述|This container contains the configuration (DSD parameters) for a subservice of a service. Only those services may have subservices, which have the DcmDsdSidTabSubfuncAvail configured as TRUE.|
|描述|概述：DcmDsdSubService配置项用于定义诊断服务中的子服务信息，包括子服务的标识符、相关条件以及对应的处理函数。|
|描述|注意：在配置DcmDsdSubService时，需要确保子服务标识符的唯一性，以避免在同一诊断服务中出现冲突；子服务处理函数应当与子服务的功能和要求相匹配，确保正确响应诊断请求；还需考虑安全访问条件，确保只有在满足特定条件下才能执行子服务。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDsdSubServiceUsed|
|描述|Allows to activate or deactivate the usage of a Subservice. This parameter can be used for multi-purpose ECUs.|
|描述|概述：DcmDsdSubServiceUsed配置项用于指定在诊断会话控制中，哪些子服务应被激活或使用。|
|描述|注意：确保只有在需要的诊断会话中激活相应的子服务，以避免不必要的资源消耗；子服务的配置应符合车辆制造商的诊断策略和安全要求；在配置时需遵循AUTOSAR CP 4.4标准中对诊断服务的具体要求和限制。|
|说明|true - subservice is available false - subservice is not available.|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDsdSubServiceFnc|
|描述|Callback function of the ECU Supplier specific component for the particular service. The function's prototype is as described for \<Module\>_\<DiagnosticService\>_\<SubService\>.|
|描述|概述：DcmDsdSubServiceFnc配置项用于定义诊断子服务的处理函数，这些函数负责执行与特定诊断子服务相关的操作。|
|描述|注意：确保为每个诊断子服务正确配置对应的处理函数，避免诊断功能执行错误；处理函数需要遵循AUTOSAR CP 4.4标准中定义的接口规范；在配置处理函数时，考虑其执行时间对系统性能的影响，以免影响整体诊断响应时间。|
|说明|If this parameter is not configured, the subservice is handled Dcm-internally.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDsdSubServiceId|
|描述|Identifier of the subservice.|
|描述|概述：DcmDsdSubServiceId配置项用于定义诊断服务中子服务的唯一标识符，这个标识符用于区分不同的子服务，以便在诊断会话中正确处理各种子服务请求。|
|描述|注意：在配置子服务时，必须确保每个子服务的标识符是唯一的，以避免在诊断服务分派时发生冲突；子服务标识符通常是一个字节大小的值，因此它的取值范围应该在0x00到0xFF之间；在配置子服务标识符时，还需要考虑与全局服务标识符的关系，确保它们在诊断服务分派器中能够被正确解析和处理。|
|说明|The possible subservice identifiers are defined in ISO 14229-1 and ISO 15031-5.|
|多实例个数|1 - 1|
|取值范围|0 - 127|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDsdSubServiceRole|
|描述|Bitfield were each bit represents one dedicated role. A sub-function of a diagnostic service is granted access if the bit value is 1. If a bit value is 0, the service is not allowed to be executed for that role.|
|描述|概述：DcmDsdSubServiceRole配置项定义了诊断子服务在诊断服务调度器（DSD）中的角色，用于控制子服务的执行权限和行为。|
|描述|注意：在配置DcmDsdSubServiceRole时，需要确保子服务的角色与其预期的行为一致；角色类型通常包括默认角色、功能请求角色和物理请求角色；在配置时应注意不同角色对安全访问级别的要求。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSubServiceModeRuleRef|
|描述|Reference to a DcmDspModeRule which controls the execution of the subservice.|
|描述|概述：DcmDsdSubServiceModeRuleRef配置项用于引用一个特定的诊断会话模式规则，该规则定义了在哪些诊断会话模式下子服务可以被执行。|
|描述|注意：确保引用的会话模式规则与子服务的实际需求相匹配；在配置时应注意不同诊断服务之间的会话模式规则可能存在冲突；在AUTOSAR CP 4.4标准中，会话模式规则需要在Dcm配置中明确定义，并且正确关联到相应的子服务。|
|说明|If there is no reference configured, no mode rule check shall be performed.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSubServiceSecurityLevelRef|
|描述|Reference to a Security Level in which the subservice is allowed to be executed. Multiple references are allowed for a subservice.|
|描述|概述：DcmDsdSubServiceSecurityLevelRef配置项用于定义诊断子服务的安全级别，确保只有在满足特定安全条件下才能访问这些子服务。|
|描述|注意：在配置时需确保安全级别与子服务的安全需求相匹配；不正确的安全级别配置可能导致未授权的访问或功能受限；AUTOSAR CP 4.4标准中，安全级别的配置应详细且清晰，避免安全漏洞。|
|说明|Please refer to ISO 14229-1, ISO 15031-5 and chapter "Verification of the Service Security Access levels." If there is no reference configured, no subservice security verification shall be performed.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDsdSubServiceSessionLevelRef|
|描述|Reference to a Session Level in which the subservice is allowed to be executed. Multiple references are allowed for a subservice.|
|描述|概述：DcmDsdSubServiceSessionLevelRef配置项用于指定诊断子服务（SubService）可以在哪些诊断会话级别（Diagnostic Session Level）下被执行，确保诊断服务的执行符合当前会话级别的权限要求。|
|描述|注意：确保为每个诊断子服务正确配置会话级别，避免在不允许的会话级别下执行诊断操作；AUTOSAR CP 4.4标准中，会话级别的配置应遵循诊断服务需求，不正确的配置可能导致诊断服务无法在特定会话级别下执行；在配置时，应参考相关诊断协议标准，如ISO 14229等，以确保兼容性和标准的遵循。|
|说明|Please refer to ISO 14229-1, ISO 15031-5 and chapter "Verification of the Diagnostic Session". If there is no reference configured, no diagnostic session verification shall be performed.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

### 1.2. DcmDsl

|容器属性|值（容器）|
|---|---|
|名称|DcmDsl|
|描述|These parameters configure the Diagnostic Session Layer submodule.|
|描述|概述：DcmDsl（Diagnostic Communication Manager Diagnostic Session Layer）是AUTOSAR中负责管理诊断通信会话层的配置项，它定义了诊断服务请求和响应之间的通信规则，以及与客户端（通常是诊断工具）的交互方式。|
|描述|注意：在配置DcmDsl时，需确保与车辆的诊断协议和诊断需求相匹配；注意DcmDsl配置与DcmDsd（Diagnostic Service Dispatcher）和DcmDsp（Diagnostic Service Processor）的交互关系；在配置诊断会话控制、测试仪器控制和网络管理等功能时，应遵循AUTOSAR CP 4.4标准的相关规定。|
|多实例个数|1 - 1|

#### 1.2.1. DcmDslBuffer

|容器属性|值（容器）|
|---|---|
|名称|DcmDslBuffer|
|描述|This container contains the configuration of a diagnostic buffer.|
|描述|概述：DcmDslBuffer配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的缓冲区，这些缓冲区用于存储发送或接收的诊断消息。|
|描述|注意：缓冲区大小应根据实际需求和最大可能的诊断消息长度来配置，以避免溢出；确保每个缓冲区的唯一性和正确的关联到相应的DcmDslProtocol；在多客户端环境中，管理缓冲区的分配和释放以防止数据冲突。|
|多实例个数|1 - 256|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslBufferSize|
|描述|Size of the diagnostic buffer in bytes.|
|描述|概述：DcmDslBufferSize配置项用于指定诊断会话层（Diagnostic Session Layer）中用于存储接收和发送诊断消息的缓冲区大小。|
|描述|注意：缓冲区大小应足够容纳最大可能的诊断请求和响应消息；过小的缓冲区可能导致消息处理失败，过大的缓冲区可能会浪费资源；在配置时需考虑ECU的内存限制和诊断需求。|
|说明|For a linear buffer the size shall be as large as the longest diagnostic message (request or response). For a paged buffer the size has impacts on the application performance.|
|多实例个数|1 - 1|
|取值范围|8 - 65535|

#### 1.2.2. DcmDslCallbackDCMRequestService

|容器属性|值（容器）|
|---|---|
|名称|DcmDslCallbackDCMRequestService|
|描述|Each DcmDslCallbackDCMRequestService container defines an R-Port with the CallbackDCMRequestServices interface which the Dcm uses to ask permission for protocol changes from the application software. The R-Port has the name CallbackDCMRequestServices_\<SWC\> where \<SWC\> is the name of this container.|
|描述|概述：DcmDslCallbackDCMRequestService配置项用于定义诊断服务请求时的回调函数，这些回调函数在诊断请求的不同阶段被调用，以实现特定的功能，如权限控制、服务处理前后的操作等。|
|描述|注意：在配置时需确保回调函数与服务请求处理流程兼容；回调函数应遵循AUTOSAR规定的接口和行为模式；在多服务处理场景中，应注意回调函数的执行顺序和资源共享问题。|
|多实例个数|0 - 255|

#### 1.2.3. DcmDslDiagResp

|容器属性|值（容器）|
|---|---|
|名称|DcmDslDiagResp|
|描述|This container contains the configuration of the automatic requestCorrectlyReceivedResponsePending response management in the Dcm.|
|描述|概述：DcmDslDiagResp配置项定义了诊断响应消息的发送行为，包括消息的优先级、缓冲区大小和发送策略，确保诊断响应能够按照既定的方式被正确处理和发送。|
|描述|注意：在配置DcmDslDiagResp时，必须确保为每个诊断请求设置合适的响应优先级，以避免重要信息的延迟；缓冲区大小应根据实际需要合理设置，以防止数据溢出或资源浪费；发送策略的选择应考虑网络带宽和系统处理能力，以优化诊断通信性能。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDslDiagRespOnSecondDeclinedRequest|
|描述|Defines the reaction upon a second request (ClientB) that can not be processed (e.g. due to priority assessment).|
|描述|概述：DcmDslDiagRespOnSecondDeclinedRequest配置项用于定义诊断服务层（DcmDsl）在连续两次请求被拒绝时的响应行为，确保了对异常请求的处理符合诊断通信管理的要求。|
|描述|注意：该配置项对于确保诊断通信的健壮性和安全性至关重要；必须确保配置正确以避免潜在的通信安全风险；在AUTOSAR CP 4.4标准中，该配置项的属性和行为应详细参照相关诊断通信管理规范进行配置。|
|说明|TRUE: when the second request (Client B) can not be processed, it shall be answered with NRC21 BusyRepeatRequest. FALSE: when the second request (Client B) can not be processed, it shall not be responded.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslDiagRespMaxNumRespPend|
|描述|Maximum number of negative responses with response code 0x78 (requestCorrectlyReceivedResponsePending) allowed for a request. If Dcm reaches this limit, an automatic 0x10 (generalReject) final response will be trasmitted and the service processing will be cancelled.|
|描述|概述：DcmDslDiagRespMaxNumRespPend 定义了在等待诊断响应期间，诊断通信管理器（DCM）可以发送的最大“响应待定”消息数量。|
|描述|注意：该参数的设置应考虑ECU处理能力和网络带宽，以避免通信拥堵；过高的设置可能导致客户端超时错误；AUTOSAR CP 4.4标准中此配置项的默认值和范围应严格遵守以保证诊断通信的可靠性。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDslDiagResponseIndicationFunc|
|描述|DcmDslDiagResponseIndicationFunc defines the function interface for passing the diagnostic response data to the user to do debugging related work during the transmission of the diagnostic response data.|
|描述|概述：DcmDslDiagResponseIndicationFunc定义了在传输诊断响应数据的过程中，将诊断响应数据传递给用户做调试相关工作的函数接口。|
|描述|注意：此配置为非标配置项，仅为用户调试过程中所使用，如果正常量产应用则需要关闭该接口，即不设置该接口的函数名。|
|说明|If this parameter is not configured, the subservice is handled Dcm-internally.|
|多实例个数|0 - 1|

#### 1.2.4. DcmDslProtocol

|容器属性|值（容器）|
|---|---|
|名称|DcmDslProtocol|
|描述|This container contains the configurations of the diagnostic protocols used in Dcm.|
|描述|概述：DcmDslProtocol配置项定义了诊断通信层协议的属性，包括诊断协议类型（如UDS，OBD等），以及与之相关的通信参数和定时器设置。|
|描述|注意：在配置DcmDslProtocol时，需要确保选择的协议类型与车辆标准和法规要求相匹配；同时，通信参数和定时器设置必须满足诊断协议的性能要求；此外，应注意与网络层的兼容性和整个诊断系统的一致性。|
|多实例个数|1 - 1|

##### 1.2.4.1. DcmDslProtocolRow

|容器属性|值（容器）|
|---|---|
|名称|DcmDslProtocolRow|
|描述|This container contains the configuration of one particular diagnostic protocol used in Dcm.|
|描述|概述：DcmDslProtocolRow配置项定义了诊断通信管理器（Diagnostic Communication Manager）中的协议行，它指定了诊断协议层的配置，如ISO TP、KWP2000等，以及这些协议的相关参数。|
|描述|注意：在配置DcmDslProtocolRow时，需要确保协议参数与实际使用的诊断协议标准一致；应注意与DcmDslProtocol配置的一致性和兼容性；在多协议系统中，还需确保不同DcmDslProtocolRow之间的参数设置不会相互冲突。|
|多实例个数|1 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDslProtocolRowUsed|
|描述|Allows to activate or deactivate the usage of a Protocol. This parameter can be used for multi-purpose ECUs.|
|描述|概述：DcmDslProtocolRowUsed配置项用于指定诊断通信管理器（Diagnostic Communication Manager）中使用的协议行，它定义了诊断会话层协议（如ISO 14229, ISO 15765等）的具体实现和行为。|
|描述|注意：在配置DcmDslProtocolRowUsed时，需要确保所选协议与车辆支持的诊断协议一致；每个DcmDslProtocolRow配置必须关联到至少一个DcmDslProtocol，以确保正确的协议行被激活；在多协议系统中，应注意协议之间的优先级和切换逻辑，以避免潜在的冲突。|
|说明|true - protocol is available false - protocol is not available.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmSendRespPendOnRestart|
|描述|If set to TRUE, the Dcm will send a NRC 0x78 before a transition to bootloader or performing an ECU reset. If set to False, no 0x78 is send in this case.|
|描述|概述：DcmSendRespPendOnRestart配置项用于定义诊断通信管理模块（Diagnostic Communication Manager, DCM）在ECU重启后是否发送响应挂起（Response Pending）消息。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项的使用需要谨慎，确保在ECU重启过程中对诊断请求的处理符合预期；重启行为可能会影响诊断会话的连续性，因此需要特别注意会话管理；此配置项的使用应结合具体的应用场景和ECU的诊断策略来决定。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDslProtocolTransType|
|描述|This parameter is used only if the protocol is of type DCM_ROE_ON_xxx. It selects the transmission type of the protocol.|
|描述|概述：DcmDslProtocolTransType 定义了诊断通信管理器（Diagnostic Communication Manager）中使用的传输类型，如正常、周期性或响应式传输。|
|描述|注意：在配置DcmDslProtocolTransType时，必须确保所选传输类型与车辆网络的支持和诊断需求相匹配；不正确的传输类型配置可能导致诊断通信失败或性能下降；AUTOSAR CP 4.4标准支持多种传输类型，应详细了解每种类型的适用场景。|
|多实例个数|0 - 1|
|默认值|TYPE1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDslProtocolType|
|描述|The diagnostic protocol type for the DCM DSL protocol that is being configured.|
|描述|概述：DcmDslProtocolType配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中使用的诊断协议类型，如ISO 14229 (UDS) 或 ISO 15765 (DoCAN)。|
|描述|注意：在配置DcmDslProtocolType时，必须确保选择的协议类型与车辆的诊断需求和规范相匹配；不同的协议类型可能会要求不同的配置参数和服务集；在实施时，应考虑与其他诊断协议的兼容性和共存问题。|
|说明|Implementation Type: Dcm_ProtocolType|
|多实例个数|1 - 1|
|默认值|DCM_UDS_ON_CAN|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmTimStrP2ServerAdjust|
|描述|This parameter is used to guarantee that the diagnostic response is available on the bus before reaching P2 by adjusting the current DcmDspSessionP2ServerMax.|
|描述|概述：DcmTimStrP2ServerAdjust 用于调整诊断通信中服务器的P2定时器，这是响应客户端请求后服务器在规定时间内必须给出响应的时间。|
|描述|注意：该配置项的值必须根据具体的车辆网络环境和诊断需求进行调整；不正确的P2Server时间设置可能导致诊断通信失败或性能下降；应遵循OEM的具体规定和标准来设置此参数。|
|说明|This parameter mainly represents the software architecture dependent communication delay between the time the transmission is initiated by DCM and the time when the message is actually transmitted to the bus. The parameter value is defined in seconds and must be a multiple of DcmTaskTime.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmTimStrP2StarServerAdjust|
|描述|This parameter is used to guarantee that the diagnostic response is available on the bus before reaching P2Star by adjusting the current DcmDspSessionP2StarServerMax.|
|描述|概述：DcmTimStrP2StarServerAdjust配置项用于调整诊断通信控制器（Diagnostics Communication Manager）中的P2\*服务器定时器，该定时器定义了服务器在发送响应之前等待客户端请求的最大时间。|
|描述|注意：该值通常需要根据具体的车辆网络环境和诊断需求进行调整；过小的值可能导致网络拥堵时无法正确响应诊断请求，过大的值可能导致诊断响应延迟；在调整此参数时，应遵循相关的诊断标准和制造商的指导。|
|说明|This parameter mainly represents the software architecture dependent communication delay between the time the transmission is initiated by DCM and the time when the message is actually transmitted to the bus. The parameter value is defined in seconds and must be a multiple of DcmTaskTime.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 5|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslProtocolMaximumResponseSize|
|描述|This parameter is mandatory and defines the maximum length of the response message in case DcmPagedBufferEnabled == TRUE|
|描述|概述：DcmDslProtocolMaximumResponseSize配置项用于定义诊断通信层中，针对每个诊断协议所能支持的最大响应报文大小，确保诊断响应不会超过ECU的缓冲区限制。|
|描述|注意：在配置时需确保该值不小于诊断服务的最大可能响应长度；同时考虑到网络层的限制，如ISO TP的单帧或多帧传输限制；此外，该值应小于或等于ECU硬件和网络接口的最大承载能力。|
|多实例个数|0 - 1|
|默认值|4095|
|取值范围|1 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslProtocolPriority|
|描述|Protocol priority used during protocol preemption. A higher priority protocol may preempt a lower priority protocol.|
|描述|概述：DcmDslProtocolPriority配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中不同诊断协议之间的优先级，以决定在多个诊断请求同时到达时哪个协议应该被优先处理。|
|描述|注意：在配置时必须确保每个诊断协议都有一个唯一的优先级值；优先级的配置应该反映实际的系统需求，确保关键诊断服务能够优先处理；在实际应用中，应考虑到不同车辆网络（如CAN, LIN, FlexRay等）的特性和要求，合理分配优先级。|
|说明|Lower numeric values represent higher protocol priority: 0 - Highest protocol priority 255 - Lowest protocol priority|
|多实例个数|1 - 1|
|默认值|1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspProtocolEcuAddr|
|描述|Ecu source address used for diagnostic communication. This parameter is required for Generic Connections.|
|描述|概述：DcmDspProtocolEcuAddr配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，针对不同诊断协议的ECU地址信息，确保诊断请求能够正确地被ECU识别和处理。|
|描述|注意：在配置DcmDspProtocolEcuAddr时，需要确保地址信息与车辆网络中的实际地址匹配；对于使用相同诊断协议的不同ECU，应有不同的地址配置以避免冲突；此配置项应与车辆的网络管理配置保持一致，以确保诊断服务的正确路由。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDemClientRef|
|描述|Reference to DemClient in Dem configuration.|
|描述|概述：DcmDemClientRef是一个配置项，用于在诊断通信管理器（Diagnostic Communication Manager, DCM）模块中引用诊断事件管理器（Diagnostic Event Manager, DEM）的客户端标识符，实现DCM与DEM之间的交互。|
|描述|注意：确保引用的DEM客户端标识符在DEM模块中已定义，以保证DCM能正确访问DEM服务；在配置时应注意版本兼容性，确保DCM和DEM模块遵循相同或兼容的AUTOSAR版本；在多客户端系统中，正确管理每个DCM客户端与DEM的关联，避免配置错误导致诊断服务失败。|
|说明|Used by the Dem to distinguish different client calls.|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemGeneral/DemClient|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolRxBufferRef|
|描述|Reference to a configured diagnostic buffer that is used for diagnostic request reception for the protocol.|
|描述|概述：DcmDslProtocolRxBufferRef配置项用于指定诊断通信层（DcmDsl）中用于接收数据的缓冲区引用，确保诊断请求能够被正确接收并存储。|
|描述|注意：在配置时需确保引用的缓冲区大小足以容纳预期的最大诊断请求消息；缓冲区应当独立于其他通信对象以避免数据冲突；在多协议配置中，每个协议可能需要独立的接收缓冲区。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsl/DcmDslBuffer|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolSIDTable|
|描述|Reference to a service table that is used for diagnostic request processing for this protocol.|
|描述|概述：DcmDslProtocolSIDTable配置项用于定义诊断会话层中支持的服务标识符（Service Identifier，SID）及其关联的处理函数，确保诊断请求能够被正确解析和响应。|
|描述|注意：在配置DcmDslProtocolSIDTable时，必须确保每个SID与其对应的处理函数正确映射，避免服务处理混淆；应考虑诊断会话控制和安全访问限制，以免在不适当的会话或安全级别下执行服务；根据AUTOSAR CP 4.4标准，还需确保配置项与诊断协议（如UDS，KWP2000等）的要求相符。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsd/DcmDsdServiceTable|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolTxBufferRef|
|描述|Reference to a configured diagnostic buffer that is used for diagnostic response transmission for the protocol.|
|描述|概述：DcmDslProtocolTxBufferRef配置项用于指定诊断会话层（Dsl）中，用于传输响应消息的缓冲区引用，确保诊断响应能够被正确地存储和发送。|
|描述|注意：必须确保引用的TxBuffer足够大，以容纳可能的最大响应消息；在配置多个诊断协议时，应注意不同协议可能需要不同大小的TxBuffer；该配置项在AUTOSAR CP 4.4中是必需的，缺失或错误配置可能导致诊断通信失败。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsl/DcmDslBuffer|

###### 1.2.4.1.1. DcmDslConnection

|容器属性|值（容器）|
|---|---|
|名称|DcmDslConnection|
|描述|This container contains the configuration of a communication channel for one particular protocol.|
|描述|概述：DcmDslConnection配置项定义了诊断通信管理器（Diagnostic Communication Manager）中客户端（通常是诊断工具）与服务器（车辆控制单元或ECU）之间的通信连接参数，包括连接的类型、通信协议和优先级等。|
|描述|注意：在配置DcmDslConnection时，需确保通信协议与车辆支持的诊断协议一致；连接类型应根据实际的诊断需求和车辆网络架构选择；优先级设置需考虑到不同诊断任务之间的相对重要性，避免重要诊断任务被延迟或阻塞。|
|说明|Note that it is allowed to communicate with multiple testers, therefore multiple connections may be configured for a protocol.|
|多实例个数|1 - inf|

####### 1.2.4.1.1.1. DcmDslMainConnection

|容器属性|值（容器）|
|---|---|
|名称|DcmDslMainConnection|
|描述|This container contains the configuration for a main connection of a diagnostic protocol. Additionally it may contain references to ROE and Periodic connections if the protocol type or protocol transmission type needs them.|
|描述|概述：DcmDslMainConnection配置项定义了诊断通信管理器（Diagnostic Communication Manager）中主连接的属性，这包括了与客户端（如诊断工具）的通信参数和连接引用。|
|描述|注意：在配置DcmDslMainConnection时，需要确保它与所引用的DcmDslProtocolRow和DcmDslConnection配置一致；主连接应该唯一地关联到一个特定的诊断协议；在配置多个连接时，要注意它们之间的优先级和冲突管理。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslProtocolRxConnectionId|
|描述|Unique identifier of the tester which uses this connection for diagnostic communication.|
|描述|概述：DcmDslProtocolRxConnectionId 是用于定义诊断通信管理器（Diagnostic Communication Manager）中，诊断协议层与网络层之间的接收连接标识符，确保正确的数据传输和接收。|
|描述|注意：在配置时需确保每个DcmDslProtocolRxConnectionId是唯一的，以避免数据接收时的冲突；该标识符通常与具体的通信通道和网络协议栈配置相关联；在配置多个诊断协议时，应注意不同协议间的连接标识符不要重复。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslProtocolRxTesterSourceAddr|
|描述|Tester source address uniquely describes a client and will be used e.g within the jump to Bootloader interfaces. This parameter is not required for generic connections (DcmPdus with MetaDataLength \>= 1).|
|描述|概述：DcmDslProtocolRxTesterSourceAddr配置项定义了用于车辆诊断通信中，接收端（通常是车辆的诊断控制模块）所期望的测试仪器的源地址。|
|描述|注意：在配置时需确保地址符合网络中实际测试设备的地址；不同的诊断协议可能需要不同的源地址配置；源地址配置错误可能导致诊断通信失败。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslPeriodicTransmissionConRef|
|描述|Reference to a periodic transmission connection which is used for the processing of periodic transmission events.|
|描述|概述：DcmDslPeriodicTransmissionConRef配置项用于引用Dcm中用于周期性传输的连接，它指定了哪些网络连接可以用于周期性数据的传输。|
|描述|注意：在配置周期性传输时，确保引用的网络连接支持所需的传输协议和带宽；周期性传输可能对网络带宽和ECU处理能力有较高要求，需谨慎配置；AUTOSAR CP 4.4中对于周期性传输的支持和配置可能有特定限制或要求，需要参考具体的AUTOSAR文档。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsl/DcmDslProtocol/DcmDslProtocolRow/DcmDslConnection/DcmDslPeriodicTransmission|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolComMChannelRef|
|描述|Reference to the ComMChannel on which the DcmDslProtocolRxPdu is received and the DcmDslProtocolTxPdu is transmitted.|
|描述|概述：DcmDslProtocolComMChannelRef配置项用于指定诊断通信管理（Diagnostic Communication Manager）层中，每个诊断协议所使用的通信通道引用。|
|描述|注意：确保每个诊断协议正确引用了对应的ComM通道，以保证诊断消息能够通过正确的网络通道传输；在配置时需注意与网络管理配置的一致性，避免配置错误导致通信失败；该配置项在AUTOSAR CP 4.4标准中是必需的，缺失可能导致诊断功能不完整或不可用。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslROEConnectionRef|
|描述|Reference to a ResponseOnEvent connection which is used for the processing of ResponseOnEvent events.|
|描述|概述：DcmDslROEConnectionRef配置项用于定义诊断通信管理（Diagnostic Communication Manager）中，响应式事件（Response On Event, ROE）与网络连接之间的关联。这使得系统能够在特定网络连接上根据事件触发诊断响应。|
|描述|注意：在配置DcmDslROEConnectionRef时，必须确保引用的网络连接已经定义且有效；此配置项对于实现基于事件的诊断通信至关重要，因此需要仔细配置以避免通信问题；AUTOSAR CP 4.4标准中，对于ROE的支持和配置要求可能与早期版本有所不同，需要注意版本间的兼容性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsl/DcmDslProtocol/DcmDslProtocolRow/DcmDslConnection/DcmDslResponseOnEvent|

######## 1.2.4.1.1.1.1. DcmDslProtocolRx

|容器属性|值（容器）|
|---|---|
|名称|DcmDslProtocolRx|
|描述|This container contains the configuration parameters of a reception channel in a diagnostic connection.|
|描述|概述：DcmDslProtocolRx配置项用于定义诊断通信层中接收通道的属性，包括接收数据的协议、PDU ID、以及与之相关的资源和参数。|
|描述|注意：在配置DcmDslProtocolRx时，需要确保PDU ID与ECU中实际的PDU配置相匹配；此外，应当注意与DcmDslProtocolTx配置项的一致性，以保证诊断通信的双向性；最后，该配置项的属性应符合AUTOSAR CP 4.4标准中对诊断通信层的规定。|
|说明|The PDU referenced by this reception channel can consume meta data items of type SOURCE_ADDRESS_16 and TARGET_ADDRESS_16.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDslProtocolRxAddrType|
|描述|Selects the addressing type of the reception channel. Physical addressing is used for 1:1 communication, functional addressing is used for 1:N communication.|
|描述|概述：DcmDslProtocolRxAddrType配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，不同诊断协议下的接收地址类型，如物理地址或功能地址。|
|描述|注意：在配置DcmDslProtocolRxAddrType时，需要确保地址类型与诊断协议的要求相匹配；此配置项对于确保正确的诊断请求路由至适当的服务组件至关重要；在多协议环境中，应注意不同协议间的地址类型可能会有所不同，需要分别配置。|
|说明|For details refer to ISO 14229-1.|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslProtocolRxPduId|
|描述|Identifier of the PDU that is used for this reception channel.|
|描述|概述：DcmDslProtocolRxPduId配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，接收协议数据单元（Protocol Data Unit）的标识符，它关联了网络层的接收PDU与Dcm的特定协议。|
|描述|注意：在配置DcmDslProtocolRxPduId时，必须确保PDU ID与ECU中定义的PDU相匹配，并且在整个系统中是唯一的；此外，PDU ID应与正确的Dcm协议层配置相对应，以确保诊断消息能够被正确处理；在配置时还应注意PDU的传输方向，确保是接收方向的PDU ID。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolRxPduRef|
|描述|Reference to a Pdu in EcuC that is used for this reception channel.|
|描述|概述：DcmDslProtocolRxPduRef配置项用于指定诊断通信管理器（Diagnostic Communication Manager）中，诊断会话层（Diagnostic Session Layer）所使用的接收PDU（Protocol Data Unit）的引用。|
|描述|注意：确保引用的PDU与所需的诊断协议匹配；PDU配置必须在PduR模块中正确定义；在配置多个协议时，注意PDU的唯一性和冲突避免。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

######## 1.2.4.1.1.1.2. DcmDslProtocolTx

|容器属性|值（容器）|
|---|---|
|名称|DcmDslProtocolTx|
|描述|This container contains the configuration parameters of a transmission channel in a diagnostic connection.|
|描述|概述：DcmDslProtocolTx配置项定义了诊断通信管理器（Diagnostic Communication Manager）中的传输协议层，用于管理与车辆控制单元（ECU）之间的数据传输。|
|描述|注意：在配置DcmDslProtocolTx时，必须确保其与车辆的ECU支持的协议一致；配置错误可能导致诊断通信失败；此配置项应与DcmDslProtocolRx相匹配，以确保数据的双向正确传输。|
|说明|The PDU referenced by this transmission channel can produce meta data items of type TARGET_ADDRESS_16 and SOURCE_ADDRESS_16.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslTxConfirmationPduId|
|描述|Identifier of the PDU that is used by the lower level module for transmission confirmation of responses on this channel.|
|描述|概述：DcmDslTxConfirmationPduId用于标识诊断通信管理（Diagnostic Communication Manager）模块中，发送确认消息时所使用的协议数据单元（PDU）ID。|
|描述|注意：该配置项必须与实际使用的PDU ID一致，以确保正确的消息确认；在配置时需注意与其他模块的PDU ID避免冲突；在AUTOSAR CP 4.4中，确保PDU ID的配置符合ECU的通信需求和规范。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslProtocolTxPduRef|
|描述|Reference to a Pdu in EcuC that is used for this transmission channel.|
|描述|概述：DcmDslProtocolTxPduRef配置项用于指定诊断会话层（DcmDsl）中，用于传输（发送）诊断消息的PDU（协议数据单元）引用。|
|描述|注意：确保引用的PDU与所需的诊断协议兼容；在配置多个协议时，注意避免PDU引用冲突；AUTOSAR CP 4.4中，该配置项的属性应与PDU属性匹配，若有不一致，需检查PDU配置。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

####### 1.2.4.1.1.2. DcmDslPeriodicTransmission

|容器属性|值（容器）|
|---|---|
|名称|DcmDslPeriodicTransmission|
|描述|This container contains the configuration of a periodic transmission connection.|
|描述|概述：DcmDslPeriodicTransmission配置项用于定义诊断通信层中，周期性数据传输的参数和行为，这包括周期性响应的发送间隔和优先级等设置。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保周期性传输的配置不会与其他网络通信活动发生冲突；合理设置周期性传输的时间间隔，以避免对网络的过度占用；考虑到不同ECU的处理能力和网络带宽，应当在系统级别上协调周期性传输的配置。|
|多实例个数|0 - 1|

######## 1.2.4.1.1.2.1. DcmDslPeriodicConnection

|容器属性|值（容器）|
|---|---|
|名称|DcmDslPeriodicConnection|
|描述|This container contains the configuration of a transmission channel for a periodic transmission connection.|
|描述|概述：DcmDslPeriodicConnection配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，周期性数据传输的连接参数，包括周期性消息的发送间隔和优先级。|
|描述|注意：在配置周期性连接时，需确保发送间隔和优先级符合网络带宽和系统处理能力；配置的值应与ECU的实际能力和网络管理策略相匹配；在多ECU系统中，还需考虑不同ECU间的周期性消息协调。|
|说明|The PDU referenced by this transmission channel can produce meta data items of type TARGET_ADDRESS_16 and SOURCE_ADDRESS_16.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslPeriodicTxConfirmationPduId|
|描述|Identifier of the PDU that is used by the lower level module for transmission confirmation of responses on this channel.|
|描述|概述：DcmDslPeriodicTxConfirmationPduId配置项用于定义诊断通信层（DcmDsl）中，周期性传输确认的PDU标识符，这是用于确认周期性响应消息已经被成功发送的。|
|描述|注意：在配置DcmDslPeriodicTxConfirmationPduId时，需要确保PDU ID与ECU中定义的PDU ID一致；此ID应与实际用于周期性消息传输的PDU ID相匹配；在配置时应注意不要与其他PDU ID冲突，以避免通信错误。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslPeriodicTxPduRef|
|描述|Reference to a Pdu in EcuC that is used for this periodic transmission channel.|
|描述|概述：DcmDslPeriodicTxPduRef配置项用于引用由诊断通信管理器（Diagnostic Communication Manager）定期发送的PDU（协议数据单元）。|
|描述|注意：在配置DcmDslPeriodicTxPduRef时，需要确保引用的PDU符合诊断协议要求，并且已经在PDU路由表中正确定义；此外，该PDU应当配置为可定期发送，以支持Dcm的定期数据传输需求；在配置过程中，还需注意PDU的传输属性，如周期时间和带宽管理，以确保系统资源的有效利用和通信的可靠性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

####### 1.2.4.1.1.3. DcmDslResponseOnEvent

|容器属性|值（容器）|
|---|---|
|名称|DcmDslResponseOnEvent|
|描述|This container contains the configuration of a ResponseOnEvent connection.|
|描述|概述：DcmDslResponseOnEvent配置项用于定义诊断通信管理器（Diagnostic Communication Manager）在特定事件发生时如何响应，例如在接收到特定的诊断请求或者内部事件时。|
|描述|注意：在配置DcmDslResponseOnEvent时，需要确保事件触发条件与响应动作之间的映射关系符合系统的诊断需求；此配置项应与其他诊断服务配置协同工作，避免配置冲突；AUTOSAR CP 4.4标准中可能对事件类型、响应行为和优先级等属性有具体的规定，需要遵守这些规定以确保兼容性。|
|说明|The PDU referenced by this transmission channel can produce meta data items of type TARGET_ADDRESS_16 and SOURCE_ADDRESS_16.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDslRoeTxConfirmationPduId|
|描述|Identifier of the PDU that is used by the lower level module for transmission confirmation of responses on this connection.|
|描述|概述：DcmDslRoeTxConfirmationPduId配置项用于定义诊断通信层中，用于发送响应事件报告（Response On Event, ROE）的确认消息的PDU（协议数据单元）标识符。|
|描述|注意：在配置DcmDslRoeTxConfirmationPduId时，需要确保所指定的PDU ID与系统中定义的PDU ID一致，并且与其他服务或功能使用的PDU ID不冲突；此配置项通常与Dcm配置中的网络层PDU ID相关联，需要根据网络管理策略和PDU路由信息进行正确配置；在AUTOSAR CP 4.4标准中，确保该配置项的使用符合诊断服务的规范要求，以保证ROE服务的正确实现和响应。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDslRoeTxPduRef|
|描述|Reference to a Pdu in EcuC that is used for this ResponseOnEvent transmission connection.|
|描述|概述：DcmDslRoeTxPduRef配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中响应输出事件（Response On Event）的传输协议数据单元（PDU）引用。|
|描述|注意：确保引用的PDU符合网络层的配置和要求；在配置时需注意PDU的传输能力是否满足响应事件的数据需求；此配置项应与网络管理配置紧密协调，以保证数据的正确传输和处理。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/EcuC/EcucConfigSet/EcucPduCollection/Pdu|

### 1.3. DcmDsp

|容器属性|值（容器）|
|---|---|
|名称|DcmDsp|
|描述|These parameters apply to Diagnostic Service Processing. There will always be one set of these parameters per Dcm.|
|描述|概述：DcmDsp配置项涉及诊断会话层的服务处理设置，用于定义诊断服务如何在不同诊断会话中被处理和执行。|
|描述|注意：在配置DcmDsp时，需确保诊断服务与会话控制策略相匹配，以避免在非法会话中执行服务；对于安全相关服务，还需考虑与安全访问级别的兼容性；AUTOSAR CP 4.4中可能增加了新的属性或服务，需要检查标准的最新版本以确保配置的兼容性。|
|说明|Please note: Although the multiplicity is set to 0..1. It can be expected that this container exists in any valid DCM configuration.|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDDDIDcheckPerSourceDID|
|描述|Defines the check for session, security and mode dependencies per source DIDs with a ReadDataByIdentifier (0x22).|
|描述|概述：DcmDspDDDIDcheckPerSourceDID配置项用于定义在动态数据诊断（Dynamic Data Definition, DDD）过程中，每个源数据标识符（Source DID）的访问权限检查策略。|
|描述|注意：在配置时需确保每个源DID的访问权限与系统安全策略一致；若系统中未使用DDD功能，则该配置项可忽略；AUTOSAR CP 4.4标准要求明确每个DID的安全访问级别，以防止未授权访问。|
|说明|true: Dcm module shall check the session, security and mode dependencies per source DIDs with a ReadDataByIdentifier (0x22) with DID in the range 0xF200 to 0xF3FF false: Dcm module shall not check the session, security and mode dependencies per source DIDs with a ReadDataByIdentifier (0x22) with DID in the range 0xF200 to 0xF3FF|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspEnableObdMirror|
|描述|DcmDspEnableObdMirror defines whether a DID inside the OBD range (F400-F4FF) and the OBD InfoType range (F800-F8FF) shall get the DID value as defined for OBD on reception of the UDS Service ReadDataByIdentifier (0x22), or not.|
|描述|概述：DcmDspEnableObdMirror配置项用于决定是否启用OBD镜像功能，该功能允许在车辆的OBD系统中复制和存储诊断信息，以便在需要时进行快速访问和检索。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保OBD镜像功能的使用符合相关法规要求；如果不需要此功能，应将其配置为禁用以节省资源；在实现时要注意数据的同步和一致性，避免数据冗余和不一致。|
|说明|It also defines whether a RID inside the OBD range (E000-E0FF) shall handle the RID as defined for OBD on reception of the UDS Service RoutineControl (0x31), or not.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspEnableSessionChangeCallback|
|描述|Enable callback to be called on diagnostic session state change.|
|描述|概述：DcmDspEnableSessionChangeCallback配置项用于定义诊断会话控制服务（Diagnostic Session Control service）在会话变更时是否调用特定的回调函数，以执行用户定义的操作。|
|描述|注意：在配置时需确保回调函数的实现与预期行为一致；此配置项对于实现会话管理逻辑特别重要；AUTOSAR CP 4.4标准中，确保该配置项的使用与系统需求相匹配，避免不必要的资源消耗。|
|说明|Enable callback to be called on diagnostic session state change.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspEnableEcuResetCallback|
|描述|Enable callback to be called on ecu reset change.|
|描述|概述：DcmDspEnableEcuResetCallback配置项用于定义在执行ECU重置服务（如UDS服务0x11）之前，是否需要调用一个特定的回调函数，以便执行一些特定的预处理操作。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保回调函数的实现不会导致重置的任何延迟或阻塞；如果不需要特定的预处理操作，可以不配置此项或将其设置为NULL；回调函数的设计应遵循AUTOSAR的编码规范，确保安全和效率。|
|说明|Enable callback to be called on ecu reset change.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDataDefaultEndianness|
|描述|Defines the default endianness belonging to a DID, RID or PID if the corresponding data does not define an endianness.|
|描述|概述：DcmDspDataDefaultEndianness配置项用于定义诊断服务处理数据时的默认字节序（Endianness），确保数据的一致性和正确解释，特别是在跨平台通信中。|
|描述|注意：在AUTOSAR CP 4.4中，必须明确指定每个诊断数据元素的字节序；如果未指定，则使用此默认值；在多字节数据处理时，正确的字节序至关重要以避免数据解释错误。|
|多实例个数|1 - 1|
|默认值|OPAQUE|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspMaxDidToRead|
|描述|Indicates the maximum allowed DIDs in a single "ReadDataByIdentifier" request.|
|描述|概述：DcmDspMaxDidToRead配置项用于定义在一个读取数据标识符（ReadDataByIdentifier）服务请求中，诊断通信管理器（Diagnostic Communication Manager）可以处理的最大数据标识符（DID）数量。|
|描述|注意：该值必须根据ECU的处理能力和网络带宽来合理设置，以避免在执行读取DID请求时超出ECU的处理能力或造成网络拥堵；在AUTOSAR CP 4.4标准中，如果该值设置得过大，可能会违反响应时间要求或内存限制，因此需要仔细评估合适的值；在配置时，还需考虑与其他诊断服务的数据交互和对应的资源分配。|
|多实例个数|0 - 1|
|默认值|1|
|取值范围|1 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspMaxPeriodicDidToRead|
|描述|Indicates the maximum allowed periodicDIDs which can be read in a single "ReadDataByPeriodicIdentifier" request.|
|描述|概述：DcmDspMaxPeriodicDidToRead配置项用于指定诊断通信管理器（Diagnostic Communication Manager）在周期性数据标识符读取列表中能够管理的最大数据标识符数量。|
|描述|注意：该值应根据实际应用需求和系统资源合理配置；超出此数量的周期性数据标识符请求可能会被拒绝；在配置时需考虑ECU的内存和处理能力限制。|
|多实例个数|0 - 1|
|取值范围|1 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPowerDownTime|
|描述|This parameter indicates to the client the minimum time of the stand-by sequence the server will remain in the power-down sequence.|
|描述|概述：DcmDspPowerDownTime配置项用于定义诊断通信管理器（Diagnostic Communication Manager）在接收到车辆关闭信号后，等待进入节能模式前的时间。|
|描述|注意：该值应根据具体的车辆电源管理策略来配置；过短的时间可能导致在车辆关闭前未完成必要的诊断通信；过长的时间可能会导致不必要的电源消耗。|
|说明|The resolution of this parameter is one second per count. The following values are valid: 00 - FE hex: 0 - 254 s powerDownTime; FF hex: indicates a failure or time not available. This value needs to be defined by the integrator according to the ECU capabilities. This parameter has to be available if the service EcuReset, sub-service enableRapidPowerShutDown is configured.|
|多实例个数|0 - 1|
|取值范围|0 - 255|

#### 1.3.1. DcmDspAuthentication

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAuthentication|
|描述|This container contains the configuration for the UDS service Authentication (0x29).|
|描述|概述：DcmDspAuthentication配置项用于定义诊断会话控制中的安全访问认证机制，包括但不限于密钥长度、加密算法类型以及尝试次数等参数，以确保对车辆进行诊断操作时的数据安全。|
|描述|注意：在配置DcmDspAuthentication时，必须确保所选加密算法符合AUTOSAR CP 4.4标准和行业安全要求；密钥长度应根据最新的安全标准选择，避免使用过短的密钥；重试次数限制应合理设置，以防止暴力破解尝试。|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationDefaultSessionTimeOut|
|描述|Defines the number of seconds after which the Dcm makes a transition to deauthenticated state, in case of no active communication.|
|描述|概述：DcmDspAuthenticationDefaultSessionTimeOut配置项用于定义诊断会话控制中，默认的会话超时时间，这是在成功认证后，系统保持会话状态的最长时间。|
|描述|注意：该时间值需要根据实际应用场景合理设置，以避免过短导致频繁重新认证，或过长增加系统安全风险；在AUTOSAR CP 4.4中，确保该配置与系统的安全需求一致；不同的诊断会话类型可能需要不同的超时设置，应细致考虑。|
|多实例个数|0 - 1|
|取值范围|0 - Inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationDeauthenticatedRole|
|描述|Role used for service authentication verification in the deauthenticated state.|
|描述|概述：DcmDspAuthenticationDeauthenticatedRole配置项定义了在车辆诊断通信控制模块（Diagnostic Communication Manager）中，当用户未通过认证时所分配的安全访问级别。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该配置项与系统的安全策略一致；正确配置此项对于保护诊断服务免受未授权访问至关重要；在实施时需考虑与其他安全相关配置项的兼容性和一致性。|
|多实例个数|1 - 1|
|取值范围|1 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationGeneralNRC|
|描述|Defines the NRC that shall be send as replacement of all ISO 14229-1 defined NRCs in case of invalid certificate or content.|
|描述|概述：DcmDspAuthenticationGeneralNRC配置项用于定义在执行诊断会话控制、安全访问或其他服务时，如果客户端（通常是诊断工具）未能通过安全认证，则由诊断通信管理器（DCM）返回的负面响应代码（NRC）。|
|描述|注意：在配置DcmDspAuthenticationGeneralNRC时，需要确保所选的NRC符合ISO 14229标准中定义的错误代码；不同服务可能需要配置不同的NRC以满足特定的安全要求；AUTOSAR CP 4.4标准中并未对所有可能的NRC进行详细规定，因此在实施时需参考最新的ISO 14229文档。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationRoleSize|
|描述|Defines the size in bytes for the role element within a certificate.|
|描述|概述：DcmDspAuthenticationRoleSize定义了诊断会话控制中，用于身份认证的角色大小，即每个角色所需的数据长度。|
|描述|注意：该配置项的值应根据具体的安全访问需求来设置，确保足够的数据长度以支持不同的安全算法；过大的值可能会增加系统的内存消耗，而过小的值可能导致安全机制无法正常工作；在AUTOSAR CP 4.4标准中，需确保此配置与安全访问需求相匹配，但标准本身不限制具体的大小值。|
|多实例个数|1 - 1|
|取值范围|1 - 4|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListDIDMaxSize|
|描述|Defines the maximum size in bytes for the white list element within a certificate.|
|描述|概述：DcmDspAuthenticationWhiteListDIDMaxSize 定义了在诊断会话中，可以在不进行安全访问检查的情况下访问的数据标识符（DID）的最大数量。|
|描述|注意：此参数的设置应考虑系统的安全需求，避免设置过高，以免降低系统的安全性；应根据实际应用需求合理配置此值；在AUTOSAR CP 4.4标准中，确保此配置与安全策略和访问控制列表相匹配。|
|多实例个数|0 - 1|
|取值范围|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListMemorySelectionMaxSize|
|描述|Defines the maximum size in bytes for the white list element within a certificate.|
|描述|概述：DcmDspAuthenticationWhiteListMemorySelectionMaxSize配置项用于定义诊断服务中，认证过程允许的最大内存范围大小，以确保认证过程中的内存访问是受限制的。|
|描述|注意：在配置此参数时，需要确保其值不超过ECU内存管理的最大限制；此参数的设置应与实际的安全需求和ECU的内存容量相匹配；在AUTOSAR CP 4.4标准中，如果该配置项的属性与标准定义的属性不一致，需要检查并调整以确保符合标准要求。|
|多实例个数|0 - 1|
|取值范围|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListRIDMaxSize|
|描述|Defines the maximum size in bytes for the white list element within a certificate.|
|描述|概述：DcmDspAuthenticationWhiteListRIDMaxSize 定义了在诊断会话中，用于认证过程的最大请求标识符（RID）列表的大小。|
|描述|注意：此参数的设置应考虑系统的安全需求和资源限制；过大的列表可能会消耗额外的系统资源，影响性能；确保此参数的设置符合AUTOSAR CP 4.4的安全管理要求。|
|多实例个数|0 - 1|
|取值范围|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListServicesMaxSize|
|描述|Defines the maximum size in bytes for the white list element within a certificate.|
|描述|概述：DcmDspAuthenticationWhiteListServicesMaxSize配置项用于定义诊断服务中，允许在未进行安全访问认证的情况下执行的服务列表的最大尺寸。|
|描述|注意：在配置时需确保该值符合系统对安全性和资源限制的要求；超出此尺寸的服务将需要进行安全访问认证后才能执行；AUTOSAR CP 4.4标准中应检查此配置项是否存在版本特定的限制或变更。|
|多实例个数|0 - 1|
|取值范围|1 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationGeneralNRCModeRuleRef|
|描述|Mode rule that defines if the general NRC shall be send for all failures due to invalid certificate or content.|
|描述|概述：DcmDspAuthenticationGeneralNRCModeRuleRef配置项用于引用一个模式规则，该规则定义了在执行诊断会话控制（Diagnostic Session Control）时，如果认证（Authentication）服务不满足特定条件，应该返回的负响应代码（Negative Response Code, NRC）。|
|描述|注意：在配置DcmDspAuthenticationGeneralNRCModeRuleRef时，需要确保引用的模式规则与实际的诊断服务逻辑相匹配；如果配置的模式规则不存在或者不正确，可能会导致诊断服务在特定情况下无法正确返回NRC；AUTOSAR CP 4.4标准中对于NRC的使用有严格的规定，因此需要仔细检查配置以确保符合标准要求。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationPersistStateModeRuleRef|
|描述|References a mode rule that defines if the authentication state shall be persisted in non-volatile memory.|
|描述|概述：DcmDspAuthenticationPersistStateModeRuleRef配置项用于引用一个模式管理规则，该规则定义了诊断会话控制（Diagnostic Session Control）下，认证状态（Authentication state）的持久性行为。|
|描述|注意：在配置时，需要确保引用的模式管理规则与所需的认证状态持久性行为相匹配；此配置项对于实现会话控制逻辑至关重要，因此必须谨慎处理；AUTOSAR CP 4.4标准中，模式管理规则应当符合预定义的模式声明，以确保系统行为的一致性。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

##### 1.3.1.1. DcmDspAuthenticationConnection

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAuthenticationConnection|
|描述|This container contains the authentication configuration use for a dsl connection.|
|描述|概述：DcmDspAuthenticationConnection配置项用于定义诊断会话控制中，特定安全访问（Security Access）服务请求与ECU之间的认证连接参数。|
|描述|注意：在配置时需确保安全算法和密钥长度符合AUTOSAR CP 4.4标准要求；认证过程中的时间限制和尝试次数应合理设置，以防止恶意攻击；该配置项的设置应与ECU的安全策略紧密相关，确保系统的安全性。|
|多实例个数|0 - inf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationCertificatePublicKeyStoreJobRef|
|描述|Reference to a CsmJob used to store the public key within the Csm.|
|描述|概述：DcmDspAuthenticationCertificatePublicKeyStoreJobRef 是一个配置项，用于引用存储认证证书公钥的作业，这通常是诊断通信管理（Diagnostic Communication Manager）的一部分，用于处理安全相关的认证过程。|
|描述|注意：在配置DcmDspAuthenticationCertificatePublicKeyStoreJobRef时，需要确保引用的作业与实际的公钥存储作业相匹配；此配置项通常与车辆制造商的安全策略和诊断安全需求紧密相关；在实施时，应考虑与其他安全模块的接口和数据共享策略，以确保系统的整体安全性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationClientCertificateRef|
|描述|Reference to a KeyMCertificate used to handle the client certificate for this connection.|
|描述|概述：DcmDspAuthenticationClientCertificateRef配置项用于引用客户端证书，该证书在诊断通信安全中用于客户端认证过程，确保通信双方的身份可靠和数据的安全性。|
|描述|注意：在配置客户端证书引用时，需要确保引用的证书与系统中实际使用的证书相匹配；此外，应当注意证书的有效期和更新机制，以防止因过期或失效的证书导致认证失败；AUTOSAR CP 4.4标准中对于证书的格式和存储可能有具体要求，需要根据标准进行相应配置。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationClientChallengeSignJobRef|
|描述|Reference to a job used to sign the client challenge.|
|描述|概述：DcmDspAuthenticationClientChallengeSignJobRef 是一个配置项，用于引用执行客户端挑战签名任务的加密服务作业，这通常是在执行诊断认证过程中的一部分。|
|描述|注意：在配置DcmDspAuthenticationClientChallengeSignJobRef时，需要确保所引用的加密服务作业与实际的客户端挑战签名任务相匹配；此配置项必须指向有效的Crypto Service Job，否则认证过程可能无法正确执行；在AUTOSAR CP 4.4标准中，确保该配置项的使用与标准定义的服务作业管理机制兼容。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationConnectionCertificateRef|
|描述|Reference to a KeyMCertificate used to store the certificate within the KeyM.|
|描述|概述：DcmDspAuthenticationConnectionCertificateRef配置项用于引用在诊断通信过程中用于认证的连接证书，这是确保通信安全性的一部分。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保引用的证书与实际用于认证的证书相匹配；证书管理应遵循AUTOSAR的安全规范；在配置时需注意证书的有效性和更新机制。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationConnectionMainConnectionRef|
|描述|Reference to the dsl diagnostic connection that uses this authentication configuration.|
|描述|概述：DcmDspAuthenticationConnectionMainConnectionRef配置项用于引用诊断通信管理器（Diagnostic Communication Manager）中主连接的标识符，这是用于特定认证过程的诊断通信链路。|
|描述|注意：确保引用的连接标识符在系统中是存在且有效的；该配置项通常与安全访问服务相关，需要正确配置以保证安全性；在多连接环境中，应注意选择正确的主连接以避免认证过程中的通信问题。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsl/DcmDslProtocol/DcmDslProtocolRow/DcmDslConnection/DcmDslMainConnection|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationECUCertificateKeyElementRef|
|描述|Reference to a CryptoKeyElement used as server certificate during bi-directional authentication.|
|描述|概述：DcmDspAuthenticationECUCertificateKeyElementRef配置项用于引用存储在ECU中的证书或密钥元素，这些证书或密钥用于诊断服务中的安全认证过程。|
|描述|注意：在配置DcmDspAuthenticationECUCertificateKeyElementRef时，需要确保引用的证书或密钥元素在ECU中确实存在并且可用；此外，应当注意证书或密钥的格式和安全要求是否符合AUTOSAR CP 4.4标准；最后，确保认证过程中对证书或密钥的访问权限和保护措施得当，以防止潜在的安全风险。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Crypto/CryptoKeyElements/CryptoKeyElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationECUCertificateRef|
|描述|Reference to a KeyMCertificate with the server certificate for bi-directional authentication.|
|描述|概述：DcmDspAuthenticationECUCertificateRef配置项用于引用ECU证书，该证书通常用于诊断服务中的安全认证过程，以确保通信的安全性。|
|描述|注意：在配置DcmDspAuthenticationECUCertificateRef时，需要确保引用的证书符合ECU的安全要求和标准；此外，该引用应正确指向存储在ECU中的有效证书；在AUTOSAR CP 4.4中，应检查该配置项是否与最新的诊断安全标准保持一致。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmKeys/CsmKey|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationPublicKeyElementRef|
|描述|Reference to a certificate data element with the public key in the certificate.|
|描述|概述：DcmDspAuthenticationPublicKeyElementRef配置项用于引用存储在Crypto Certificate Manager中的公钥元素，该公钥用于诊断服务组件（Dcm）中的安全访问认证过程。|
|描述|注意：在配置DcmDspAuthenticationPublicKeyElementRef时，必须确保引用的公钥元素与所需的安全算法和认证过程相匹配；公钥元素的存储位置和格式应符合AUTOSAR的加密服务管理规范；在实际应用中，公钥的管理和更新需要遵循严格的安全策略，以防止未授权的访问或篡改。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationRandomJobRef|
|描述|Reference to a certificate parse job used to parse the authentication certificate.|
|描述|概述：DcmDspAuthenticationRandomJobRef配置项用于引用在诊断会话中用于认证的随机数生成作业，它是诊断安全访问服务的一部分，确保安全性要求得到满足。|
|描述|注意：在配置DcmDspAuthenticationRandomJobRef时，需要确保引用的作业符合AUTOSAR标准中定义的随机数生成机制；此配置项通常与安全算法和密钥管理模块紧密相关，因此需要与安全专家协作以确保正确实现；在不同的安全等级下，可能需要配置不同的随机数生成作业，因此应根据项目的安全需求进行配置。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationRoleElementRef|
|描述|Reference to a certificate data element with the role in the certificate.|
|描述|概述：DcmDspAuthenticationRoleElementRef配置项用于引用特定的安全访问角色元素，它定义了诊断会话控制（Diagnostic Session Control）中安全访问（Security Access）服务所需的认证和授权级别。|
|描述|注意：在配置DcmDspAuthenticationRoleElementRef时，需要确保引用的安全访问角色元素在系统中是存在且有效的；此外，应当注意角色元素与所需安全级别之间的匹配关系，以确保正确的访问控制；AUTOSAR CP 4.4标准中对安全访问的配置可能有特定的要求和限制，需要遵守这些规范以保证系统的安全性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationTargetIdentificationModeRuleRef|
|描述|Reference to a mode rule that is used to evaluate the target identification.|
|描述|概述：DcmDspAuthenticationTargetIdentificationModeRuleRef配置项用于定义诊断会话控制（Diagnostic Session Control）中，针对特定诊断请求的认证和授权过程中，目标识别模式的规则引用。|
|描述|注意：此配置项要求与安全访问（Security Access）服务的配置紧密协调，确保诊断安全级别和目标识别模式的一致性；在配置时需确保引用的规则与实际的安全策略相匹配，避免安全漏洞；AUTOSAR CP 4.4标准中对此配置项的具体要求可能与早期版本有所不同，需要仔细核对标准文档。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationVerifyProofOfOwnerShipClientJobRef|
|描述|Reference to a CsmJob used to verify the proof of ownership client in the Csm.|
|描述|概述：DcmDspAuthenticationVerifyProofOfOwnerShipClientJobRef 是用于引用执行车辆所有权证明验证的客户端服务作业的配置项，它确保了诊断通信管理器（Dcm）在进行安全访问时能够正确调用相关的服务作业。|
|描述|注意：在配置时需确保引用的客户端服务作业与实际实现的认证机制相匹配；若该配置项引用错误，可能会导致安全访问验证失败；AUTOSAR CP 4.4标准中应保持该配置项与相关的认证服务作业之间的一致性和正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Csm/CsmJobs/CsmJob|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListDIDElementRef|
|描述|Reference to a certificate data element with the white list for data identifiers in the certificate.|
|描述|概述：DcmDspAuthenticationWhiteListDIDElementRef配置项用于指定在执行诊断会话控制或安全访问服务时，不需要进行安全访问认证的数据标识符（DID）列表。|
|描述|注意：在配置此项时，确保只有那些确实不需要安全保护的DID被列入白名单；不恰当的配置可能会导致安全风险；AUTOSAR CP 4.4标准中应当有明确的定义和限制关于哪些DID可以被包含在白名单中。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListMemorySelectionElementRef|
|描述|Reference to a certificate data element with the white list for user defined memory selection in the certificate.|
|描述|概述：DcmDspAuthenticationWhiteListMemorySelectionElementRef配置项用于定义诊断服务中，哪些内存区域可以在没有进行安全访问认证的情况下被访问，以支持特定的诊断需求。|
|描述|注意：在配置时需确保所选内存区域的访问不会影响系统的安全性和稳定性；该配置项在AUTOSAR CP 4.4中可能没有直接对应，需要通过安全访问配置来间接实现；正确配置白名单内存区域对于避免潜在的安全风险至关重要。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListRIDElementRef|
|描述|Reference to a certificate data element with the white list for routine identifiers in the certificate.|
|描述|概述：DcmDspAuthenticationWhiteListRIDElementRef 是用于定义在诊断会话中，哪些诊断请求标识符（RID）可以在没有安全访问（即不需要进行安全认证）的情况下被执行。|
|描述|注意：此配置项应谨慎使用，以避免安全漏洞；确保只有非敏感操作被列入白名单；AUTOSAR CP 4.4标准中未明确提及此配置项，可能属于特定实现或扩展。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAuthenticationWhiteListServicesElementRef|
|描述|Reference to a certificate data element with the white list in the certificate.|
|描述|概述：DcmDspAuthenticationWhiteListServicesElementRef配置项用于定义在执行诊断会话控制时，不需要进行安全访问认证的服务列表。|
|描述|注意：在配置此项时，必须确保只有那些不影响车辆安全和安全性的服务被列入白名单；应遵循相关的法规和标准，确保不会因为绕过安全认证而暴露敏感操作；在AUTOSAR CP 4.4标准中，应正确使用引用机制来指向具体的服务，以保证配置的一致性和正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

#### 1.3.2. DcmDspClearDTC

|容器属性|值（容器）|
|---|---|
|名称|DcmDspClearDTC|
|描述|This container contains the configuration for the Clear DTC service.|
|描述|概述：DcmDspClearDTC是一个配置参数，用于定义诊断通信管理器（Diagnostic Communication Manager）中的DTC（Diagnostic Trouble Code）清除服务的行为和属性，包括清除DTC的范围和条件。|
|描述|注意：在配置DcmDspClearDTC时，需要确保它符合车辆制造商的诊断策略和法规要求；此外，应注意与其他诊断服务的交互，以及在不同诊断会话控制下的DTC清除权限。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspClearDTCCheckFnc|
|描述|Callback function for condition check, manufacturer / supplier specific checks on the groupOfDTC, which is requested to clear.|
|描述|概述：DcmDspClearDTCCheckFnc配置项用于定义一个函数，该函数在执行故障码清除（Clear Diagnostic Trouble Codes, DTCs）操作之前被调用，以检查是否满足清除DTC的条件。|
|描述|注意：在配置DcmDspClearDTCCheckFnc时，需要确保所引用的函数符合AUTOSAR标准中对该函数的定义和要求；该函数的实现应当仅检查清除DTC的条件，而不执行其他诊断服务或副作用；在设计该函数时，应考虑到车辆状态和安全要求，确保在适当的条件下才允许清除DTC。|
|说明|This parameter is related to the interface : Xxx_ClearDTCCheckFnc.|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspClearDTCModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspClearDTCModeRuleRef配置项用于定义诊断服务中清除故障码（DTC）操作的模式规则引用，指定在何种条件下允许执行清除DTC的操作。|
|描述|注意：确保引用的模式规则与实际的诊断需求相匹配，避免因规则设置不当导致清除DTC操作无法按预期执行；在配置时需考虑车辆的安全和诊断策略，确保不会误清除关键故障码；AUTOSAR CP 4.4标准中，对于DcmDspClearDTCModeRuleRef的具体实现细节和限制可能有更新，建议参考最新的AUTOSAR文档。|
|说明|Mode rule which controls to clear the DTCs. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

#### 1.3.3. DcmDspComControl

|容器属性|值（容器）|
|---|---|
|名称|DcmDspComControl|
|描述|Provides the configuration of the CommunicationControl mechanism.|
|描述|概述：DcmDspComControl配置项是用于定义诊断通信控制服务（Diagnostic Communication Manager Service）的参数，它允许控制ECU（电子控制单元）的通信能力，例如开启或关闭ECU的网络通信。|
|描述|注意：在配置DcmDspComControl时，需要确保与ECU支持的诊断服务和安全级别相匹配；此外，应考虑与其他诊断服务的交互和对车辆网络的影响；AUTOSAR CP 4.4标准中可能对该服务的实现和配置有具体的要求和限制，需要遵循这些规范来确保兼容性和正确性。|
|多实例个数|0 - 1|

##### 1.3.3.1. DcmDspComControlAllChannel

|容器属性|值（容器）|
|---|---|
|名称|DcmDspComControlAllChannel|
|描述|Collection of ComM channels which shall be controlled if all networks are addressed.|
|描述|概述：DcmDspComControlAllChannel 是一个配置项，用于定义诊断通信管理（Diagnostic Communication Manager）中是否允许对所有通信通道执行通信控制。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保Dcm模块配置与通信堆栈的其他部分兼容；如果不需要对所有通道执行通信控制，应避免启用此配置以节省资源；此配置项的使用应符合车辆制造商的诊断策略和安全要求。|
|多实例个数|0 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspComControlAllChannelUsed|
|描述|Allow to activate or deactivate the usage of a ComM channel collection to be controlled, for multi purpose ECUs|
|描述|概述：DcmDspComControlAllChannelUsed配置项用于指定在执行通信控制服务时，是否允许控制所有通信通道。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项确保了诊断通信控制服务（Service 0x28）能够按需控制单个或所有通信通道；若设置为允许，需确保系统设计能够安全地处理对所有通道的控制；不正确的配置可能导致通信中断或系统行为不稳定。|
|说明|true = ComM channel collection used false = ComM channel collection not used|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspAllComMChannelRef|
|描述|Reference to ComM channel.|
|描述|概述：DcmDspAllComMChannelRef配置项用于引用诊断通信管理器（Diagnostic Communication Manager）中所有通信通道的标识符，这些通道在执行诊断会话控制时需要被管理。|
|描述|注意：在配置DcmDspAllComMChannelRef时，需要确保引用的ComM通道标识符与实际的通信通道配置相匹配；此配置项对于确保在不同诊断会话中正确管理通信通道至关重要；在AUTOSAR CP 4.4标准中，应当遵循相关的模块间接口定义和引用机制。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

##### 1.3.3.2. DcmDspComControlSetting

|容器属性|值（容器）|
|---|---|
|名称|DcmDspComControlSetting|
|描述|Provide the configuration of the Communication control.|
|描述|概述：DcmDspComControlSetting 用于定义诊断通信控制模块的设置，包括启用或禁用网络通信控制功能。|
|描述|注意：在配置DcmDspComControlSetting时，必须确保与车辆的网络管理策略一致；此配置项应根据具体的车辆网络需求和诊断需求进行调整；不正确的设置可能导致网络通信异常或诊断功能不可用。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspComControlCommunicationReEnableModeRuleRef|
|描述|Reference to DcmModeRule Mode rule which controls re-enabling|
|描述|概述：DcmDspComControlCommunicationReEnableModeRuleRef配置项用于引用一个定义了通信控制器重新启用模式的规则，这个规则指定了在执行诊断通信控制时，通信通道如何被重新启用。|
|描述|注意：确保引用的模式规则与实际的通信控制需求相匹配；在配置时要注意引用的模式规则必须已在系统中定义；在多通道通信系统中，要确保每个通道的重新启用规则正确配置，以避免通信混乱。|
|说明|of communication by DCM. [ref. SWS_Dcm_00753]|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

##### 1.3.3.3. DcmDspComControlSpecificChannel

|容器属性|值（容器）|
|---|---|
|名称|DcmDspComControlSpecificChannel|
|描述|Assigns subnet number to ComM channel which will be controlled.|
|描述|概述：DcmDspComControlSpecificChannel配置项用于定义诊断服务组件（Dcm）中，通信控制服务（Communication Control, 0x28）针对特定通信通道的控制属性和行为。|
|描述|注意：在配置时需确保通道标识符与实际系统中的通信通道相匹配；该配置项在AUTOSAR CP 4.4中要求明确支持网络管理控制器的能力，如果系统不支持，应在设计时予以考虑；配置应遵循ECU支持的通信协议和标准，确保兼容性和协议一致性。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspComControlSpecificChannelUsed|
|描述|Allow to activate or deactivate the usage of a Subnet assigned to the ComM channel which will be controlled, for multi purpose ECUs.|
|描述|概述：DcmDspComControlSpecificChannelUsed配置项用于指定诊断服务是否允许对特定的通信通道进行控制，这有助于在执行诊断会话时，根据需要启用或禁用特定的通信路径。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用此配置项时，已经明确了哪些通信通道可以被控制，以避免对系统通信造成意外的干扰；此配置项的使用应与车辆制造商的安全和诊断策略保持一致；在配置时，应详细考虑对通信通道控制的影响，确保不会影响到系统的正常运行和安全。|
|说明|true = Subnet used false = Subnet not used|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSubnetNumber|
|描述|Subnet Number which controls the specific ComMChannel.|
|描述|概述：DcmDspSubnetNumber配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中子网的数量，这有助于管理不同网络子集上的诊断通信。|
|描述|注意：在配置DcmDspSubnetNumber时，需要确保其值反映了实际网络拓扑中存在的子网数量；超出实际子网数量的配置可能会导致资源浪费；如果配置的子网数量少于实际存在的子网，可能会导致部分子网上的诊断请求无法得到处理。|
|多实例个数|1 - 1|
|取值范围|1 - 14|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspSpecificComMChannelRef|
|描述|Reference to ComM channel.|
|描述|概述：DcmDspSpecificComMChannelRef配置项用于指定诊断通信管理器（Diagnostic Communication Manager）中特定的通信通道引用，以便于Dcm模块控制特定通道的通信状态。|
|描述|注意：在配置DcmDspSpecificComMChannelRef时，需要确保引用的ComM通道已经在系统中定义并且有效；此配置项通常与车辆网络相关的诊断功能紧密相关，因此需要根据网络架构和诊断需求谨慎配置；在AUTOSAR CP 4.4标准中，应当遵循相关的模块间接口定义和配置规则，以确保模块间的兼容性和通信的正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

##### 1.3.3.4. DcmDspComControlSubNode

|容器属性|值（容器）|
|---|---|
|名称|DcmDspComControlSubNode|
|描述|This container gives information about the node identification number and the ComM channel used to address a sub-network.|
|描述|概述：DcmDspComControlSubNode配置项用于定义诊断通信控制服务（Diagnostic Communication Manager Service）中子节点的通信控制选项，它指定了哪些网络节点（ECUs）的通信可以被控制。|
|描述|注意：在配置DcmDspComControlSubNode时，需要确保子节点的标识符与实际网络中的ECU标识符相匹配；此配置项通常与车辆网络拓扑结构和诊断需求紧密相关，因此需要根据具体的车辆网络设计来进行配置；在AUTOSAR CP 4.4标准中，应当遵循相关的诊断服务规范来确保通信控制的正确实施。|
|多实例个数|0 - 65535|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspComControlSubNodeUsed|
|描述|This parameter determines if a node control function is available or not.|
|描述|概述：DcmDspComControlSubNodeUsed 是一个配置项，用于指定是否在诊断通信控制（Dcm）服务中使用子节点控制。|
|描述|注意：在AUTOSAR CP 4.4标准中，如果项目需要支持对网络中的子节点（如网关下的各个ECU）进行通信控制，则应启用此配置项；如果不需要子节点控制功能，该配置项应设置为不启用以节省资源；在配置时需要确保与项目需求和网络架构相匹配。|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspComControlSubNodeId|
|描述|The node identification number DcmDspComControlSubNodeId is addressed by the CommunicationControl (0x28) request.|
|描述|概述：DcmDspComControlSubNodeId配置项用于定义诊断通信控制服务（Diagnostic Communication Manager Service Processor）中子网络的标识符，这有助于管理不同子网络上的通信控制。|
|描述|注意：在配置DcmDspComControlSubNodeId时，需要确保子网络标识符的唯一性，以避免在诊断会话中的冲突；此外，标识符应与实际网络结构相对应，确保正确的通信控制；在AUTOSAR CP 4.4标准中，如果子网络的概念被用于项目中，该配置项应当与网络管理配置紧密协调。|
|多实例个数|1 - 1|
|取值范围|1 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspComControlSubNodeComMChannelRef|
|描述|This parameter references a ComM channel where this node is connected to.|
|描述|概述：DcmDspComControlSubNodeComMChannelRef配置项用于定义诊断服务组件（Dcm）中，特定子节点与通信管理（ComM）通道的关联，以便控制网络通信状态。|
|描述|注意：确保引用的ComM通道与子节点兼容；在配置时需注意AUTOSAR版本对ComM通道引用的具体要求可能有所不同；此配置项对于实现网络管理和诊断通信控制功能至关重要。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/ComM/ComMConfigSet/ComMChannel|

#### 1.3.4. DcmDspCommonAuthorization

|容器属性|值（容器）|
|---|---|
|名称|DcmDspCommonAuthorization|
|描述|This container contains the configuration (parameters) for the common Authorization being equal for several services / sub-services.|
|描述|概述：DcmDspCommonAuthorization配置项用于定义诊断服务的授权级别，它规定了访问不同诊断服务时所需的安全级别，以确保只有授权用户可以执行特定的诊断操作。|
|描述|注意：在配置DcmDspCommonAuthorization时，需要确保授权级别与实际的安全需求相匹配；此外，应注意与Dcm的安全策略和密钥管理机制的兼容性；在AUTOSAR CP 4.4标准中，应遵循相关的模块和服务的安全规范。|
|多实例个数|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspCommonAuthorizationModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspCommonAuthorizationModeRuleRef配置项用于引用一个授权模式规则，该规则定义了对诊断服务请求的访问权限控制，以确保只有授权的用户可以访问特定的诊断服务。|
|描述|注意：在配置时需确保引用的授权模式规则已经定义且有效；授权模式规则的配置应与系统的安全需求相匹配，以防未授权访问；AUTOSAR CP 4.4中，对授权模式的支持和实现细节可能有所不同，需要参考具体的AUTOSAR文档。|
|说明|Mode rule which controls this service/ sub-service. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspCommonAuthorizationSecurityLevelRef|
|描述|Reference to DcmDspSecurityRow|
|描述|概述：DcmDspCommonAuthorizationSecurityLevelRef配置项用于引用在诊断服务处理期间需要的安全等级，它定义了访问特定诊断服务时所需的安全授权级别。|
|描述|注意：在配置时需确保引用的安全等级与实际实现的安全策略相匹配；若引用了不存在的安全等级，可能导致诊断服务无法正确执行；在多安全等级的系统中，正确管理和配置每个服务的安全等级至关重要。|
|说明|Security levels allowed to control this service/ sub-service. If there is no reference, no check of security level shall be done.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspCommonAuthorizationSessionRef|
|描述|Reference to DcmDspSessionRow|
|描述|概述：DcmDspCommonAuthorizationSessionRef配置项用于定义诊断服务组件（Diagnostic Service Component）在执行特定服务前所需的会话控制权限，确保只有在适当的会话级别下才能访问和执行特定的诊断服务。|
|描述|注意：该配置项需要与会话控制管理模块的会话级别定义保持一致；确保为每个需要会话控制的诊断服务正确配置会话级别；不正确的会话级别配置可能导致诊断服务无法在预期的会话中执行。|
|说明|Sessions allowed to control this service/ sub-service. If there is no reference, no check of session level shall be done.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspCommonAuthorizationVehicleSystemGroupRef|
|描述|Defines RID availability dependency to a specific VSG|
|描述|概述：DcmDspCommonAuthorizationVehicleSystemGroupRef 用于定义诊断会话控制中，特定车辆系统组的访问权限引用。|
|描述|注意：确保引用的车辆系统组在系统中已定义且有效；此配置项对安全性要求高，应仔细管理权限设置；在AUTOSAR CP 4.4中，此配置项的使用应符合最新的安全和诊断标准。|
|说明|VSGs allowed to control this service/ sub-service. If there is no reference, no check of vsg shall be done.|
|多实例个数|0 - 255|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspVehicleSystemGroup/DcmDspVehicleSystemGroupRow|

#### 1.3.5. DcmDspControlDTCSetting

|容器属性|值（容器）|
|---|---|
|名称|DcmDspControlDTCSetting|
|描述|Provide the configuration of the ControlDTCSetting mechanism.|
|描述|概述：DcmDspControlDTCSetting配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，控制诊断故障码（DTC）设置的行为和属性，如启用或禁用DTC的存储。|
|描述|注意事项：在配置DcmDspControlDTCSetting时，需确保与车辆制造商的诊断策略一致；此配置项对故障诊断和后续的故障处理流程有重要影响；AUTOSAR CP 4.4标准中，对DTC控制的具体实现细节有明确规范，需遵守这些规范以保证兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmSupportDTCSettingControlOptionRecord|
|描述|This configuration switch defines if the DTCSettingControlOptionRecord is in general supported in the request message or not.|
|描述|概述：DcmSupportDTCSettingControlOptionRecord配置项用于定义诊断通信管理器（Diagnostic Communication Manager）是否支持故障码设置控制选项记录功能，这是一个用于控制故障诊断记录开启或关闭的功能。|
|描述|注意：在配置Dcm模块时，需要根据项目需求决定是否启用此功能；如果启用，需确保与故障管理模块的交互被正确实现；在不同地区的法规要求可能不同，需要根据目标市场的法规要求来配置此项。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspControlDTCSettingReEnableModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspControlDTCSettingReEnableModeRuleRef配置项用于引用诊断服务组件中控制DTC设置的重新启用模式规则，这决定了在何种条件下可以重新启用DTC记录。|
|描述|注意：确保引用的模式规则与实际的诊断需求和法规要求相匹配；在配置时应参照相关的诊断需求文档；在AUTOSAR CP 4.4标准中，应保证该引用的模式规则在系统中是存在且有效的。|
|说明|Mode rule which controls re-enabling of controlDTCsetting by DCM. The DCM module shall execute a ControlDTCSetting.Off (call Dem_EnableDTCSetting()) in case that the referenced mode rule is not fulfilled anymore.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

#### 1.3.6. DcmDspData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspData|
|描述|This container contains the configuration (parameters) of a Data belonging to a DID|
|描述|概述：DcmDspData配置项用于定义诊断服务处理模块中的数据属性，如数据标识符和数据类型，以便正确处理来自诊断工具的请求。|
|描述|注意：确保数据标识符的唯一性和与标准诊断数据标识符的一致性；数据类型应符合AUTOSAR CP 4.4标准中定义的类型；在配置时需考虑数据的安全性和访问权限控制。|
|多实例个数|0 - inf|

|配置项属性|值（添加信息参数配置项）|
|---|---|
|名称|DcmDspOdxDataDescription|
|描述|Defines additional description for ODX documentation|
|描述|概述：DcmDspOdxDataDescription配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，ODX（Open Diagnostic data eXchange）文件中的数据描述，这些描述包括用于车辆诊断的数据结构和参数。|
|描述|注意：在AUTOSAR CP 4.4中，确保ODX文件与Dcm模块的配置保持一致；ODX数据描述应符合ISO 22901-1标准；在实施时，应注意数据描述的精确性和兼容性，以确保诊断服务的正确性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDataConditionCheckReadFncUsed|
|描述|This parameter determines if a condition check function is available or not.|
|描述|概述：DcmDspDataConditionCheckReadFncUsed 是一个配置项，用于指定是否使用了数据条件检查读取功能，这是诊断通信管理器（Diagnostic Communication Manager）的一部分，用于在读取数据之前检查是否满足特定条件。|
|描述|注意：在AUTOSAR CP 4.4标准中，该配置项应当与实际实现的功能相匹配；如果未实现数据条件检查功能，则该配置项应设置为false；如果实现了该功能，确保相关函数的正确实现和配置。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDataEndianness|
|描述|Defines the endianness of the data belonging to a DID in a diagnostic request or response message.|
|描述|概述：DcmDspDataEndianness配置项用于定义诊断服务处理数据时所采用的字节序，确保数据的正确解析和编码，可以是大端（Big Endian）或小端（Little Endian）。|
|描述|注意：在配置DcmDspDataEndianness时，需要确保它与ECU中数据的实际存储格式一致；不正确的字节序配置可能导致诊断响应错误或数据解析失败；AUTOSAR CP 4.4标准中，该配置项应与ECU的硬件架构和编译器设置保持一致。|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDataType|
|描述|Provide the implementation data type of data belonging to a DID.|
|描述|概述：DcmDspDataType配置项用于定义诊断服务处理器（Diagnostic Service Processor）中使用的数据类型，这些数据类型用于读取或写入数据时与ECU内部数据类型的映射。|
|描述|注意：在配置DcmDspDataType时，需要确保数据类型的定义与ECU支持的实际数据类型相匹配；此外，应注意数据类型的大小、符号性以及字节序（大端或小端）是否符合ECU的硬件架构和应用需求；在AUTOSAR CP 4.4标准中，数据类型的配置应遵循标准规定的数据类型模板。|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDataUsePort|
|描述|Defines which interface shall be used to access the data.|
|描述|概述：DcmDspDataUsePort配置项指定了诊断服务组件（Diagnostic Service Component）如何访问车辆数据，即通过哪种端口（Sender-Receiver或Client-Server）与其他软件组件交互以获取或设置数据。|
|描述|注意：在AUTOSAR CP 4.4中，确保选择的端口类型与所需的数据交互模式兼容；配置时需考虑数据的实时性要求和安全性要求；不同的端口类型可能会影响系统的响应时间和资源占用。|
|多实例个数|1 - 1|
|默认值|USE_DATA_ASYNCH_CLIENT_SERVER|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataConditionCheckReadFnc|
|描述|Function name to demand application if the conditions (e.g. System state) to read the DID are correct. (ConditionCheckRead-function).|
|描述|概述：DcmDspDataConditionCheckReadFnc配置项用于定义一个函数，该函数在读取诊断数据之前执行，用于检查是否满足读取条件。|
|描述|注意：该函数应返回一个标准的Dcm_ReturnReadDataConditionCheckType枚举值，以指示读取条件是否满足；如果读取条件不满足，应阻止数据的读取并返回相应的错误码；确保该函数的实现与系统的安全和权限管理策略一致。|
|说明|Multiplicity shall be equal to parameter DcmDspDataReadFnc. This parameter is related to the interface Xxx_ConditionCheckRead.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataEcuSignal|
|描述|Function name to control the access to a certain ECU Signal by the DCM. (IoHwAb_Dcm_\<symbolic name of ECU signal\>-function).|
|描述|概述：DcmDspDataEcuSignal配置项用于定义诊断服务中与ECU信号相关的数据，它指定了如何从ECU中读取或向ECU写入数据。|
|描述|注意：在配置DcmDspDataEcuSignal时，需要确保引用的数据标识符与ECU中实际的信号匹配；此外，还需注意数据的读写权限和安全访问条件是否符合要求；在配置数据信号时，还应考虑数据的格式和长度是否符合诊断标准和ECU的实际处理能力。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataFreezeCurrentStateFnc|
|描述|Function name to request to application to freeze the current state of an IOControl. (FreezeCurrentState-function).|
|描述|概述：DcmDspDataFreezeCurrentStateFnc是一个配置项，用于定义诊断服务组件（Diagnostic Communication Manager）中的数据服务处理函数，该函数用于冻结当前的数据状态，通常与诊断服务如读取冻结帧数据相关。|
|描述|注意：在配置DcmDspDataFreezeCurrentStateFnc时，需要确保该函数与实际的数据冻结需求相匹配，并且符合ECU的硬件和软件能力；该函数的实现必须满足AUTOSAR标准中对诊断服务的要求；在实现时应注意资源的同步和互斥，避免在多任务环境下的数据一致性问题。|
|说明|This parameter is related to the interface Xxx_FreezeCurrentState.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataGetScalingInfoFnc|
|描述|Function name to request to application the scaling information of the DID. (GetScalingInformation-function).|
|描述|概述：DcmDspDataGetScalingInfoFnc是一个配置项，用于指定一个函数，该函数由诊断通信管理器（Diagnostic Communication Manager）调用，以获取数据标识符（Data Identifier, DID）的缩放信息。|
|描述|注意：在配置DcmDspDataGetScalingInfoFnc时，需要确保所引用的函数符合AUTOSAR标准中定义的原型和行为要求；此函数通常与DID相关联，因此必须确保DID配置正确；在实现时，应注意缩放信息的准确性和与DID的一致性。|
|说明|This parameter is related to the interface Xxxx_GetScalingInformation.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataReadDataLengthFnc|
|描述|Function name to request from application the data length of a DID. (ReadDataLength-function).|
|描述|概述：DcmDspDataReadDataLengthFnc配置项用于定义一个函数，该函数负责返回诊断服务中特定数据标识符（DID）的数据长度，确保数据交换的准确性和有效性。|
|描述|注意：在实现该函数时，需要确保返回的数据长度准确反映了对应DID的实际数据大小；对于可变长度的DID，该函数实现应能动态计算并返回正确的长度；在AUTOSAR CP 4.4标准中，该配置项的命名和功能需遵循规范，以保证诊断服务的兼容性和互操作性。|
|说明|This parameter is related to the interface Xxx_ReadDataLength.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataReadEcuSignal|
|描述|Function name for read access to a certain ECU Signal by the DCM. (IoHwAb_Dcm_Read\<EcuSignalName\>-function).|
|描述|概述：DcmDspDataReadEcuSignal 用于定义诊断服务组件中，从ECU读取信号的配置和行为。|
|描述|注意：确保配置的信号与ECU支持的信号匹配；在配置时应注意数据的安全性和访问权限；此配置项应与ECU的实际硬件和软件能力相一致。|
|说明|Only relevant if DcmDspDataUsePort==USE_ECU_SIGNAL.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataReadFnc|
|描述|Function name to request from application the data value of a DID.|
|描述|概述：DcmDspDataReadFnc配置项指定了用于读取诊断数据的函数，这是在诊断服务中用于获取ECU内部数据的函数指针。|
|描述|注意：确保该函数与实际的数据读取逻辑相匹配，以保证诊断服务的正确执行；在配置时需注意函数的返回类型和参数列表与AUTOSAR标准的一致性；对于不同的数据项可能需要配置不同的读取函数。|
|说明|(ReadData-function). This parameter is related to the interface Xxx_ReadData.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataResetToDefaultFnc|
|描述|Function name to request to application to reset an IOControl to default value. (ResetToDefault-function).|
|描述|概述：DcmDspDataResetToDefaultFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，特定数据元素重置为默认值时所调用的函数。|
|描述|注意：该函数需要确保能够将数据安全地重置为出厂设置或预定义的默认状态；在实现时需考虑数据重置过程中可能对系统其他部分产生的影响；根据AUTOSAR CP 4.4标准，确保该函数符合诊断服务的安全和权限要求。|
|说明|This parameter is related to the interface Xxx_ResetToDefault.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataReturnControlToEcuFnc|
|描述|Function name to request to application to return control to ECU of an IOControl. (ReturnControlToECU-function).|
|描述|概述：DcmDspDataReturnControlToEcuFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，执行"返回控制权给ECU"操作的函数指针，该操作是服务0x31（写数据或调整参数）的一部分。|
|描述|注意：在配置该函数指针时，确保所引用的函数与AUTOSAR标准中定义的原型一致；函数实现应确保能够将数据项的控制权从诊断工具返回给ECU；在多ECU系统中，应确保该函数能够正确区分并作用于目标ECU。|
|说明|This parameter is related to the interface Xxx_ReturnControlToECU.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataShortTermAdjustmentFnc|
|描述|Function name to request to application to adjust the IO signal. (ShortTermAdjustment-function).|
|描述|概述：DcmDspDataShortTermAdjustmentFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，短期调整数据的函数名称，该函数用于处理来自诊断测试仪的调整请求。|
|描述|注意：函数名称应遵循C语言命名规则，避免与其他函数名冲突；确保该函数实现符合AUTOSAR标准中对短期调整的要求；在配置时需注意与Dcm配置的其他部分的一致性，如数据标识符和服务标识符的匹配。|
|说明|This parameter is related to the interface Xxx_ShortTermAdjustment.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDataWriteFnc|
|描述|Function name to request application to write the data value of a DID. (WriteData-function).|
|描述|概述：DcmDspDataWriteFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，用于写入数据到ECU的函数指针。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该函数指针指向的函数遵循了标准的API原型；该函数通常与DcmDspData元素相关联，需要确保数据一致性和安全性；在实现时，应考虑对写入操作的权限管理和错误处理。|
|说明|This parameter is related to the interface Xxx_WriteData.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDataByteSize|
|描述|Defines the array length in bytes or the the maximum array length for variable datalengths.|
|描述|概述：DcmDspDataByteSize配置项用于定义诊断服务处理中，数据元素的大小，即数据元素占用的字节数。|
|描述|注意：在配置DcmDspDataByteSize时，需要确保其值与实际数据元素的大小相匹配；超出有效范围的配置可能导致数据处理错误；AUTOSAR CP 4.4标准中可能有特定的限制或要求，需要遵守这些规范以确保兼容性。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDataBlockIdRef|
|描述|NRAM blockId to access the data.|
|描述|概述：DcmDspDataBlockIdRef 用于引用诊断服务中的特定数据块标识符，该标识符用于访问或修改ECU中存储的数据。|
|描述|注意：确保引用的数据块标识符在整个诊断系统中是唯一的；在配置时应关联正确的数据块以避免数据错误；在AUTOSAR CP 4.4中，对数据块的访问权限和安全性要求应严格遵守。|
|说明|Only relevant if DcmDspDataUsePort==USE_BLOCK_ID.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/NvM/NvMBlockDescriptor|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDataInfoRef|
|描述|Reference to 1 DcmDspDataInfo|
|描述|概述：DcmDspDataInfoRef配置项用于引用数据元素的特定信息，这些信息定义了数据元素如何被诊断服务处理，包括读取和写入权限、安全访问级别等。|
|描述|注意：确保引用的数据信息与实际的诊断需求相匹配，避免权限不足或过高；在配置时需注意数据信息的兼容性，确保其符合AUTOSAR CP 4.4标准；对于安全敏感的数据元素，应仔细配置安全访问级别，以防未授权访问。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDataInfo|

##### 1.3.6.1. DcmDspDiagnosisScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDiagnosisScaling|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

###### 1.3.6.1.1. DcmDspAlternativeDataInterface

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataInterface|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a VariableDataPrototoype in a DataInterface.|
|说明|Additionally a reference to PortInterfaceMapping can be defined which provide already the mapping rules between the VariableDataPrototoype in a DataInterface used by the software component (DcmDspExternalSRDataElementClass) and the intended Diagnosis Representation defined by DcmDataElement.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a VariableDataPrototoype in a DataInterface.|
|说明|The CompuMethod of the data type of the referenced VariableDataPrototype will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|VARIABLE-DATA-PROTOTYPE|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmPortInterfaceMapping|
|描述|Optional reference to PortInterfaceMapping which defines the mapping rules.|
|说明|The PortInterfaceMapping is used to get the DataPrototypeMapping that describes a conversion between the data prototype referenced by DcmDataElement and the data prototype referenced from DcmDspExternalSRDataElementClass.|
|多实例个数|0 - 1|
|目标类型|PORT-INTERFACE-MAPPING|

###### 1.3.6.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

####### 1.3.6.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

###### 1.3.6.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

##### 1.3.6.2. DcmDspExternalSRDataElementClass

|容器属性|值（容器）|
|---|---|
|名称|DcmDspExternalSRDataElementClass|
|描述|This container defines the source of data in a provided port which shall be read respectively the target of data in a required port which shall be written.|
|描述|概述：DcmDspExternalSRDataElementClass配置项用于定义诊断服务处理过程中，外部信号或数据元素的属性和行为，如数据大小、地址、读写权限等。|
|描述|注意：在配置时需确保数据元素的属性与实际应用中的数据类型和访问权限相匹配；对于敏感或安全相关的数据，应特别注意访问权限的设置；AUTOSAR CP 4.4标准中，对于数据元素的定义和使用有明确规范，需要遵循这些规范以保证诊断服务的正确实现。|
|说明|This container shall contain either one DcmSubElementInDataElementInstance OR DcmDataElementInstance OR DcmSubElementInImplDataElementInstance reference.|
|多实例个数|0 - 1|

###### 1.3.6.2.1. DcmDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmDataElementInstance|
|描述|Instance Reference to the primitive data in a port where the data element is typed with an ApplicationPrimitveDataType or an ImplementationDataType.|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmDataElementInstanceRef|
|描述|Instance Reference to the primitive or array data which shall be read or written.|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ApplicationPrimitiveDataType of category VALUE or BOOLEAN or ApplicationArrayDataType or if the AutosarDataPrototype is typed with a ImplementationDataType of category VALUE, ARRAY or TYPE_REFERENCE that in turn boils down to VALUE or ARRAY|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE|
|目标类型|AUTOSAR-DATA-PROTOTYPE|

###### 1.3.6.2.2. DcmSubElementInDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmSubElementInDataElementInstance|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port where the data element is typed with an ApplicationCompositeDataType.|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmSubElementInDataElementInstanceRef|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port which shall be read.|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ApplicationCompositeDataType.|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE AUTOSAR-DATA-PROTOTYPE APPLICATION-COMPOSITE-ELEMENT-DATA-PROTOTYPE\*|
|目标类型|APPLICATION-COMPOSITE-ELEMENT-DATA-PROTOTYPE|

###### 1.3.6.2.3. DcmSubElementInImplDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmSubElementInImplDataElementInstance|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port where the data element is typed with an ImplementationDataType.|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmSubElementInImplDataElementInstanceRef|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port which shall be read.|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ImplementationDataType of category STRUCTURE or ARRAY. Please note that in case of ARRAY the index attribute in the target reference has to be set to select a single array element.|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE AUTOSAR-DATA-PROTOTYPE IMPLEMENTATION-DATA-TYPE-ELEMENT\*|
|目标类型|IMPLEMENTATION-DATA-TYPE-ELEMENT|

##### 1.3.6.3. DcmDspDidDataSupportInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidDataSupportInfo|
|描述|This container defines the supported information.|
|描述|概述：DcmDspDidDataSupportInfo配置项用于定义诊断服务中数据标识符（DID）的支持信息，包括DID是否支持读取、写入、控制等操作。|
|描述|注意：在配置DcmDspDidDataSupportInfo时，需要确保所指定的DID与实际支持的诊断服务相匹配；对于不支持的操作，应明确标记以避免诊断工具误操作；AUTOSAR CP 4.4标准中对DID的操作权限有严格规定，需遵守相应的安全和权限要求。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidDataSupportInfoBit|
|描述|Referenced Bit of the SupportInfo|
|描述|概述：DcmDspDidDataSupportInfoBit配置项用于定义在诊断服务中，数据标识符（DID）的支持信息位，这通常用于指示某个DID是否支持读取、写入或控制操作。|
|描述|注意：在配置DcmDspDidDataSupportInfoBit时，需要确保它与DID支持的操作相匹配；此配置项的设置必须符合ISO 14229标准中定义的服务响应格式；在AUTOSAR CP 4.4中，如果此配置项的属性与标准不一致，可能会导致诊断通信不正确或不兼容。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidDataSupportInfoRef|
|描述|Reference to DcmDspDidSupportInfo|
|描述|概述：DcmDspDidDataSupportInfoRef 用于引用支持特定数据标识符（DID）的数据支持信息，这有助于诊断通信管理中数据的读取和编码过程。|
|描述|注意：确保引用的数据支持信息与DID匹配正确，以保证诊断功能的正确执行；在配置时应参考具体的DID和其数据结构要求；在AUTOSAR CP 4.4中，此配置项的使用应严格遵循标准定义的数据封装和访问规则。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDid/DcmDspDidSupportInfo|

#### 1.3.7. DcmDspDataInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDataInfo|
|描述|This container contains the configuration (parameters) of one Data.|
|描述|概述：DcmDspDataInfo 是用于定义诊断服务中数据元素的属性，如数据的安全访问级别和读写权限。|
|描述|注意：确保配置的安全访问级别符合系统的安全需求；读写权限应明确，避免数据访问冲突；在配置时应考虑数据的敏感性和保护需求。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDataScalingInfoSize|
|描述|If Scaling information service is available for this Data, it provides the size in bytes of the scaling information.|
|描述|概述：DcmDspDataScalingInfoSize配置项用于定义诊断服务中数据缩放信息的大小，这通常与数据参数的缩放比例有关，用于调整或转换数据值。|
|描述|注意：在配置数据缩放信息时，必须确保DcmDspDataScalingInfoSize的值与实际应用中使用的数据类型大小相匹配；此配置项的值应符合ECU支持的数据长度限制；在AUTOSAR CP 4.4标准中，如果数据缩放功能未被使用，该配置项可能不需要配置或者应设置为零。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 4294967295|

#### 1.3.8. DcmDspDid

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDid|
|描述|This container contains the configuration (parameters) of the DID.|
|描述|概述：DcmDspDid 是用于定义诊断服务中数据标识符（DID）的配置，它指定了DID的属性、访问权限和与之关联的读写函数。|
|描述|注意：确保DID的唯一性以避免在诊断会话中的冲突；合理配置访问权限以符合安全要求；在配置读写函数时，确保它们符合实际的硬件和应用需求。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidUsed|
|描述|Allow to activate or deactivate the usage of a DID, for multi purpose ECUs|
|描述|概述：DcmDspDidUsed配置项用于指定在诊断服务中使用的数据标识符（DID），它定义了哪些DID将被诊断通信管理器（Diagnostic Communication Manager）识别和处理。|
|描述|注意：在配置DcmDspDidUsed时，需要确保所引用的DID已在系统中定义，并且与诊断需求相匹配；DID的授权级别和安全访问条件也需要正确配置，以确保只有合适的诊断会话和安全级别才能访问这些DID；此外，DcmDspDidUsed配置应与车辆的诊断规范一致，避免配置不一致导致的诊断功能异常。|
|说明|true = DID available false = DID not available|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDidUsePort|
|描述|Selects application interface type for DID data elements between a single operation for all data elements or data element specific operations.|
|描述|概述：DcmDspDidUsePort配置项用于指定诊断数据标识符（DID）是否使用端口接口来访问数据。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保DcmDspDidUsePort的设置与DID访问方式一致；如果使用端口接口，则需要定义相应的端口接口映射；不使用端口时，应使用内部或外部函数访问DID数据。|
|多实例个数|1 - 1|
|默认值|USE_DATA_ELEMENT_SPECIFIC_INTERFACES|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidIdentifier|
|描述|2 byte Identifier of the DID|
|描述|概述：DcmDspDidIdentifier用于定义诊断数据标识符（DID）的属性，包括DID的标识符号、访问权限、以及与之关联的读写服务等。|
|描述|注意：在配置DcmDspDidIdentifier时，确保DID符合ISO 14229标准中定义的范围；配置的访问权限需满足安全访问需求，避免未授权访问；AUTOSAR CP 4.4中对DID的处理能力和配置方式可能与早期版本有所不同，需注意兼容性。|
|说明|Within each DcmConfigSet all DcmDspDidIdentifier values shall be unique.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidSize|
|描述|Length of a DID in byte(s).|
|描述|概述：DcmDspDidSize配置项用于定义诊断数据标识符（DID）的大小，即DID所能承载的数据长度，这对于确保数据的正确读取和编码至关重要。|
|描述|注意：DID大小需根据实际应用需求和标准协议要求谨慎设置；超出规定大小的DID可能导致诊断通信过程中的数据错误或丢失；在AUTOSAR CP 4.4中，确保DID大小与ECU支持的数据长度一致是必要的。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidInfoRef|
|描述|Reference to DcmDspDidInfo containing information on this DID.|
|描述|概述：DcmDspDidInfoRef是一个配置项，用于引用与诊断数据标识符(DID)相关的信息，如DID的属性、服务和安全级别等，以支持诊断服务中对DID的处理。|
|描述|注意：在配置DcmDspDidInfoRef时，确保引用的信息与DID的实际需求相匹配，以避免诊断服务中的错误处理；引用的信息应在系统中唯一定义，避免重复或冲突；AUTOSAR CP 4.4标准中对DcmDspDidInfoRef的使用有明确规范，需要遵守相关规则以保证兼容性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDidInfo|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidRef|
|描述|Reference to DcmDspDid in case this DID refer to one or serveral other DID's|
|描述|概述：DcmDspDidRef配置项用于定义诊断服务中数据标识符（DID）的引用，确保正确的数据访问和操作。|
|描述|注意：在配置DcmDspDidRef时，必须确保引用的DID在系统中是存在且有效的；配置错误可能导致诊断通信失败；应遵循AUTOSAR CP 4.4标准中对DID管理和访问的具体规定。|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDid|

##### 1.3.8.1. DcmDspDidSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidSignal|
|描述|This container defines the reference to 1 DcmDspData container and position relevant for this DID.|
|描述|概述：DcmDspDidSignal配置项用于定义诊断数据标识符（DID）与信号之间的映射关系，确保在执行诊断服务时能够正确访问和操作特定的车辆信号。|
|描述|注意：在配置DcmDspDidSignal时，需确保信号与DID之间的映射关系准确无误；对每个DID，应详细定义信号的访问权限和安全级别；此配置项在AUTOSAR CP 4.4标准中应遵循诊断通信管理模块的规范要求。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidByteOffset|
|描述|Defines the absolute byte offset of the data defined by DcmDspDidDataRef reference to DcmDspData container in the DID.|
|描述|概述：DcmDspDidByteOffset配置项用于定义数据标识符（DID）在数据存储区中的字节偏移量，这决定了DID数据在内存中的具体位置。|
|描述|注意：在配置DcmDspDidByteOffset时，需要确保偏移量正确反映了DID数据在内存中的实际位置；避免不同的DID之间存在重叠，这可能导致数据的读写冲突；在配置时还应考虑数据对齐要求，以确保有效的内存访问和符合架构的数据访问规则。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidDataRef|
|描述|Reference to 1 DcmDspData container relevant for this DID.|
|描述|概述：DcmDspDidDataRef配置项用于定义诊断数据标识符（DID）与其相关数据元素的关联，这样在诊断通信中可以正确地访问和管理这些数据。|
|描述|注意：在配置DcmDspDidDataRef时，必须确保引用的数据元素与DID兼容，并且满足诊断服务的数据格式和长度要求；此外，应当注意数据元素的访问权限设置，以确保只有授权的诊断会话和安全等级才能访问敏感数据；在AUTOSAR CP 4.4标准中，如果配置项的属性与标准不一致，可能会导致诊断服务无法正确执行或数据访问出现错误。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspData|

##### 1.3.8.2. DcmDspDidSupportInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidSupportInfo|
|描述|This container defines the support information to declare the usability of the data bytes within the DIDs|
|描述|概述：DcmDspDidSupportInfo配置项用于定义诊断服务中数据标识符（DID）的支持信息，包括DID是否支持读取、写入、控制等操作。|
|描述|注意：在配置DcmDspDidSupportInfo时，需要确保每个DID的支持信息与实际功能需求相匹配；对于不支持的操作，应明确标记以避免诊断工具误操作；AUTOSAR CP 4.4标准要求详细定义每个DID的支持级别，以确保诊断通信的准确性和安全性。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidSupportInfoLen|
|描述|Length of the support information in bytes.|
|描述|概述：DcmDspDidSupportInfoLen配置项用于定义诊断服务中数据标识符（DID）的支持信息长度，即DID的支持信息所占用的字节数。|
|描述|注意：在AUTOSAR CP 4.4标准中，DcmDspDidSupportInfoLen的值应当与实际DID支持信息的长度相匹配；如果设置不正确，可能会导致诊断响应格式错误或信息丢失；此配置项通常由诊断通信管理模块的开发者或配置工程师根据具体的DID和诊断需求来设定。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidSupportInfoPos|
|描述|Length of the support information in bytes.|
|描述|概述：DcmDspDidSupportInfoPos配置项用于定义数据标识符（DID）在诊断服务中的支持信息位置，这有助于诊断服务确定如何处理特定的DID。|
|描述|注意：在配置DcmDspDidSupportInfoPos时，需要确保DID与其支持信息位置的映射是唯一的，以避免在诊断通信过程中的任何歧义；此外，应当遵循AUTOSAR标准中对于DID支持信息的规定，确保配置的兼容性和正确性；在实际应用中，还需考虑DID支持信息位置对于诊断工具的影响，以确保工具能正确解析和使用DID。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.3.9. DcmDspDidInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidInfo|
|描述|This container contains the configuration (parameters) of the DID's Info|
|描述|概述：DcmDspDidInfo配置项用于定义诊断数据标识符（DID）的属性，包括DID的读取、写入和控制权限，以及与之相关的服务和子功能。|
|描述|注意：在配置DcmDspDidInfo时，需要确保DID与其属性的匹配正确，遵循ISO 14229和AUTOSAR标准中对服务和子功能的定义；此外，对于安全相关的DID，还需配置相应的安全访问级别；在配置过程中，还应注意DID的唯一性，避免与其他DID冲突。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidDynamicallyDefined|
|描述|Indicates if this DID can be dynamically defined|
|描述|概述：DcmDspDidDynamicallyDefined配置项用于定义动态数据标识符（Dynamic Data Identifier, DID）的属性，这些DIDs可以在车辆运行时通过诊断服务动态定义。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保动态定义的DIDs不与静态定义的DIDs冲突；动态DIDs的管理需要遵循诊断服务的规范；对于动态DIDs的存储和恢复机制，应当考虑车辆断电后的数据持久性要求。|
|说明|true = DID can be dynamically defined false = DID can not be dynamically defined|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDDDIDMaxElements|
|描述|Maximum number of source elements of a DDDID.|
|描述|概述：DcmDspDDDIDMaxElements配置项定义了动态定义数据标识符（Dynamic Data Identifier, DDDID）中最大元素的数量，这是用于诊断通信中，允许在一个DDDID中动态定义的最大数据元素数。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保此配置项的值不超过实际系统能够处理的最大元素数量；过高的值可能会导致系统资源不足，而过低的值可能限制了DDDID的灵活性和功能性；此配置项的设置应考虑到ECU的内存和处理能力。|
|多实例个数|0 - 1|
|默认值|1|
|取值范围|1 - 255|

##### 1.3.9.1. DcmDspDidControl

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidControl|
|描述|This container contains the configuration (parameters) of the DID control.|
|描述|概述：DcmDspDidControl配置项用于定义诊断数据标识符（DID）的控制属性，包括控制选项和相关的服务处理规则，以便在车辆诊断通信中对DID执行控制操作。|
|描述|注意：在配置DcmDspDidControl时，需要确保控制选项与DID支持的控制类型相匹配；应注意与DcmDspDidInfo配置项的一致性，以确保正确的服务响应；在AUTOSAR CP 4.4标准中，控制操作可能受到安全访问（Secured Access）的限制，因此配置时应考虑安全策略的要求。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidFreezeCurrentState|
|描述|This indicates the presence of "FreezeCurrentState".|
|描述|概述：DcmDspDidFreezeCurrentState配置项用于定义诊断服务是否支持冻结当前数据标识符（DID）的状态，这允许在诊断会话期间暂时保存DID的当前值。|
|描述|注意：在实现此功能时，需要确保ECU具备足够的资源来存储冻结的DID值；此配置项的使用应符合车辆制造商的诊断策略和要求；在配置时应注意与其他诊断服务的兼容性和数据一致性。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidResetToDefault|
|描述|This indicates the presence of "ResetToDefault".|
|描述|概述：DcmDspDidResetToDefault配置项用于定义诊断服务中重置数据标识符（DID）到其默认值的行为，确保在执行特定的诊断请求时，能够将DID恢复到预设的默认状态。|
|描述|注意：在配置时需确保DID支持重置到默认值的操作；重置操作可能会影响系统的正常运行，需谨慎设计；此配置项在AUTOSAR CP 4.4中应与DID相关的安全访问权限设置相匹配，以避免安全风险。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidShortTermAdjustment|
|描述|This indicates the presence of "ShortTermAdjustment".|
|描述|概述：DcmDspDidShortTermAdjustment配置项用于定义诊断会话中，对数据标识符（DID）的短期调整参数和行为。|
|描述|注意：该配置项必须确保与车辆的安全和隐私要求相符合；调整操作应在授权的诊断会话中进行，避免未授权访问；在实施时需考虑对系统性能的影响，确保不会对其他系统功能造成干扰。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspDidControlMask|
|描述|This indicates the presence of "controlEnableMask" in SWC service interfaces and defines how the Dcm treats a service request.|
|描述|概述：DcmDspDidControlMask配置项用于定义诊断服务中数据标识符（DID）的控制选项掩码，它决定了哪些位可以被客户端（如诊断工具）控制。|
|描述|注意：在配置DcmDspDidControlMask时，需要确保掩码与DID支持的控制选项相匹配；掩码中的每个位代表DID的一个特定控制功能，因此需要仔细设计以避免不必要的功能暴露；在AUTOSAR CP 4.4标准中，如果该属性与DID的实际功能或安全要求不一致，可能会导致诊断服务的安全性问题。|
|多实例个数|1 - 1|
|默认值|DCM_CONTROLMASK_INTERNAL|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidControlMaskSize|
|描述|The value defines the size of the controlEnableMaskRecord in bytes.|
|描述|概述：DcmDspDidControlMaskSize配置项定义了用于DID控制操作的掩码大小，该掩码用于确定哪些位可以被控制。|
|描述|注意：掩码大小应与DID的大小相匹配，以确保正确的操作；在配置掩码时，需要注意数据的字节序；掩码大小的配置必须符合ECU支持的数据长度限制。|
|多实例个数|0 - 1|
|取值范围|1 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidControlRole|
|描述|Bitfield were each bit represents one dedicated role. A DID is granted IOcontrol access if the bit value is 1. If a bit value is 0, the DID is not allowed to be controlled for that role.|
|描述|概述：DcmDspDidControlRole配置项定义了数据标识符（DID）的控制权限，用于指定哪些会话层或安全访问级别可以对DID执行控制操作。|
|描述|注意：在配置DcmDspDidControlRole时，需要确保控制权限与项目的安全需求相匹配；此外，应当注意不同DID可能需要不同的控制权限设置；在配置时还应考虑到会话层的变化，确保在不同会话下DID的控制权限得到正确管理。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidControlModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspDidControlModeRuleRef配置项用于引用一个诊断服务数据标识符（DID）的控制模式规则，该规则定义了在何种条件下可以对DID执行控制操作。|
|描述|注意：在配置DcmDspDidControlModeRuleRef时，需要确保引用的控制模式规则已经在系统中定义；控制模式规则应与DID的安全级别和会话控制要求相匹配；在AUTOSAR CP 4.4标准中，控制模式规则的定义和引用应遵循模块的规范要求。|
|说明|Mode rule which controls this DID. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidControlSecurityLevelRef|
|描述|Reference to DcmDspSecurityRow|
|描述|概述：DcmDspDidControlSecurityLevelRef配置项用于指定数据标识符（DID）控制操作所需的安全访问级别，确保只有在达到适当的安全级别后才能对DID执行控制操作。|
|描述|注意：在配置时需确保引用的安全级别与实际的安全策略相匹配；如果配置了不支持的安全级别，可能导致控制操作无法执行；AUTOSAR CP 4.4标准中可能有对支持的安全级别数量或类型的限制，需要遵守这些限制。|
|说明|Security levels allowed to control this DID. If there is no reference, no check of security level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidControlSessionRef|
|描述|Reference to DcmDspSessionRow|
|描述|概述：DcmDspDidControlSessionRef配置项用于指定哪些诊断会话层(Diagnostic Session Layer)可以访问特定的数据标识符(DID)进行控制操作。|
|描述|注意：确保只有授权的诊断会话能够访问和控制DID；在配置时需遵循安全访问规则，防止未授权访问；该配置项应与DID的安全访问级别设置相匹配，以确保数据安全。|
|说明|Sessions allowed to control this DID. If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidControlVehicleSystemGroupRef|
|描述|Defines DID IO Control operation availability dependency to a specific VSG|
|描述|概述：DcmDspDidControlVehicleSystemGroupRef配置项用于引用诊断服务组件中的车辆系统组，该组定义了一组相关的车辆控制系统，这些系统可以通过诊断数据标识符（DID）进行控制。|
|描述|注意：在配置DcmDspDidControlVehicleSystemGroupRef时，需要确保引用的车辆系统组在系统中是存在且有效的；此配置项通常与特定的DID关联，确保正确映射以满足诊断需求；在AUTOSAR CP 4.4标准中，应当遵循诊断配置的模块化原则，确保配置的一致性和可维护性。|
|说明|VSGs allowed to control this DID. If there is no reference, no check of vsg shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspVehicleSystemGroup/DcmDspVehicleSystemGroupRow|

###### 1.3.9.1.1. DcmDspDidControlEnableMask

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidControlEnableMask|
|描述|The shortname of the container value defines the symbol of the controlMask.|
|描述|概述：DcmDspDidControlEnableMask配置项用于定义诊断服务中数据标识符（DID）的控制权限，它指定了在执行控制操作时哪些位需要被检查和使能。|
|描述|注意：在配置DcmDspDidControlEnableMask时，需要确保掩码与DID支持的控制操作相匹配；掩码的长度应与DID的大小一致；在定义掩码时，要注意权限管理，确保只有授权的用户可以执行敏感或关键的控制操作。|
|多实例个数|0 - 32|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidControlMaskBitPosition|
|描述|Defines the position of the bit in the controlMask starting from most significant bit (MSB first) to least significant bit.|
|描述|概述：DcmDspDidControlMaskBitPosition 定义了在诊断控制服务中，控制选项掩码的位位置，用于控制数据标识符的特定功能。|
|描述|注意：在配置控制选项掩码时，必须确保位位置正确且符合相关诊断标准；掩码位位置的错误配置可能导致诊断功能不正确或无法执行；此配置项应与车辆制造商的诊断需求和规范一致。|
|说明|This Bit endianness is identical to the controlMask in UDS. The DcmDspDidControlMaskSize should be considered for most significant bit.|
|多实例个数|1 - 1|
|取值范围|0 - 31|

##### 1.3.9.2. DcmDspDidRead

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidRead|
|描述|This container contains the configuration (parameters) of the DID read.|
|描述|概述：DcmDspDidRead配置项用于定义诊断服务中数据标识符（DID）的读取属性，包括访问权限和读取方法。|
|描述|注意：确保配置的读取权限符合车辆制造商的安全要求；在配置读取方法时，应考虑数据的实时性和准确性；遵循AUTOSAR CP 4.4标准中对DID读取的具体规定和限制。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidReadRole|
|描述|Bitfield were each bit represents one dedicated role. A DID is granted read access if the bit value is 1. If a bit value is 0, the DID is not allowed to be read for that role.|
|描述|概述：DcmDspDidReadRole配置项定义了数据标识符（DID）在诊断服务中的读取权限，用于控制不同诊断会话和安全等级下的访问权限。|
|描述|注意：确保配置的读取权限符合车辆制造商的安全要求和法规要求；在配置时需考虑不同诊断会话和安全等级的需求；AUTOSAR CP 4.4标准中，此配置项应详细定义每个DID的访问权限，以防止未授权访问。|
|说明|Reading DIDs is possible by different UDS services. This setting applies to all possible DID read operations.|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidReadModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspDidReadModeRuleRef配置项用于引用一个规则，该规则定义了数据标识符（DID）在诊断会话控制（Diagnostic Session Control）和安全访问（Security Access）等级下的读取条件。|
|描述|注意：在配置DcmDspDidReadModeRuleRef时，需要确保引用的规则已经在Dcm配置中定义；此外，要注意规则的适用性，确保在特定的诊断会话和安全等级下DID是可读的；如果规则配置不正确，可能导致DID在某些情况下无法被正确读取，影响诊断功能。|
|说明|Mode rule which controls to read this DID. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidReadSecurityLevelRef|
|描述|Reference to DcmDspSecurityRow Referenced security levels are allowed to read this DID.|
|描述|概述：DcmDspDidReadSecurityLevelRef配置项用于指定访问特定数据标识符（DID）时所需的安全等级，确保只有在满足相应安全条件下才能读取敏感或受保护的数据。|
|描述|注意：在配置时需确保引用的安全等级与实际实现的安全策略相匹配；如果配置了不支持的安全等级，可能导致数据访问权限校验失败；AUTOSAR CP 4.4标准中，安全等级通常以bitmask的形式表示，需要注意正确配置这些bitmask值。|
|说明|If there is no reference, no check of security level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidReadSessionRef|
|描述|Reference to DcmDspSessionRow Referenced sessions are allowed to read this DID.|
|描述|概述：DcmDspDidReadSessionRef配置项指定了数据标识符（DID）在哪些诊断会话层级中可被读取。|
|描述|注意：确保配置的会话层级与实际应用中的诊断安全需求相匹配；不正确的会话配置可能导致数据访问权限问题；在AUTOSAR CP 4.4中，每个DID的会话访问权限应明确区分并正确配置。|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidReadVehicleSystemGroupRef|
|描述|Defines DID read operation availability dependency to a specific VSG.|
|描述|概述：DcmDspDidReadVehicleSystemGroupRef配置项用于定义诊断服务中，读取数据标识符（DID）时所关联的车辆系统组引用。|
|描述|注意：确保引用的车辆系统组在系统中已定义且有效；此配置项应与具体的DID及其读取权限和安全策略一致；在配置时需考虑数据的安全性和访问权限控制。|
|说明|If there is no reference, no check of vsg shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspVehicleSystemGroup/DcmDspVehicleSystemGroupRow|

##### 1.3.9.3. DcmDspDidWrite

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidWrite|
|描述|This container contains the configuration (parameters) of the DID write.|
|描述|概述：DcmDspDidWrite配置项用于定义诊断服务中数据标识符（DID）的写操作属性，包括写入权限、写入条件和相关的回调函数。|
|描述|注意：在配置DcmDspDidWrite时，需要确保写入权限符合系统安全要求；写入条件应与实际应用场景相匹配，避免在不适当的时机允许写操作；回调函数需要正确实现，以确保写入操作的数据处理符合预期。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidWriteRole|
|描述|Bitfield were each bit represents one dedicated role. A DID is granted write access if the bit value is 1. If a bit value is 0, the DID is not allowed to be written for that role.|
|描述|概述：DcmDspDidWriteRole配置项定义了数据标识符（DID）的写入权限，用于控制对特定DID的写入访问，确保只有授权的客户端可以修改DID的值。|
|描述|注意：在配置DcmDspDidWriteRole时，需要确保权限设置符合应用的安全要求；此外，应考虑与DcmDspDidReadRole的配置一致性，以保证读写权限的合理性；最后，需要注意的是，任何修改都应遵循AUTOSAR CP 4.4标准中关于数据访问权限的规定。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidWriteModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspDidWriteModeRuleRef配置项用于引用一个规则，该规则定义了数据标识符（DID）写入操作的条件，确保只有在满足特定条件时才能对DID执行写入操作。|
|描述|注意：在配置DcmDspDidWriteModeRuleRef时，需要确保引用的规则已经在系统中定义；规则的定义应符合AUTOSAR的诊断事件管理和服务请求管理要求；此外，对于写入操作的安全性和合法性要求较高，因此需要仔细设计和验证引用的规则。|
|说明|Mode rule which controls to write this DID. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidWriteSecurityLevelRef|
|描述|Reference to DcmDspSecurityRow Referenced security levels are allowed to wirte this DID.|
|描述|概述：DcmDspDidWriteSecurityLevelRef配置项用于指定在诊断服务中写入数据标识符（DID）所需的安全访问级别，确保只有在满足相应安全级别条件下才能对DID进行写操作。|
|描述|注意：在配置此项时，必须确保引用的安全级别已在Dcm的安全策略中定义；安全级别的配置应与实际的安全需求相匹配，以防止未授权的数据访问；AUTOSAR CP 4.4标准中可能对安全级别的表示方法和可用选项有具体规定，需要遵守这些规定以确保兼容性。|
|说明|If there is no reference, no check of security level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidWriteSessionRef|
|描述|Reference to DcmDspSessionRow Referenced sessions are allowed to write this DID.|
|描述|概述：DcmDspDidWriteSessionRef配置项用于指定哪些诊断会话层次（Diagnostic Session Layers）允许对数据标识符（DID）进行写操作。|
|描述|注意：确保仅在允许的诊断会话中进行DID的写操作，避免在不适当的会话中修改数据；此配置项对安全访问控制至关重要，需谨慎配置以防止未授权访问。|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidWriteVehicleSystemGroupRef|
|描述|Defines DID write operation availability dependency to a specific VSG.|
|描述|概述：DcmDspDidWriteVehicleSystemGroupRef配置项用于引用一个车辆系统组，该组定义了一组数据标识符（DID），这些DID可以在诊断会话中被写入。|
|描述|注意：在配置时需确保引用的车辆系统组中的DID支持写入操作；对于不支持写入的DID，尝试写入可能会导致诊断会话中的错误响应；AUTOSAR CP 4.4标准中，确保该配置项与车辆系统组的定义一致，避免引用不存在的组。|
|说明|If there is no reference, no check of vsg shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspVehicleSystemGroup/DcmDspVehicleSystemGroupRow|

#### 1.3.10. DcmDspDidRange

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDidRange|
|描述|This container defines the DID Range|
|描述|概述：DcmDspDidRange配置项用于定义诊断服务中可用的数据标识符（DID）范围，允许对一系列DID进行统一处理，而不是单独配置每个DID。|
|描述|注意：在配置DcmDspDidRange时，确保DID范围内的每个DID都不与单独配置的DID冲突；DID范围的使用应遵循诊断协议标准，确保兼容性；AUTOSAR CP 4.4标准中对DID范围的支持可能有特定限制或要求，需要仔细检查标准文档。|
|多实例个数|0 - 255|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidRangeHasGaps|
|描述|Parameter specifying if there are gaps in the DID range (parameter set to TRUE) or not (parameter set to FALSE)|
|描述|概述：DcmDspDidRangeHasGaps配置项用于指示在诊断数据标识符（DID）范围定义中是否存在间隙，即非连续的DID区间。|
|描述|注意：在定义DID范围时，需要明确指出区间是否连续；如果存在间隙，确保正确配置此属性以反映实际的DID布局；不正确的间隙配置可能会导致诊断服务的响应不符合预期。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspDidRangeUsePort|
|描述|When the parameter DcmDspDidRangeUsePort is set to true the DCM will access the Data using an R-Port requiring a PortInteface DataServices_DIDRange. In that case, DcmDspDidRangeIsDidAvailableFnc, DcmDspDidRangeReadDidFnc and DcmDspDidRangeWriteDidFnc are ignored and the RTE APIs are used. When the parameter DcmDspDidRangeUsePort is false, the DCM calls the functions defined in DcmDspDidRangeIsDidAvailableFnc, DcmDspDidRangeReadDidFnc and DcmDspDidRangeWriteDidFnc.|
|描述|概述：DcmDspDidRangeUsePort配置项用于指定诊断数据标识符（DID）范围是否使用端口接口，以便为一组DID提供读取和写入服务。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保DcmDspDidRangeUsePort的配置与DID范围处理的实现方式相匹配；如果使用端口接口，则需要定义相应的端口API；若不使用端口接口，则应通过其他方式（如内部函数调用）实现DID范围的读写服务。|
|多实例个数|1 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDidRangeIsDidAvailableFnc|
|描述|Function name to request from application if a specific DID is available within the range or not.|
|描述|概述：DcmDspDidRangeIsDidAvailableFnc配置项用于定义一个函数，该函数决定一个动态定义的数据标识符（DID）范围内的特定DID是否可用。|
|描述|注意：在配置动态DID范围时，必须确保此函数正确实现，以便DID范围检查能够正确执行；该函数的实现必须符合AUTOSAR CP 4.4标准中对DID可用性检查的要求；在实现时应注意性能影响，因为该函数可能会被频繁调用。|
|说明|Only relevant if DcmDspDidRangeUsePort is set to false. This parameter is related to the interface Xxx_IsDidAvailable.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDidRangeReadDataLengthFnc|
|描述|Function name to request from application the length of the data of a range DID.|
|描述|概述：DcmDspDidRangeReadDataLengthFnc是一个配置项，用于定义在诊断通信管理器（Diagnostic Communication Manager）中，读取数据标识符（DID）范围时获取数据长度的函数名称。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保该函数名称与实际实现的函数名匹配；该函数需要正确处理数据长度的计算，以避免数据溢出或不一致问题；函数的实现必须符合AUTOSAR的模块接口标准。|
|说明|Only relevant if DcmDspDidRangeUsePort is set to false. This parameter is related to the interface Xxx_ReadDidRangeDataLength.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDidRangeReadDidFnc|
|描述|Function name to request from application the data range value of a DID.(ReadData-function).|
|描述|概述：DcmDspDidRangeReadDidFnc配置项用于定义在诊断服务中，当请求读取数据标识符（DID）范围时，所调用的函数。|
|描述|注意：在配置DcmDspDidRangeReadDidFnc时，需要确保所引用的函数符合AUTOSAR标准中对读取DID范围的函数原型要求；此外，该函数需要能够处理请求的DID范围内的所有可能值，并且要确保对应的数据权限和安全级别得到正确处理；在实现时还应考虑到函数的执行时间，以满足可能的实时性要求。|
|说明|Only relevant if DcmDspDidRangeUsePort is set to false. This parameter is related to the interface Xxx_ReadDidData.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspDidRangeWriteDidFnc|
|描述|Function name to request application to write the data range value of a DID.(WriteData-function).|
|描述|概述：DcmDspDidRangeWriteDidFnc配置项用于定义在诊断服务中，当写入数据标识符（DID）属于一个特定范围时，所调用的函数名称。|
|描述|注意：在配置DcmDspDidRangeWriteDidFnc时，需要确保所引用的函数符合AUTOSAR标准中对服务处理函数的要求；函数需要能够处理请求的写入操作，并返回适当的诊断响应码；此配置项通常与DcmDspDidRange定义关联，确保DID范围与对应的处理函数匹配。|
|说明|Only relevant if DcmDspDidRangeUsePort is set to false. This parameter is related to the interface Xxx_WriteDidData.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidRangeIdentifierLowerLimit|
|描述|Lower limit of DID range.|
|描述|概述：DcmDspDidRangeIdentifierLowerLimit 用于定义诊断数据标识符（DID）范围的下限，这有助于确定哪些DID可以被访问和处理。|
|描述|注意：确保设置的下限值不低于允许的最小DID值；在配置DID范围时，下限值应小于或等于上限值DcmDspDidRangeIdentifierUpperLimit；适当配置此值以避免数据访问冲突或安全问题。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidRangeIdentifierUpperLimit|
|描述|Upper limit of DID range.|
|描述|概述：DcmDspDidRangeIdentifierUpperLimit用于定义诊断数据标识符（DID）范围的上限，这是在配置诊断服务时，用于指定可接受的DID范围的最大值。|
|描述|注意：该配置项的值必须大于或等于DcmDspDidRangeIdentifierLowerLimit的值；确保配置的DID范围不与其他已配置的DID范围重叠；在配置时考虑实际应用中可能需要的DID范围，避免将来的扩展需求导致配置修改。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDidRangeMaxDataLength|
|描述|Maximum data length in bytes|
|描述|概述：DcmDspDidRangeMaxDataLength配置项用于定义在诊断服务中，动态定义数据标识符（DID）范围的最大数据长度，这是为了确保在读取或写入数据时，数据块的大小不会超过ECU处理能力。|
|描述|注意：在配置此参数时，必须确保它反映了ECU的实际数据处理能力和存储限制；超出此长度的数据请求可能会被诊断服务拒绝；此参数的设置应与ECU的内存和性能特性相匹配，以避免潜在的通信或操作问题。|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspDidRangeInfoRef|
|描述|Reference to DcmDspDidInfo containing information on this DID Range.|
|描述|概述：DcmDspDidRangeInfoRef配置项用于引用一个特定的DID范围信息，该信息定义了诊断服务处理动态定义的数据标识符（DID）范围的参数和行为。|
|描述|注意：在配置DcmDspDidRangeInfoRef时，必须确保引用的DID范围信息已经在系统中定义；引用的DID范围必须与实际的诊断需求相匹配，以确保正确的诊断行为；在AUTOSAR CP 4.4标准中，DID范围的配置应遵循标准的模块定义和约束。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDidInfo|

#### 1.3.11. DcmDspEcuReset

|容器属性|值（容器）|
|---|---|
|名称|DcmDspEcuReset|
|描述|This container contains the configuration for DcmDspEcuReset service|
|描述|概述：DcmDspEcuReset配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中ECU复位服务的参数，包括复位类型、复位时间以及与之相关的诊断服务请求和响应行为。|
|描述|注意：在配置DcmDspEcuReset时，需要确保复位类型与ECU支持的复位方式相匹配；复位时间参数应符合系统复位需求和诊断规范；此外，还需注意与安全访问服务的交互，确保在执行复位前满足安全级别要求。|
|多实例个数|0 - 1|

##### 1.3.11.1. DcmDspEcuResetRow

|容器属性|值（容器）|
|---|---|
|名称|DcmDspEcuResetRow|
|描述|This container contains the configuration for each DcmDspEcuReset subservice.|
|描述|概述：DcmDspEcuResetRow配置项用于定义ECU重置类型及其相关属性，如重置服务的支持情况、安全访问级别和会话控制要求等，以便在诊断通信过程中正确处理ECU重置请求。|
|描述|注意：确保为每种重置类型正确配置安全访问级别和会话控制要求，以避免未授权的重置操作；在配置时需考虑ECU的实际能力和安全要求，以确保配置的合理性和安全性；AUTOSAR CP 4.4标准中对ECU重置的处理和配置有明确规范，需遵循标准以保证兼容性。|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmResponseToEcuReset|
|描述|Defines the answer to EcuReset service should come: Before or after the reset.|
|描述|概述：DcmResponseToEcuReset配置项用于定义诊断通信管理器（Diagnostic Communication Manager）如何响应来自外部测试设备的ECU重置请求，包括重置类型和执行后的行为。|
|描述|注意：在配置DcmResponseToEcuReset时，需要确保所选的重置类型与ECU支持的重置类型相匹配；对于安全相关的重置请求，应确保适当的安全措施被实施，以防止未授权的重置操作；AUTOSAR CP 4.4标准中，对于ECU重置的响应行为应详细定义，以避免在重置后出现不可预期的行为。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspEcuResetId|
|描述|Defines the subfunction ID|
|描述|概述：DcmDspEcuResetId 是用于定义诊断服务组件（Diagnostic Communication Manager）中ECU重置类型的标识符，它指定了执行ECU重置时所需的服务标识符和选项。|
|描述|注意：在配置DcmDspEcuResetId时，需要确保其值与ISO 14229标准中定义的ECU重置服务标识符一致；此外，应当检查与该重置类型相关的所有依赖性和权限设置，以确保在执行重置时系统的安全性和一致性；在AUTOSAR CP 4.4标准中，还应注意与诊断事件管理和诊断操作周期的兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 127|

#### 1.3.12. DcmDspMemory

|容器属性|值（容器）|
|---|---|
|名称|DcmDspMemory|
|描述|This container contains the configuration of the memory access.|
|描述|概述：DcmDspMemory配置项用于定义诊断服务组件（Diagnostic Communication Manager）中与内存操作相关的属性，例如读取或写入ECU内存的权限、地址范围以及内存大小等。|
|描述|注意：在配置DcmDspMemory时，需要确保内存地址范围和大小与ECU实际硬件资源相匹配；权限设置应符合安全和诊断策略要求；在AUTOSAR CP 4.4标准中，可能需要考虑与SecOC模块的安全通信集成。|
|多实例个数|0 - 1|

##### 1.3.12.1. DcmDspAddressAndLengthFormatIdentifier

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAddressAndLengthFormatIdentifier|
|描述|This container contains the configuration of the supported AddressAndLengthFormatIdentifiers for memory access.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSupportedAddressAndLengthFormatIdentifier|
|描述|This parameter defines the supported AddressAndLengthFormatIdentifier of the request message.|
|多实例个数|1 - inf|
|取值范围|0 - 255|

##### 1.3.12.2. DcmDspMemoryIdInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspMemoryIdInfo|
|描述|Provides the value of memory identifier used to select the desired memory device|
|描述|概述：DcmDspMemoryIdInfo配置项用于定义诊断服务中内存标识符的属性，包括内存地址范围和内存大小，用于支持读写内存服务（如服务10、3D）中对不同内存区域的访问控制。|
|描述|注意：内存标识符必须唯一，以避免在诊断会话中对内存区域的访问冲突；配置的内存地址范围和大小应与实际硬件资源相匹配，确保诊断访问的有效性和安全性；在配置时需考虑不同安全访问级别对内存访问的限制。|
|说明|This container contains the configuration of the memory access requested through diagnostic services : ReadMemoryByAddress, WriteMemoryByAddress, and DynamicallyDefineDataIdentifier|
|多实例个数|1 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspMemoryIdValue|
|描述|Value of the memory device identifier used.|
|说明|Each DcmDspMemoryIdInfo should have a unique ID. The MemoryIdValue is retrieved from the request messages (RMBA,WMBA,RD,RU,DDDI) according to ISO-14229-1 with the most significant byte of the request parameter memoryAddress.|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|

###### 1.3.12.2.1. DcmDspReadMemoryRangeByLabelInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspReadMemoryRangeByLabelInfo|
|描述|Provides a memory range allowed for reading via labels (lower and higher address configured as strings).|
|描述|概述：DcmDspReadMemoryRangeByLabelInfo是一个配置项，用于定义诊断服务中读取内存范围的参数，包括内存地址、大小以及相关的访问权限标签。|
|描述|注意：在配置时需确保内存地址和大小的正确性，以避免对系统的非法访问或潜在的内存损坏；访问权限标签应与系统的安全策略相匹配，确保只有授权的诊断会话能够访问对应的内存区域；AUTOSAR CP 4.4标准可能对内存读取服务的实现和配置有特定的要求，需要仔细参照标准文档进行配置。|
|多实例个数|0 - inf|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeByLabelHigh|
|描述|High memory address as label (string) of a range allowed for reading.|
|描述|概述：DcmDspReadMemoryRangeByLabelHigh配置项用于定义诊断服务中读取内存范围的上限地址，这是在执行读取内存范围（ReadMemoryByAddress）服务时，通过标签指定的内存地址的最高可能值。|
|描述|注意：在配置此项时，需确保上限地址不低于对应的DcmDspReadMemoryRangeByLabelLow配置的下限地址；地址范围应符合ECU内存布局和安全访问要求；此配置应与ECU的实际物理内存地址和访问权限相匹配，避免配置超出实际可访问的内存范围。|
|多实例个数|1 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeByLabelLow|
|描述|Low memory address as label (string) of a range allowed for reading.|
|描述|概述：DcmDspReadMemoryRangeByLabelLow配置项用于定义诊断服务中读取内存范围请求的最低地址标签，它指定了允许读取的内存地址下限。|
|描述|注意：在配置时需确保该地址低于或等于对应的DcmDspReadMemoryRangeByLabelHigh配置项中的地址，以保证内存读取范围的有效性和安全性；此外，地址应当符合ECU内存地址空间的实际分布，避免指向非法或保护区域；在AUTOSAR CP 4.4标准中，确保该配置与ECU的内存映射和安全访问权限设置一致。|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeModeRuleRef|
|描述|Reference to DcmModeRule|
|说明|Mode rule which controls read access on this memory address. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeSecurityLevelRef|
|描述|Link to the Security Access Levels needed for read access on this memory address. If there is no reference, no check of security level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeSessionLevelRef|
|描述|Link to the session level needed for access to this memory address range.|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

###### 1.3.12.2.2. DcmDspReadMemoryRangeInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspReadMemoryRangeInfo|
|描述|Provides the range of memory address allowed for reading|
|描述|概述：DcmDspReadMemoryRangeInfo配置项用于定义诊断服务组件（Diagnostic Communication Manager）中读取内存范围的参数，包括内存地址、大小以及相关的安全访问权限。|
|描述|注意：在配置DcmDspReadMemoryRangeInfo时，需要确保内存地址和大小的定义不会超出实际的物理或应用程序内存范围；必须考虑到安全访问权限，以防止未授权的内存访问；此外，应当检查与ECU内存映射的一致性，确保诊断请求能够正确地访问指定的内存区域。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeHigh|
|描述|High memory address of a range allowed for reading|
|描述|概述：DcmDspReadMemoryRangeHigh配置项用于定义诊断服务中读取内存范围的上限地址，确保诊断请求只能访问允许的内存区域。|
|描述|注意：在配置时需确保上限地址不低于对应的DcmDspReadMemoryRangeLow配置项中的下限地址；地址范围应符合ECU内存布局和安全要求；在配置多个内存范围时，要避免地址范围重叠。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeLow|
|描述|Low memory address of a range allowed for reading|
|描述|概述：DcmDspReadMemoryRangeLow配置项用于定义诊断服务读取内存范围的最低地址限制，确保内存读取操作在允许的地址范围内进行。|
|描述|注意：在配置DcmDspReadMemoryRangeLow时，需要确保该地址低于或等于对应的DcmDspReadMemoryRangeHigh配置项以定义有效的地址范围；此外，应检查ECU内存映射和安全访问权限，以确保配置的地址是可访问和允许读取的；在AUTOSAR CP 4.4标准中，地址值应符合ECU的内存寻址能力和数据类型限制。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspReadMemoryRangeModeRuleRef配置项用于定义诊断服务读取内存范围时应用的模式规则引用，确保在执行读取内存操作时，满足特定的条件或权限限制。|
|描述|注意：该配置项需要与Dcm的安全访问和会话控制策略相匹配，确保只有在适当的诊断会话和安全访问级别下才能读取特定的内存范围；在配置时需确保引用的模式规则存在且正确；AUTOSAR CP 4.4中对于权限管理和安全性有更加严格的要求，需要仔细检查与之相关的配置。|
|说明|Mode rule which controls read access on this memory address. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeSecurityLevelRef|
|描述|Link to the Security Access Levels needed for read access on this memory address. If there is no reference, no check of security level shall be done.|
|描述|概述：DcmDspReadMemoryRangeSecurityLevelRef配置项用于指定访问特定内存范围时所需的安全等级，确保只有在达到相应安全等级后才能读取特定的内存区域。|
|描述|注意：在配置时需确保引用的安全等级已在系统中定义；不同的内存范围可以配置不同的安全等级要求，以满足不同安全需求；AUTOSAR CP 4.4标准中，安全等级的配置和管理是一个重要方面，需要仔细规划以确保系统安全。|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspReadMemoryRangeSessionLevelRef|
|描述|Link to the session level needed for access to this memory address range.|
|描述|概述：DcmDspReadMemoryRangeSessionLevelRef配置项指定了在执行读取内存范围操作时，允许的诊断会话级别，用于控制不同诊断会话下哪些内存区域可以被访问。|
|描述|注意：确保配置的会话级别与实际应用场景相匹配，避免在安全关键的会话中误配置允许访问敏感内存区域；在配置时考虑所有可能的会话级别，确保系统的安全性和数据保护；AUTOSAR CP 4.4标准中，对会话级别的定义和使用有严格规范，需要遵循这些规范以保证兼容性。|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

###### 1.3.12.2.3. DcmDspWriteMemoryRangeByLabelInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspWriteMemoryRangeByLabelInfo|
|描述|Provides a memory range allowed for writing via labels (lower and higher address configured as strings).|
|描述|概述：DcmDspWriteMemoryRangeByLabelInfo配置项用于定义诊断服务中写入内存范围的参数，包括内存地址、大小以及访问权限等信息，以支持对特定内存区域的写操作。|
|描述|注意：在配置时需确保内存地址和大小的正确性，避免对系统的其他部分造成意外的影响；必须正确设置访问权限，以防止未授权的访问；该配置项在AUTOSAR CP 4.4中应与安全和诊断需求紧密结合，确保配置的安全性。|
|多实例个数|0 - inf|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeByLabelHigh|
|描述|High memory address as label (string) of a range allowed for writing.|
|描述|概述：DcmDspWriteMemoryRangeByLabelHigh配置项用于定义诊断服务中写入内存操作的上限地址标签，它指定了可以通过诊断服务写入的内存区域的最高地址。|
|描述|注意：在配置时需确保该地址范围内的内存可被安全写入，且不会影响系统的稳定性；地址标签应与实际的内存布局相匹配，避免因地址错误导致潜在的内存损坏；在配置多个内存范围时，应保证它们之间不会重叠，以防止写入操作的冲突。|
|多实例个数|1 - 1|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeByLabelLow|
|描述|Low memory address as label (string) of a range allowed for writing.|
|描述|概述：DcmDspWriteMemoryRangeByLabelLow配置项用于定义诊断服务中写入内存操作的最低地址限制，确保内存写入操作不会超出预设的地址范围。|
|描述|注意：在配置时需确保地址范围与实际可写入的内存区域相匹配，避免因地址错误导致系统不稳定或安全问题；此配置项应与DcmDspWriteMemoryRangeByLabelHigh一起使用，以定义一个完整的内存写入范围；在AUTOSAR CP 4.4标准中，如果该配置项的属性与标准定义不一致，可能会导致诊断服务无法正确执行内存写入操作。|
|多实例个数|1 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeModeRuleRef|
|描述|Reference to DcmModeRule|
|说明|Mode rule which controls write access on this memory address. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeSecurityLevelRef|
|描述|Link to the Security Access Levels needed for write access on this memory address. If there is no reference, no check of security level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeSessionLevelRef|
|描述|Link to the session level needed for access to this memory address range.|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

###### 1.3.12.2.4. DcmDspWriteMemoryRangeInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspWriteMemoryRangeInfo|
|描述|Provides the range of memory address allowed for writting.|
|描述|概述：DcmDspWriteMemoryRangeInfo配置项定义了诊断服务中写内存操作的范围信息，包括可写的内存地址范围和相关的安全访问级别。|
|描述|注意：在配置时需确保内存地址范围不与其他服务或应用的内存使用冲突；必须正确配置安全访问级别，以防止未授权访问；该配置项在AUTOSAR CP 4.4中应与诊断安全需求相一致，确保配置的安全性。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeHigh|
|描述|High memory address of a range allowed for writing.|
|描述|概述：DcmDspWriteMemoryRangeHigh配置项用于定义诊断服务中写入内存操作的最高内存地址范围，确保诊断请求只能访问允许的内存区域。|
|描述|注意：在配置时需确保该地址范围与实际可写内存区域相匹配，避免潜在的安全风险；该配置项通常与DcmDspWriteMemoryRangeLow一起使用，以定义一个完整的内存写入范围；在多内存区域的系统中，可能需要配置多个写内存范围对。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeLow|
|描述|Low memory address of a range allowed for writing|
|描述|概述：DcmDspWriteMemoryRangeLow配置项用于定义诊断服务中可写内存地址的最低边界，确保内存写入操作的地址范围在允许的区域内。|
|描述|注意：在配置DcmDspWriteMemoryRangeLow时，必须确保该值不低于ECU内存地址空间的最小边界；同时，该值应与DcmDspWriteMemoryRangeHigh配合使用，以定义一个有效的写入内存范围；此外，应考虑ECU的安全策略，以防止未授权的内存写入操作。|
|多实例个数|1 - 1|
|取值范围|0 - 4294967294|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeModeRuleRef|
|描述|Reference to DcmModeRule|
|描述|概述：DcmDspWriteMemoryRangeModeRuleRef配置项用于引用特定的诊断会话和安全访问级别规则，这些规则定义了在哪些条件下允许对内存范围进行写操作。|
|描述|注意：在配置DcmDspWriteMemoryRangeModeRuleRef时，需要确保引用的诊断会话和安全访问级别规则与实际的应用场景相匹配；引用的规则必须在Dcm配置中预先定义；违反这些规则可能导致诊断服务的写操作被不正确地限制或允许。|
|说明|Mode rule which controls write access on this memory address. If there is no reference, no check of the mode rule shall be done.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeSecurityLevelRef|
|描述|Link to the Security Access Levels needed for write access on this memory address. If there is no reference, no check of security level shall be done.|
|描述|概述：DcmDspWriteMemoryRangeSecurityLevelRef配置项用于定义在执行写内存操作时必须满足的安全级别，确保只有在适当的安全级别下才能访问或修改特定的内存区域。|
|描述|注意：必须确保引用的安全级别与系统的安全策略一致；在配置时应考虑所有潜在的安全风险，避免未授权的内存访问；该配置项应与Dcm的安全策略紧密集成，确保其有效性和一致性。|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSecurity/DcmDspSecurityRow|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspWriteMemoryRangeSessionLevelRef|
|描述|Link to the session level needed for access to this memory address range.|
|描述|概述：DcmDspWriteMemoryRangeSessionLevelRef配置项用于指定在执行写内存范围操作时，允许的诊断会话级别，确保只有在特定的会话级别下才能执行写内存操作。|
|描述|注意：在配置时需确保引用的会话级别与实际支持的诊断会话级别相匹配；若配置的会话级别不支持写内存操作，则在该会话级别下执行写内存操作将被拒绝；AUTOSAR CP 4.4标准中可能有特定的会话级别要求，需要根据标准进行配置。|
|说明|If there is no reference, no check of session level shall be done.|
|多实例个数|0 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspSession/DcmDspSessionRow|

#### 1.3.13. DcmDspMemoryTransfer

|容器属性|值（容器）|
|---|---|
|名称|DcmDspMemoryTransfer|
|描述|This container contains the configuration of the memory transfer.|
|描述|概述：DcmDspMemoryTransfer配置项是用于定义诊断服务组件（Diagnostic Communication Manager）中内存传输操作的参数，这包括读取、写入和擦除内存操作的相关配置。|
|描述|注意：在配置DcmDspMemoryTransfer时，需要确保内存范围、访问权限和传输协议符合ECU的硬件和软件要求；此外，应当注意内存操作可能对系统的实时性和安全性产生影响，因此需要仔细规划和测试；AUTOSAR CP 4.4标准中可能对内存传输的数据大小、安全访问机制和传输协议有特定的要求或限制，需要遵守这些规范以确保兼容性。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspMemoryTransferUsePort|
|描述|If this parameter is set to true, the Dcm uses a port requiring a PortInterface UploadDownload.|
|描述|概述：DcmDspMemoryTransferUsePort配置项用于指定诊断服务组件（Dcm）在执行内存传输操作时是否使用端口接口。|
|描述|注意：在AUTOSAR CP 4.4标准中，应当确保该配置项与系统中实际使用的内存传输机制相匹配；如果系统设计要求通过端口接口与其他软件组件交互进行内存读写，该选项应配置为启用；反之，如果系统使用直接内存访问方式，则应配置为禁用。|
|说明|If the parameter is false, the DCM uses the according C-API callouts.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspMemoryTransferFnc|
|描述|Function name for memory transfer services.|
|描述|概述：DcmDspMemoryTransferFnc配置项用于定义诊断服务中的内存传输功能，它指定了用于读取、写入和擦除内存的函数指针，以便在诊断会话中执行内存操作。|
|描述|注意：在配置DcmDspMemoryTransferFnc时，需要确保提供的函数指针与实际实现的内存操作函数相匹配；此配置项通常与Dcm的内存映射和安全访问权限设置紧密相关；在AUTOSAR CP 4.4标准中，应当遵循模块的内存和安全管理策略来配置此项，以确保诊断服务的正确性和安全性。|
|说明|Only relevant if DcmDspMemoryTransferUsePort is set to false.|
|多实例个数|0 - 1|

##### 1.3.13.1. DcmDspAddressAndLengthFormatIdentifier

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAddressAndLengthFormatIdentifier|
|描述|This container contains the configuration of the supported AddressAndLengthFormatIdentifiers for memory access.|
|描述|概述：DcmDspAddressAndLengthFormatIdentifier配置项用于定义诊断服务中地址和长度信息的格式，这决定了如何解析从客户端接收到的数据以及如何构建响应消息。|
|描述|注意：在配置此项时，需要确保所选格式与客户端期望的格式一致；格式标识符必须符合ISO 14229标准中定义的规范；在AUTOSAR CP 4.4中，应当检查该配置项是否支持新的或者已经废弃的格式标识符。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSupportedAddressAndLengthFormatIdentifier|
|描述|This parameter defines the supported AddressAndLengthFormatIdentifier of the request message.|
|描述|概述：DcmDspSupportedAddressAndLengthFormatIdentifier配置项用于定义诊断服务处理器（Diagnostic Service Processor）支持的地址和长度格式标识符，这有助于确保诊断请求和响应中的数据格式正确解析和处理。|
|描述|注意：该配置项必须与车辆支持的诊断协议一致；不正确的配置可能导致诊断通信失败；在实现时需考虑诊断请求的多样性和兼容性。|
|多实例个数|1 - inf|
|取值范围|0 - 255|

##### 1.3.13.2. DcmDspMemoryTransferIdInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspMemoryTransferIdInfo|
|描述|Provides the value of memory identifier used to select the desired memory device|
|描述|概述：DcmDspMemoryTransferIdInfo配置项用于定义诊断服务中内存传输操作的标识符信息，这些信息用于支持不同的内存传输请求，如读取内存或写入内存。|
|描述|注意：在配置DcmDspMemoryTransferIdInfo时，需要确保每个内存传输标识符与其对应的内存操作类型、地址范围和权限设置匹配；标识符应唯一，以避免在内存传输服务中的冲突；AUTOSAR CP 4.4标准可能对内存传输的数据大小、对齐和安全访问有特定要求，这些应在配置时考虑。|
|说明|This container contains the configuration of the memory access requested through diagnostic services : RequestDownload, RequestUpload, TransferData, RequestTransferExit|
|多实例个数|1 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspMemoryIdValue|
|描述|Value of the memory device identifier used.|
|描述|概述：DcmDspMemoryIdValue 是用于配置诊断服务组件（Diagnostic Communication Manager）中，内存标识符的值，该值用于区分不同的内存块，如EEPROM、闪存等，以便在执行读写内存服务时能够正确地访问对应的内存区域。|
|描述|注意：在配置DcmDspMemoryIdValue时，需要确保内存标识符的值与实际硬件和ECU内存映射一致；标识符的值应该是唯一的，不应与其他内存块的标识符冲突；在AUTOSAR CP 4.4标准中，应遵循相关的诊断协议标准（如ISO 14229）中对内存标识符的规定。|
|说明|Each DcmDspMemoryIdInfo should have a unique ID. The MemoryIdValue is retrieved from the request messages (RMBA,WMBA,RD,RU,DDDI) according to ISO-14229-1 with the most significant byte of the request parameter memoryAddress.|
|多实例个数|0 - 1|
|取值范围|0 - 255|

#### 1.3.14. DcmDspPeriodicTransmission

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPeriodicTransmission|
|描述|This container contains the configuration (parameters) for Periodic Transmission Scheduler.|
|描述|概述：DcmDspPeriodicTransmission配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的周期性数据传输属性，这包括周期性传输的数据和时间间隔等。|
|描述|注意：在配置周期性传输时，需要确保数据的传输周期符合网络带宽和ECU处理能力的限制；应遵循相关的诊断协议标准，如ISO 14229；在AUTOSAR CP 4.4中，应确保配置与标准中定义的模块和参数兼容。|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspPeriodicTransmissionFastRate|
|描述|This parameter give the transmission rate of the requested periodicDataIdentifiers to be used if the parameter transmissionMode given in the ReadDataByPeriodicID request is equal to 0x03 ("sendAtFastRate"). This parameter value in seconds have to be configured as a multiple of DcmTaskTime.|
|描述|概述：DcmDspPeriodicTransmissionFastRate配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，快速周期性数据传输的速率，即在快速周期性消息传输模式下，ECU发送周期性数据的时间间隔。|
|描述|注意：该配置项的值应当符合车辆网络的带宽和ECU处理能力；过快的传输速率可能导致网络拥塞或ECU处理瓶颈；在配置时需遵循相关诊断协议标准和OEM的具体要求。|
|说明|min: A negative value and zero is not allowed.|
|多实例个数|0 - 1|
|取值范围|1E-4 - 0.255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspPeriodicTransmissionMediumRate|
|描述|This parameter give the transmission rate of the requested periodicDataIdentifiers to be used if the parameter transmissionMode given in the ReadDataByPeriodicID request is equal to 0x02 ("sendAtMediumRate"). This parameter value in seconds have to be configured as a multiple of DcmTaskTime.|
|描述|概述：DcmDspPeriodicTransmissionMediumRate配置项用于定义诊断通信管理（Diagnostic Communication Manager）中，周期性数据传输的中等速率，即在周期性传输控制中，中等速率的数据传输频率。|
|描述|注意：该配置项的值需要根据网络带宽和ECU处理能力合理设置，以避免数据传输过程中的拥堵或丢失；在不同的车辆网络（如CAN、Ethernet等）中，合理的速率设置可能会有所不同，需要根据具体的网络特性进行调整；AUTOSAR CP 4.4标准中对于周期性传输的速率类别进行了定义，但具体数值需要根据实际应用场景和性能要求来确定。|
|说明|min: A negative value and zero is not allowed.|
|多实例个数|0 - 1|
|取值范围|1E-4 - 0.255|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspPeriodicTransmissionSlowRate|
|描述|This parameter give the transmission rate of the requested periodicDataIdentifiers to be used if the parameter transmissionMode given in the ReadDataByPeriodicID request is equal to 0x01 ("sendAtSlowRate"). This parameter value in seconds have to be configured as a multiple of DcmTaskTime.|
|描述|概述：DcmDspPeriodicTransmissionSlowRate配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，慢速速率下的周期性数据传输的时间间隔，通常用于控制车辆诊断时数据更新的频率。|
|描述|注意：该配置项的值应当根据车辆网络的带宽和诊断需求来设置，以确保网络不会因为过高的数据传输频率而过载；在设置时需要考虑到不同诊断会话模式下的数据传输要求，以及可能的诊断策略变化；如果配置的值与实际车辆网络的性能不匹配，可能会导致诊断响应时间延迟或通信失败。|
|说明|min: A negative value and zero is not allowed.|
|多实例个数|0 - 1|
|取值范围|1E-4 - 0.255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspMaxPeriodicDidScheduler|
|描述|Defines the maximum number of periodicDataIdentifiers that can be scheduled concurrently.|
|描述|概述：DcmDspMaxPeriodicDidScheduler配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，最大周期性数据标识符（DID）调度器的数量，这决定了可以同时激活的周期性DID传输的最大数量。|
|描述|注意：在配置时需确保该值不超过ECU处理能力和网络带宽限制；该值应与实际应用中需要支持的周期性DID数量相匹配；超出此配置的周期性DID请求可能会被拒绝或导致系统性能下降。|
|多实例个数|1 - 1|
|取值范围|1 - 255|

#### 1.3.15. DcmDspPid

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPid|
|描述|This container defines the availability of a PID to the DCM.|
|描述|概述：DcmDspPid配置项用于定义诊断服务中的参数标识符（PID），它指定了哪些数据可以通过诊断服务被读取或监控。|
|描述|注意：PID的配置必须符合ISO 14229和ISO 15031标准中的要求；确保PID的唯一性，避免在同一诊断会话中重复配置；在配置PID时，应考虑数据的访问权限和安全级别，以保护敏感信息。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspPidUsed|
|描述|Allow to activate or deactivate the usage of a PID, for multi purpose ECUs|
|描述|概述：DcmDspPidUsed 是一个配置参数，用于指示是否使用了诊断服务组件（Diagnostic Service Component）中的参数标识符（Parameter Identifier，PID）。|
|描述|注意：在配置Dcm模块时，如果需要支持OBD（On-Board Diagnostics）或UDS（Unified Diagnostic Services）中的某些PID，应将此参数设置为true；如果不使用任何PID，则可以设置为false以节省资源；确保配置与实际实现的诊断服务相匹配。|
|说明|true = PID is available false = PID is not available|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspPidService|
|描述|Indicates if a PID is used with service $01 and/or $02|
|描述|概述：DcmDspPidService配置项是用于定义诊断服务组件中的参数标识符（PID）服务的属性，这些服务允许访问车辆的数据，如发动机转速或车速等。|
|描述|注意：在配置DcmDspPidService时，必须确保PID的唯一性和合法性，遵循OBD（On-Board Diagnostics）或制造商特定的诊断协议；配置的数据访问权限应符合安全访问要求，以防止未授权访问；AUTOSAR CP 4.4标准可能对PID服务的实现和配置有特定的要求，需要仔细遵守相关规范。|
|多实例个数|1 - 1|
|默认值|DCM_SERVICE_01|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidIdentifier|
|描述|1 byte Identifier of the PID|
|描述|概述：DcmDspPidIdentifier配置项用于定义诊断服务中的参数标识符（PID），它指定了用于车辆诊断的特定参数ID，这些参数可以通过诊断服务被读取或监控。|
|描述|注意：在配置DcmDspPidIdentifier时，必须确保PID符合ISO 15031-5定义的标准，并且在一个诊断会话中PID的值必须是唯一的；此外，与PID相关联的数据长度和格式应该符合预期的诊断协议要求；在AUTOSAR CP 4.4标准中，如果有新增的属性或者对现有属性有修改，需要确保配置项与标准保持一致。|
|说明|Within each DcmConfigSet all DcmDspPidIdentifier values shall be unique.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidSize|
|描述|Length of a PID in byte(s).|
|描述|概述：DcmDspPidSize配置项用于定义诊断服务中参数标识符（PID）的大小，即PID数据的长度，这对于确保正确解析和响应车辆诊断请求是必要的。|
|描述|注意：在AUTOSAR CP 4.4标准中，PID的大小应当符合诊断服务的规范要求；不正确的PID大小可能导致诊断通信失败或数据解析错误；在配置PID大小时，还需考虑与相关诊断请求和响应消息格式的兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.3.15.1. DcmDspPidData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidData|
|描述|This container defines the parameter for a Signal in the PID.|
|描述|概述：DcmDspPidData配置项用于定义诊断服务中参数标识符（PID）的数据属性，包括PID的长度、格式和存储位置，确保正确解析和响应PID请求。|
|描述|注意：在配置DcmDspPidData时，必须确保PID的长度和格式与实际应用中的数据匹配；PID数据的存储位置应指向有效的内存或数据结构；AUTOSAR CP 4.4标准可能对PID的最大长度和支持的数据类型有具体要求，需要仔细核对。|
|多实例个数|1 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidByteOffset|
|描述|This is the position in bytes of the PID structure and will not start at position 0 in case a support information is available (for packeted PIDs).|
|描述|概述：DcmDspPidByteOffset配置项用于定义在诊断服务中，特定PID（Parameter Identifiers）数据的字节偏移量，确保数据能够被正确地解析和访问。|
|描述|注意：该配置项的设置必须确保与实际PID数据结构的布局一致，避免数据解析错误；在配置多个PID时，需要注意各PID之间的字节偏移量设置不应该产生重叠；AUTOSAR CP 4.4标准中未对此配置项的具体属性做出特别限制，但实际应用时应根据具体的诊断需求和数据结构进行准确配置。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidDataByteSize|
|描述|Defines the array length in bytes or the the maximum array length for variable datalengths.|
|描述|概述：DcmDspPidDataByteSize配置项用于定义诊断服务中参数标识符（PID）的数据字节大小，这决定了PID数据的长度，是诊断通信中重要的配置。|
|描述|注意：在配置DcmDspPidDataByteSize时，必须确保其大小与实际PID所需的数据长度一致；超出或不足的数据字节大小可能导致诊断响应不正确；此外，该配置项应符合诊断标准和车辆制造商的具体要求。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

###### 1.3.15.1.1. DcmDspPidDataSupportInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidDataSupportInfo|
|描述|This container defines the supported information.|
|描述|概述：DcmDspPidDataSupportInfo配置项用于定义诊断服务中参数标识符（PID）的支持信息，包括PID是否被支持以及如何读取PID的数据。|
|描述|注意：在配置DcmDspPidDataSupportInfo时，需要确保PID符合车辆制造商的诊断需求；对于不支持的PID，应明确标记以避免诊断工具错误识别；配置信息应与ECU支持的实际能力相匹配，避免诊断通信中的数据不一致问题。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidDataSupportInfoBit|
|描述|Referenced Bit of the SupportInfo|
|描述|概述：DcmDspPidDataSupportInfoBit配置项用于决定在诊断服务中，特定的PID（Parameter Identifiers）是否支持数据流的“支持信息位”。这通常用于指示一个数据标识符是否可用于车辆的诊断数据流。|
|描述|注意：在配置DcmDspPidDataSupportInfoBit时，需要确保它与车辆支持的PID列表相匹配；此配置项的设置必须符合OBD（On-Board Diagnostics）要求，如果适用；在AUTOSAR CP 4.4标准中，应当遵循相关的诊断协议标准，如ISO 15031-5或ISO 14229-1，以确保兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspPidDataSupportInfoRef|
|描述|Reference to DcmDspPidSupportInfo|
|描述|概述：DcmDspPidDataSupportInfoRef是一个配置项，用于引用支持特定诊断服务标识符（PID）的数据元素的信息，以便在诊断通信中正确处理和响应PID请求。|
|描述|注意：确保引用的数据元素信息与实际支持的PID匹配，以保证诊断服务的正确性；在配置时需注意数据元素的访问权限和安全级别，以满足诊断安全要求；该配置项在AUTOSAR CP 4.4中应与诊断服务的需求和实现紧密相关，确保配置的一致性和准确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspPid/DcmDspPidSupportInfo|

###### 1.3.15.1.2. DcmDspPidService01

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidService01|
|描述|Contains specific configuration parameter of PID for service $01. This container exists only if DcmDspPidService is set to DCM_SERVICE_01 or DCM_SERVICE_01_02.|
|描述|概述：DcmDspPidService01配置项是用于定义诊断服务$01（读取数据流）中的参数标识符（PID），它指定了哪些数据应当被读取并返回给诊断工具。|
|描述|注意：在配置DcmDspPidService01时，需要确保PID符合车辆制造商的要求以及相关法规标准；PID的数据类型和长度必须与ECU提供的数据匹配；在配置过程中，还需注意PID之间的依赖关系和数据一致性。|
|多实例个数|0 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspPidDataEndianness|
|描述|Defines the endianness of the data belonging to a PID in a diagnostic response message.|
|描述|概述：DcmDspPidDataEndianness配置项用于定义诊断服务中参数标识符（PID）数据的字节序，确保数据的正确解析和交换。|
|描述|注意：在配置时需确保字节序与ECU内部数据处理的字节序一致；不同平台间的数据交换可能需要考虑字节序转换；AUTOSAR CP 4.4标准支持大端和小端字节序，但具体选择应基于目标平台和应用需求。|
|说明|If no DcmDspPidDataEndianness is defined the value of DcmDspDataDefaultEndianness is applicable.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspPidDataType|
|描述|Provide the implementation data type of data belonging to a PID.|
|描述|概述：DcmDspPidDataType用于定义诊断服务中参数标识符（PID）的数据类型，这有助于确保数据的正确解释和处理。|
|描述|注意：在配置DcmDspPidDataType时，必须确保所选数据类型与PID的实际数据格式相匹配；不正确的数据类型配置可能导致数据解析错误或通信故障；AUTOSAR CP 4.4标准中对于诊断数据类型有明确的规范，需要遵循这些规范以保证兼容性。|
|多实例个数|1 - 1|
|默认值|UINT8_N|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspPidDataUsePort|
|描述|If this parameter is set to USE_DATA_SYNCH_FNC, the Dcm will use the function defined in DcmDspPidDataReadFnc to get the PID data value.|
|描述|概述：DcmDspPidDataUsePort配置项指定了诊断服务组件（Diagnostic Service Component）中，用于处理特定PID（Parameter Identifiers）数据的端口类型，决定了数据如何从软件组件中获取。|
|描述|注意：在AUTOSAR CP 4.4标准中，必须确保端口类型与实际的软件组件接口匹配；端口类型的选择会影响数据访问的实现方式和性能；不正确的端口配置可能导致诊断服务无法正确访问所需数据。|
|说明|If this parameter is set to USE_DATA_SYNCH_CLIENT_SERVER, the Dcm will have an R-Port requiring the interface DataServices_{Data}. If this parameter is set to USE_DATA_SENDER_RECEIVER or USE_DATA_SENDER_RECEIVER_AS_SERVICE, the DCM will have an R-Port requiring a SenderReceiverInterface. The R-Port is named DataServices_{Data} where {Data} is the name of the container DcmDspPidData.|
|多实例个数|1 - 1|
|默认值|USE_DATA_SYNCH_CLIENT_SERVER|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspPidDataReadFnc|
|描述|Function name for reading PID data value.|
|描述|概述：DcmDspPidDataReadFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，用于读取特定参数标识符（Parameter Identifier, PID）数据的函数名称。|
|描述|注意：函数名称应遵循AUTOSAR命名规范，确保与实际实现的函数名一致；该函数需要符合AUTOSAR规定的接口和行为模式，以确保正确的数据读取和错误处理；在配置时需注意PID数据的安全访问，防止未授权的数据读取。|
|说明|This is only relevant if DcmDspPidDataUsePort==USE_DATA_SYNCH_FNC. This parameter is related to the interface Xxx_ReadData.|
|多实例个数|0 - 1|

####### 1.3.15.1.2.1. DcmDspDiagnosisScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspDiagnosisScaling|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|描述|概述：DcmDspDiagnosisScaling配置项用于定义诊断服务中数据缩放的参数，这些参数决定了如何将内部数据值转换为对外报告的诊断值，或者反之，如何将诊断值转换回内部数据值。|
|描述|注意：在配置DcmDspDiagnosisScaling时，需要确保缩放算法与实际应用场景相匹配；缩放参数必须与相关的数据类型和诊断需求一致；在AUTOSAR CP 4.4标准中，应当遵循相关规范来配置这些参数，以保证诊断服务的正确性和互操作性。|
|多实例个数|0 - 1|

######## 1.3.15.1.2.1.1. DcmDspAlternativeDataInterface

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataInterface|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a VariableDataPrototoype in a DataInterface.|
|描述|概述：DcmDspAlternativeDataInterface配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，备选数据接口的属性，这些接口用于读取或写入数据，当标准数据接口不可用时。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保备选数据接口的配置与系统中实际可用的备选接口相匹配；备选数据接口应当仅在标准接口无法满足需求时使用；配置时需注意备选接口的权限和安全性要求，以防止未授权访问。|
|说明|Additionally a reference to PortInterfaceMapping can be defined which provide already the mapping rules between the VariableDataPrototoype in a DataInterface used by the software component (DcmDspExternalSRDataElementClass) and the intended Diagnosis Representation defined by DcmDataElement.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a VariableDataPrototoype in a DataInterface.|
|说明|The CompuMethod of the data type of the referenced VariableDataPrototype will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|VARIABLE-DATA-PROTOTYPE|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmPortInterfaceMapping|
|描述|Optional reference to PortInterfaceMapping which defines the mapping rules.|
|描述|概述：DcmPortInterfaceMapping用于定义诊断通信管理器（Diagnostic Communication Manager）与软件组件之间的接口映射，确保诊断请求能够正确地传递给相应的软件组件进行处理。|
|描述|注意：在配置DcmPortInterfaceMapping时，需要确保映射关系的正确性和一致性，避免诊断请求无法正确处理；此配置项对于实现车辆诊断功能至关重要，应仔细设计和验证；AUTOSAR CP 4.4标准中对诊断功能有详细规定，需遵守相关规范以保证兼容性。|
|说明|The PortInterfaceMapping is used to get the DataPrototypeMapping that describes a conversion between the data prototype referenced by DcmDataElement and the data prototype referenced from DcmDspExternalSRDataElementClass.|
|多实例个数|0 - 1|
|目标类型|PORT-INTERFACE-MAPPING|

######## 1.3.15.1.2.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

######### 1.3.15.1.2.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######## 1.3.15.1.2.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

####### 1.3.15.1.2.2. DcmDspPidService01ExternalSRDataElementClass

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidService01ExternalSRDataElementClass|
|描述|This container defines the source of data in a provided port which shall be read respectively the target of data in a required port which shall be written.|
|描述|概述：DcmDspPidService01ExternalSRDataElementClass配置项用于定义诊断服务$01（读取数据流）中外部信号表示的数据元素类别，这些数据元素通常来源于车辆信号或传感器，并且可以通过服务$01被读取。|
|描述|注意：在配置DcmDspPidService01ExternalSRDataElementClass时，需要确保引用的数据元素与实际的车辆信号或传感器数据一致；此外，还需注意数据元素的访问权限和安全级别设置，以确保数据的安全性；AUTOSAR CP 4.4标准可能对数据元素的类型和大小有特定要求，因此在配置时应参照标准文档以保证兼容性。|
|说明|This container shall contain either one DcmSubElementInDataElementInstance OR DcmDataElementInstance OR DcmSubElementInImplDataElementInstance reference.|
|多实例个数|0 - 1|

######## 1.3.15.1.2.2.1. DcmDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmDataElementInstance|
|描述|Instance Reference to the primitive data in a port where the data element is typed with an ApplicationPrimitveDataType or an ImplementationDataType.|
|描述|概述：DcmDataElementInstance配置项用于定义诊断数据元素的实例，它指定了数据元素在诊断服务中的具体实现，如数据源和数据大小。|
|描述|注意：在配置DcmDataElementInstance时，需要确保数据元素的类型、大小和对齐方式符合AUTOSAR标准和ECU的内存映射要求；数据元素的访问权限应与诊断服务的安全级别相匹配；在配置数据元素时，还应考虑到数据的实时性和一致性要求。|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmDataElementInstanceRef|
|描述|Instance Reference to the primitive or array data which shall be read or written.|
|描述|概述：DcmDataElementInstanceRef配置项用于引用诊断数据元素实例，它指定了诊断服务中使用的具体数据元素，如车辆速度或引擎转速。|
|描述|注意：在配置DcmDataElementInstanceRef时，需要确保引用的数据元素与诊断服务的需求相匹配；引用的数据元素必须在系统中定义且可访问；在配置过程中，还需注意数据元素的访问权限和安全级别设置，以确保数据的保护和合规性。|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ApplicationPrimitiveDataType of category VALUE or BOOLEAN or ApplicationArrayDataType or if the AutosarDataPrototype is typed with a ImplementationDataType of category VALUE, ARRAY or TYPE_REFERENCE that in turn boils down to VALUE or ARRAY|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE|
|目标类型|AUTOSAR-DATA-PROTOTYPE|

######## 1.3.15.1.2.2.2. DcmSubElementInDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmSubElementInDataElementInstance|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port where the data element is typed with an ApplicationCompositeDataType.|
|描述|概述：DcmSubElementInDataElementInstance配置项用于定义诊断数据元素实例中的子元素，这些子元素可以是基本数据类型或者更复杂的数据结构，用于支持复杂的诊断通信需求。|
|描述|注意：在定义子元素时，必须确保其数据类型与父数据元素兼容；子元素的顺序可能会影响诊断消息的解析和构造，因此需要仔细规划；此配置项在AUTOSAR CP 4.4中可能受到严格的数据封装和接口规范的约束。|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmSubElementInDataElementInstanceRef|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port which shall be read.|
|描述|概述：DcmSubElementInDataElementInstanceRef配置项用于定义诊断数据元素实例中子元素的引用，它指定了子元素在父数据元素中的位置，以便于在诊断通信中正确解析和访问这些子元素。|
|描述|注意：在配置子元素引用时，需要确保引用的有效性和正确性，以免在诊断通信过程中出现数据不一致；子元素的定义必须与实际的数据结构相匹配，遵循AUTOSAR标准中对数据元素的规定；在多层嵌套的数据结构中，正确地识别和配置每个子元素的路径是关键，以确保诊断服务的准确性。|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ApplicationCompositeDataType.|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE AUTOSAR-DATA-PROTOTYPE APPLICATION-COMPOSITE-ELEMENT-DATA-PROTOTYPE\*|
|目标类型|APPLICATION-COMPOSITE-ELEMENT-DATA-PROTOTYPE|

######## 1.3.15.1.2.2.3. DcmSubElementInImplDataElementInstance

|容器属性|值（容器）|
|---|---|
|名称|DcmSubElementInImplDataElementInstance|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port where the data element is typed with an ImplementationDataType.|
|描述|概述：DcmSubElementInImplDataElementInstance配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中实现数据元素实例的子元素，这些子元素是实现数据元素的一部分，用于处理车辆诊断过程中的数据交换。|
|描述|注意：在配置DcmSubElementInImplDataElementInstance时，需要确保子元素与其父实现数据元素之间的关系正确无误；子元素的数据类型和大小必须与其在诊断数据标识符中定义的类型和大小相匹配；在配置过程中，应遵循AUTOSAR规范中关于诊断数据元素的定义和约束。|
|多实例个数|0 - 1|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmSubElementInImplDataElementInstanceRef|
|描述|Instance Reference to the primitve sub-element (at any level) of composite data in a port which shall be read.|
|描述|概述：DcmSubElementInImplDataElementInstanceRef 用于引用实现数据元素中的子元素，这有助于在诊断通信管理模块中精确地定位和处理数据。|
|描述|注意：确保引用的子元素在实现数据元素中正确定义和存在；在配置时应遵循AUTOSAR的数据引用规则，以保证数据的一致性和正确性；在多层嵌套的数据结构中，路径引用需要特别小心以避免错误。|
|说明|Supported are VariableDataPrototypes in SenderReceiverInterfaces and NvDataInterfaces and ParameterDataPrototypes in ParameterInterfaces (read only). This reference is applicable if the AutosarDataPrototype is typed with a ImplementationDataType of category STRUCTURE or ARRAY. Please note that in case of ARRAY the index attribute in the target reference has to be set to select a single array element.|
|多实例个数|1 - 1|
|目标上下文|ROOT-SW-COMPOSITION-PROTOTYPE SW-COMPONENT-PROTOTYPE PORT-PROTOTYPE AUTOSAR-DATA-PROTOTYPE IMPLEMENTATION-DATA-TYPE-ELEMENT\*|
|目标类型|IMPLEMENTATION-DATA-TYPE-ELEMENT|

###### 1.3.15.1.3. DcmDspPidService02

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidService02|
|描述|Contains specific configuration parameter of PID for service $02. This container exists only if DcmDspPidService is set to DCM_SERVICE_02 or DCM_SERVICE_01_02.|
|描述|概述：DcmDspPidService02配置项用于定义诊断服务02（读取当前数据）中的参数标识符（PID）的处理方式，包括如何读取数据和响应请求。|
|描述|注意：确保配置的PID符合车辆制造商的规范和诊断需求；在配置PID时，应注意数据的安全性和访问权限控制；此配置项应与车辆的实际硬件和软件资源相匹配，以确保正确的数据读取和响应速度。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspPidDataDemRef|
|描述|Reference to DemPidDataElement in DEM configuration. Allows to link the DCM PID and DEM PID configuration for Mode $02.|
|描述|概述：DcmDspPidDataDemRef配置项用于将诊断服务的参数标识符（PID）与数据元素管理（DEM）事件引用关联起来，以便在发生故障时记录和报告相关的故障码。|
|描述|注意：确保每个PID正确地映射到相应的DEM事件，以保证故障诊断的准确性；DEM事件引用必须指向有效的DEM事件ID；在配置时应遵循AUTOSAR DEM模块的标准要求。|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dem/DemConfigSet/DemPidClass/DemPidDataElement|

##### 1.3.15.2. DcmDspPidSupportInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspPidSupportInfo|
|描述|This container defines the support information (typically byte A) to declare the usability of the data bytes within the so-called packeted PIDs (e.g. PID$68).|
|描述|概述：DcmDspPidSupportInfo配置项用于定义诊断服务0x22（读取数据标识符）中支持的参数标识符（PID）及其相关属性，如PID的数据长度、访问权限和是否支持快速信息交换。|
|描述|注意：在配置DcmDspPidSupportInfo时，需要确保PID符合ISO 14229和ISO 15031标准中定义的参数标识符；还需注意PID数据长度的正确性，以及与实际ECU支持的功能匹配；此外，配置时应考虑PID的访问权限设置，确保只有授权用户能够访问敏感或受限的数据。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidSupportInfoLen|
|描述|Length of the support information in bytes.|
|描述|概述：DcmDspPidSupportInfoLen配置项用于定义诊断服务中支持的参数标识符（PID）的支持信息长度，即告诉诊断工具哪些PID是可用的。|
|描述|注意：该配置项的值应当与实际支持的PID数量和格式相匹配；超出实际PID数量的支持信息长度可能会导致诊断工具解析错误；在AUTOSAR CP 4.4标准中，确保该配置项符合诊断通信管理器（Dcm）模块的规范要求。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspPidSupportInfoPos|
|描述|Position of the support information in bytes.|
|描述|概述：DcmDspPidSupportInfoPos配置项用于定义在诊断服务中，特定PID（Parameter Identifiers）支持信息的位置，这有助于确定哪些PID是受支持的，以及它们的支持信息如何被组织和访问。|
|描述|注意：在配置DcmDspPidSupportInfoPos时，必须确保其值与实际PID支持信息的存储位置相匹配；此配置项对于确保诊断服务正确识别和处理PID请求至关重要；不正确的配置可能导致诊断服务无法正确响应PID请求。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.3.16. DcmDspReadDTCInformation

|容器属性|值（容器）|
|---|---|
|名称|DcmDspReadDTCInformation|
|描述|This container contains the configuration for the UDS service ReadDTCInformation (0x19).|
|描述|概述：DcmDspReadDTCInformation配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中读取故障诊断代码（DTC）信息的参数和行为，包括支持的读取方式、过滤条件以及返回的信息内容。|
|描述|注意：在配置时需确保所选的读取方式与车辆支持的诊断协议一致；对于返回信息内容的配置，需符合ISO 14229标准中定义的数据结构和格式；在多ECU系统中，应考虑DTC信息的来源和访问权限，避免数据冲突或泄露。|
|多实例个数|0 - 1|

##### 1.3.16.1. DcmDspReadDTCInformationUserDefinedFaultMemory

|容器属性|值（容器）|
|---|---|
|名称|DcmDspReadDTCInformationUserDefinedFaultMemory|
|描述|This container contains the configuration for user defined fault memories in DcmDspReadDTCInformation.|
|描述|概述：DcmDspReadDTCInformationUserDefinedFaultMemory配置项用于定义用户自定义的故障存储器，允许通过诊断服务读取特定的故障码信息。|
|描述|注意：在使用此配置项时，需要确保定义的用户自定义故障存储器与AUTOSAR标准中定义的故障存储器兼容；此配置项可能需要与车辆制造商的特定诊断需求相匹配；在实现时应注意不同制造商可能有不同的实现要求和限制。|
|多实例个数|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspReadDTCInformationUserDefinedFaultMemoryId|
|描述|Identifier used by external tester to identify the User defined event Memory.|
|描述|概述：DcmDspReadDTCInformationUserDefinedFaultMemoryId用于定义用户自定义的故障存储器标识符，允许对特定的故障存储器进行读取故障码（DTC）操作。|
|描述|注意：在配置时需确保标识符的唯一性，避免与标准故障存储器标识符冲突；AUTOSAR CP 4.4标准中未明确列出此配置项，用户需根据实际项目需求谨慎使用；在实现时应考虑与Dcm模块其他配置项的兼容性。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspReadDTCInformationUserDefinedFaultMemoryRole|
|描述|Bitfield were each bit represents one dedicated role. A user defined fault memory is granted access if the bit value is 1. If a bit value is 0, it is not allowed for that role.|
|描述|概述：DcmDspReadDTCInformationUserDefinedFaultMemoryRole配置项用于定义用户自定义的故障存储器角色，这将决定如何处理诊断通信管理器（Dcm）中的读取故障诊断码（DTC）信息服务。|
|描述|注意：在配置用户定义的故障存储器时，需要确保它与AUTOSAR标准中定义的故障存储器类型兼容；此配置项应与Dcm的其他配置参数协同工作，以确保正确的故障码读取行为；在实现时，应注意用户定义的故障存储器角色是否满足特定项目的需求和法规要求。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

#### 1.3.17. DcmDspRequestControl

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestControl|
|描述|This container contains the configuration (parameters) of the "Request control of on-board system, test or component" service (Service $08).|
|描述|概述：DcmDspRequestControl配置项用于定义诊断服务组件（Diagnostic Communication Manager）中请求控制服务的属性，这些属性包括请求控制服务的支持情况、安全性访问级别以及会话控制等。|
|描述|注意：在配置DcmDspRequestControl时，需要确保配置的安全访问级别和会话控制与实际的诊断需求相匹配；此外，AUTOSAR CP 4.4标准可能对支持的服务代码和子功能代码有特定的要求或限制，因此需要根据标准进行配置；最后，确保配置的参数与ECU支持的诊断功能一致，避免因配置错误导致诊断服务无法正常工作。|
|说明|The DCM will request the control using an R-Port requiring a PortInteface RequestControlServices_{Tid}. The R-Port is named RequestControlServices_{Tid} where {Tid} is the name of the container DcmDspRequestControl.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRequestControlInBufferSize|
|描述|Number of bytes to be provided in the input buffer of the interface RequestControlServices_{Tid} for OBD Service $08|
|描述|概述：DcmDspRequestControlInBufferSize配置项用于定义诊断服务处理请求时，输入缓冲区的大小，这个缓冲区用于存储来自诊断测试仪的请求数据。|
|描述|注意：缓冲区大小需要根据实际支持的诊断服务和数据长度来配置，以确保能够处理最大可能的请求；过小的缓冲区可能导致无法处理大的诊断请求，而过大的缓冲区可能会浪费系统资源；在AUTOSAR CP 4.4标准中，应确保该配置项与ECU的内存和处理能力相匹配。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRequestControlInfoByte|
|描述|Manufacturer specific value reported to the tester for the record identifiers 0xE000 to OxE1FF. (WWH-OBD use cases)|
|描述|概述：DcmDspRequestControlInfoByte配置项用于定义诊断服务请求中控制信息字节的属性，这通常包括控制参数的类型和大小，用于控制ECU行为。|
|描述|注意：在配置DcmDspRequestControlInfoByte时，必须确保控制参数的类型和大小符合ECU的实际需求和诊断标准；此配置项的属性应与实际的诊断请求匹配，避免诊断通信中的错误；AUTOSAR CP 4.4标准中对诊断服务的定义非常严格，因此在配置时应仔细参考相关规范文档。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRequestControlOutBufferSize|
|描述|Number of bytes to be provided in the output buffer of the interface RequestControlServices_{Tid} for OBD Service $08|
|描述|概述：DcmDspRequestControlOutBufferSize 定义了诊断控制服务（如重置或控制ECU操作）的输出缓冲区大小，用于存储响应数据。|
|描述|注意：缓冲区大小应足以容纳最大可能的响应数据；过小的缓冲区可能导致数据截断，影响诊断服务的执行；在配置时需考虑ECU的处理能力和响应时间。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRequestControlTestId|
|描述|Test Id for Service $08|
|描述|概述：DcmDspRequestControlTestId用于定义诊断服务中请求控制操作的测试标识符，它指定了在执行控制操作时需要使用的特定测试ID。|
|描述|注意：该标识符必须在Dcm配置中唯一，以确保诊断请求的正确处理；在配置时需遵循ISO 14229标准中定义的服务标识符和参数要求；AUTOSAR CP 4.4中并未对此项进行特殊的修改或限制，但实现时应确保与整体诊断策略和架构兼容。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.3.18. DcmDspRequestFileTransfer

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestFileTransfer|
|描述|This container contains the configuration for RequestFileTransfer.|
|描述|概述：DcmDspRequestFileTransfer配置项用于定义诊断服务中请求文件传输的参数，包括文件传输的模式、内存地址、大小等信息，以支持文件的上传或下载过程。|
|描述|注意：在配置时需确保文件传输请求的参数与实际应用场景相匹配，避免因参数不当导致传输失败；AUTOSAR CP 4.4标准中对文件传输服务的支持可能受限于ECU的硬件能力和网络带宽，需谨慎评估；配置应遵循安全传输原则，确保数据在传输过程中的安全性。|
|说明|This container only exists if RequestFileTransfer is configured.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmRequestFileTransferUsePort|
|描述|Defines if a C/S or C function call shall be used for RequestFileTransfer processing.|
|描述|概述：DcmRequestFileTransferUsePort配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，文件传输请求的使用端口，以便在诊断会话中支持文件的上传或下载功能。|
|描述|注意：该配置项需要与诊断服务的实现紧密配合，确保端口配置正确以支持预期的文件传输操作；在配置时需考虑安全性，确保数据传输过程中的数据保护；此配置项在AUTOSAR CP 4.4标准中未明确列出，用户需参考相关诊断通信服务的配置要求。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmRequestFileTransferFileSizeOrDirInfoParameterLength|
|描述|Defines the length (number of bytes, i.e. the value of fileSizeOrDirInfoParameterLength) of the fileSizeUncompressedOrDirInfoLength and fileSizeCompressed in the response of RequestFileTransfer.|
|描述|概述：DcmRequestFileTransferFileSizeOrDirInfoParameterLength配置项用于定义在文件传输或目录信息请求中，文件大小或目录信息参数的长度。|
|描述|注意：在配置此参数时，需要确保其长度符合实际应用中文件大小或目录信息的表示需求；长度配置应遵循相关诊断协议标准；在AUTOSAR CP 4.4标准中，应检查此参数是否与最新的诊断服务要求保持一致。|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|1 - 4|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmRequestFileTransferLengthFormatIdentifier|
|描述|Defines the length (number of bytes) of the maxNumberOfBlockLength parameter in the response of RequestFileTransfer.|
|描述|概述：DcmRequestFileTransferLengthFormatIdentifier用于定义在诊断通信中，文件传输请求的长度字段的格式，确保文件传输过程中长度信息的准确传递。|
|描述|注意：该配置项的值应根据实际的文件传输协议和需求来设置，以确保兼容性和正确性；在AUTOSAR CP 4.4标准中，需注意与其他诊断服务的兼容性和整体诊断策略的一致性；长度格式标识符的选择直接影响到传输效率和协议的灵活性。|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|1 - 4|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmRequestFileTransferMaxFileAndDirName|
|描述|Defines the maximum size allowed for the FileAndDirName parameter with RTE interfaces used for RequestFileTransfer.|
|描述|概述：DcmRequestFileTransferMaxFileAndDirName配置项定义了在使用诊断通信管理器（Diagnostic Communication Manager）进行文件传输请求时，允许的最大文件和目录名长度。|
|描述|注意：该配置项的值需要根据实际应用场景和系统资源进行合理设置，以避免因名称过长导致的内存溢出或处理失败；超出此长度的文件或目录名将导致文件传输请求被拒绝；在AUTOSAR CP 4.4标准中，确保该配置项的设置符合诊断协议要求。|
|多实例个数|0 - 1|
|默认值|1|
|取值范围|1 - 65535|

#### 1.3.19. DcmDspRoe

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoe|
|描述|Provide the configuration of the ResponseOnEvent mechanism.|
|描述|概述：DcmDspRoe配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的响应式事件（Response On Event）功能，该功能允许在预定义的车辆事件发生时自动触发诊断响应。|
|描述|注意：在配置DcmDspRoe时，必须确保与车辆的事件检测系统兼容；此功能的实现必须遵守相关的安全和隐私标准；AUTOSAR CP 4.4标准中对此功能的支持可能有特定的限制或要求，需要详细查阅标准文档。|
|多实例个数|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspRoeInterMessageTime|
|描述|Provide the minimum time in seconds between two transmissions of ROE event. It is used for the delay between two different consecutive Roe transmissions.|
|描述|概述：DcmDspRoeInterMessageTime配置项用于定义诊断通信中，响应输出扩展(ROE)服务之间消息的最大允许时间间隔。|
|描述|注意：该时间间隔必须足够短，以确保系统能够及时响应ROE服务请求；过长的时间间隔可能导致诊断通信效率降低或超时错误；该配置项的具体值需根据系统性能和网络带宽合理设置。|
|多实例个数|1 - 1|
|取值范围|0 - 5|

##### 1.3.19.1. DcmDspRoeEvent

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoeEvent|
|描述|This container contains a list of all supported Roe eventTypeRecords which are accepted by this ECU.|
|描述|概述：DcmDspRoeEvent配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的响应On事件（Response On Event）功能，它指定了在特定条件下触发的诊断响应事件。|
|描述|注意：ROE功能需要确保ECU支持并且已经激活；在配置ROE事件时，必须确保事件的唯一性和与诊断需求的一致性；AUTOSAR CP 4.4标准中对ROE的支持可能受限于具体的ECU硬件和软件能力，需仔细核对。|
|说明|At most one DcmDspRoeEvent container is allowed to define a DcmDspRoeEventProperties container with the choice DcmDspRoeOnDTCStatusChange.|
|多实例个数|1 - 255|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoeInitialEventStatus|
|描述|Initial Roe status of this RoeEvent|
|描述|概述：DcmDspRoeInitialEventStatus配置项用于定义诊断事件在系统启动时的初始状态，这决定了诊断事件是否在系统启动后立即激活。|
|描述|注意：该配置项的设置对系统的诊断响应行为有直接影响；确保与系统的安全和诊断需求相匹配；在AUTOSAR CP 4.4标准中，该配置项的属性应与系统设计文档中的要求一致，否则可能导致诊断功能不符合预期。|
|多实例个数|1 - 1|
|默认值|DCM_ROE_CLEARED|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoeEventId|
|描述|EventId for a global identification of this ROE event it is used within APIs Dcm_TriggerOnEvent() and the ModeDeclarationGroup.|
|描述|概述：DcmDspRoeEventId配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的响应OnEvent（ROE）功能的事件标识符，这是用于区分不同ROE事件的唯一标识。|
|描述|注意：在配置DcmDspRoeEventId时，必须确保事件标识符的唯一性，以避免在诊断会话中对事件的混淆；此外，ROE事件标识符的范围和分配应符合ISO 14229标准中定义的要求；在AUTOSAR CP 4.4标准中，应当检查与ROE相关的其他配置参数，如DcmDspRoeEventLogic和DcmDspRoeEventWindowTime，以确保ROE功能的正确实现。|
|说明|The ratio Ids should be sequentially ordered beginning with 0 and no gaps in between.|
|多实例个数|1 - 1|
|取值范围|0 - 254|

###### 1.3.19.1.1. DcmDspRoeEventProperties

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoeEventProperties|
|描述|This container contains the properties of Roe eventTypeRecords.|
|描述|概述：DcmDspRoeEventProperties配置项定义了诊断通信管理器（Diagnostic Communication Manager）中响应On Event（ROE）服务的事件属性，包括事件类型、事件窗口时间以及事件记录的相关参数。|
|描述|注意：在配置ROE事件时，需要确保事件类型与诊断需求相匹配；事件窗口时间必须设置在合理范围内，以避免对系统性能造成不利影响；此外，应当注意存储空间的分配，确保事件记录能够被正确保存和处理。|
|说明|In one DcmDspRoeEventProperties container one DcmDspRoeOnDTCStatusChange or DcmDspRoeOnChangeOfDataIdentifier container shall be defined.|
|多实例个数|1 - 1|

####### 1.3.19.1.1.1. DcmDspRoeOnChangeOfDataIdentifier

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoeOnChangeOfDataIdentifier|
|描述|This container contains the eventTypeRecord supported for onChangeOfDataIdentifier eventType.|
|描述|概述：DcmDspRoeOnChangeOfDataIdentifier 用于定义诊断通信管理系统中，当数据标识符发生变化时，如何响应和执行相关的诊断服务。|
|描述|注意：确保数据标识符的变化能够被正确监测和识别；配置应符合车辆制造商的诊断策略和安全要求；在实现时需考虑系统资源和响应时间的优化。|
|多实例个数|0 - 1|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspRoeDidRef|
|描述|Reference to a Did which is watched.|
|描述|概述：DcmDspRoeDidRef配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，与事件相关数据标识符（DID）相关联的参考，这使得在诊断事件发生时能够报告特定的DID。|
|描述|注意：在配置DcmDspRoeDidRef时，需要确保引用的DID已在诊断系统中定义并且有效；此配置项通常与诊断事件管理相关，因此需要与DcmDspRoeEvent配置项协同工作；AUTOSAR CP 4.4标准中对于诊断服务的配置有严格的规范，因此在配置时应遵循标准的要求以确保诊断服务的正确性。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDid|

####### 1.3.19.1.1.2. DcmDspRoeOnDTCStatusChange

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoeOnDTCStatusChange|
|描述|This container contains the eventTypeRecord supported for onDTCStatusChange eventType.|
|描述|概述：DcmDspRoeOnDTCStatusChange配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，当故障诊断码（DTC）的状态发生变化时是否启动响应式事件报告（Response On Event, ROE）功能。|
|描述|注意：该配置项需要确保与车辆的故障管理策略相一致；在实现时需考虑对网络带宽和ECU处理能力的影响；AUTOSAR CP 4.4标准中，对ROE的支持和配置要求可能与早期版本有所不同，需要仔细核对标准文档。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoeDTCStatusMask|
|描述|Value of the relevant DTCStatusMask|
|描述|概述：DcmDspRoeDTCStatusMask配置项用于定义诊断事件记录器（DTC）的状态掩码，这个掩码决定了哪些DTC状态变化会触发响应事件的记录。|
|描述|注意：在配置DcmDspRoeDTCStatusMask时，需要确保掩码与实际应用中需要监控的DTC状态相匹配；AUTOSAR标准可能对可用的DTC状态掩码值有具体要求，需仔细参考相关文档；错误配置可能导致某些DTC状态变化未能正确触发事件记录，影响诊断准确性。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

##### 1.3.19.2. DcmDspRoeEventWindowTime

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoeEventWindowTime|
|描述|This container configures the available EventWindowTime in this Ecu.|
|说明|This container contains a sub-set of EventWindowTimes supported by the Dcm, to limit the Ecu resources.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoeEventWindowTime|
|描述|Value of the EventWindowTime|
|描述|概述：DcmDspRoeEventWindowTime配置项用于定义诊断事件记录功能中，响应事件触发后的时间窗口，在此时间窗口内的事件将被记录或处理。|
|描述|注意：该配置项的时间单位和精度应符合项目具体要求；在配置时需考虑系统的实时性和处理能力，避免设置过长的时间窗口导致系统资源紧张；AUTOSAR CP 4.4标准中对于DcmDspRoeEventWindowTime的具体数值范围没有强制要求，但建议根据实际应用场景合理配置。|
|多实例个数|1 - 1|

#### 1.3.20. DcmDspRoutine

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRoutine|
|描述|This container contains the configuration (parameters) for Routines|
|描述|概述：DcmDspRoutine配置项用于定义诊断服务组件中的例行控制服务，它指定了例行控制服务的属性，如例行控制操作的标识符、支持的子功能以及相关的执行条件。|
|描述|注意：在配置DcmDspRoutine时，需要确保例行控制标识符的唯一性，避免与其他服务或例行控制冲突；根据AUTOSAR标准，应正确配置支持的子功能，如启动、停止、请求结果等；还需注意与实际的硬件和应用层软件的兼容性，确保例行控制操作能够正确执行。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspRoutineUsed|
|描述|Allow to activate or deactivate the usage of a Routine, for multi purpose ECUs|
|描述|概述：DcmDspRoutineUsed配置项用于指定诊断例程是否在诊断通信管理器（Dcm）中被使用，以支持车辆诊断服务中的特定功能。|
|描述|注意：确保只有必要的诊断例程被标记为使用，以优化资源和性能；在配置时需遵循OEM的诊断策略和标准；不正确的配置可能导致诊断服务不可用或行为异常。|
|说明|True = Routine is available False = Routine is not available|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspRoutineUsePort|
|描述|If this parameter is set to true, the DCM uses a port requiring a PortInterface RoutineServices_{RoutineName}.|
|描述|概述：DcmDspRoutineUsePort配置项用于定义诊断服务组件（Dcm）中的诊断例程是否使用端口（Port）与其他软件组件进行通信，以实现特定的诊断功能。|
|描述|注意：在AUTOSAR CP 4.4中，确保当诊断例程需要与其他软件组件交互时，正确配置DcmDspRoutineUsePort为true；如果诊断例程不需要与其他组件交互，则可以将其设置为false以减少系统开销；配置时需考虑诊断例程的实际需求，避免不必要的端口通信开销。|
|说明|The R-Port is named RoutineServices_{RoutineName} where {RoutineName} is the name of the container DcmDspRoutine In that case, the configuration must not provide function names in DcmDspStartRoutineFnc, DcmDspStopRoutineFnc or DcmDspRequestResultsRoutineFnc. If this is false, the DCM expects to find the names of the functions to be used in DcmDspStartRoutineFnc, DcmDspStopRoutineFnc or DcmDspRequestResultsRoutineFnc.|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineIdentifier|
|描述|2 bytes Identifier of the RID|
|描述|概述：DcmDspRoutineIdentifier配置项用于定义诊断服务组件（Diagnostic Communication Manager）中的例程标识符，它关联了特定的诊断例程，允许对车辆的ECU执行特定的测试和操作。|
|描述|注意：在配置DcmDspRoutineIdentifier时，必须确保例程标识符的唯一性，避免与其他诊断例程冲突；应当遵循OEM的诊断规范来分配例程标识符；在实施例程控制时，还需考虑例程的权限管理和安全访问要求。|
|说明|Within each DcmConfigSet all DcmDspRoutineIdentifier values shall be unique.|
|多实例个数|1 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineInfoByte|
|描述|Manufacturer specific value reported to the tester for the record identifiers 0xE000 to OxE1FF. (OBD use cases)|
|描述|概述：DcmDspRoutineInfoByte配置项用于定义诊断例程中的信息字节，这些信息字节用于在执行诊断服务时传递额外的参数或返回状态信息。|
|描述|注意：在配置DcmDspRoutineInfoByte时，需要确保信息字节的定义与实际诊断例程的要求相匹配；此配置项在AUTOSAR CP 4.4中应遵循诊断服务的标准格式和规范；配置错误可能导致诊断通信失败或信息解析错误。|
|多实例个数|0 - 1|
|取值范围|0 - 255|

##### 1.3.20.1. DcmDspRequestRoutineResults

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestRoutineResults|
|描述|Provides the configuration of RequestResult subservice for RoutineControl service.|
|描述|概述：DcmDspRequestRoutineResults配置项用于定义诊断服务处理过程中，如何请求和获取诊断例程的执行结果，这是诊断通信管理（Diagnostic Communication Manager）的一部分。|
|描述|注意：在配置DcmDspRequestRoutineResults时，需要确保诊断例程标识符与实际例程匹配，避免数据不一致；此配置项应与DcmDspRoutine控制选项一起考虑，以确保例程的正确执行和结果获取；AUTOSAR CP 4.4标准中，对于诊断例程结果的请求和报告方式有明确规范，需要遵守这些规范以保证诊断通信的兼容性和准确性。|
|说明|Existence indicates that the RequestRoutineResults in the RoutineControl is supported.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspRequestRoutineResultsConfirmationEnabled|
|描述|Allows to enable/disable the confirmation function to indicate the transmission of a response to a RequestRoutineResults request|
|描述|概述：DcmDspRequestRoutineResultsConfirmationEnabled配置项用于启用或禁用诊断例程结果的确认，这是在执行诊断服务时，用于控制是否需要对例程结果进行确认的配置。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在使用此配置项时，已经根据项目需求和诊断通信需求明确是否需要例程结果确认；此配置项的启用可能会影响诊断响应时间和网络带宽，因此需要谨慎考虑；如果项目中不需要对诊断例程结果进行确认，可以禁用此选项以优化性能。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspRequestRoutineResultsConfirmationFnc|
|描述|C-function to call if a transmission confirmation is needed by the issuer (BSW module)|
|描述|概述：DcmDspRequestRoutineResultsConfirmationFnc 是用于定义诊断服务组件中，请求例行检查结果确认的函数。|
|描述|注意：该函数需要确保能处理从ECU接收到的所有可能的例行检查结果；函数实现应遵循AUTOSAR CP 4.4标准中对诊断服务的安全和时间要求；确保该函数在系统中的唯一性和正确性，避免与其他诊断服务功能冲突。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspRequestRoutineResultsFnc|
|描述|Function name for request to application the results of a routine. (Routine_RequestResults-function)|
|描述|概述：DcmDspRequestRoutineResultsFnc配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，请求例行检查结果的函数名称，该函数负责获取例行诊断检查的结果数据。|
|描述|注意：函数名称应遵循C语言命名规则且不应与现有系统中的其他函数名称冲突；确保该函数实现与AUTOSAR标准中定义的例行诊断结果请求服务的要求一致；在配置时，需要注意与DcmDspRequestRoutineResults的其他属性设置相匹配，以确保正确的服务响应。|
|说明|This parameter is related to the interface Xxx_RequestResults.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRequestRoutineResultsRole|
|描述|Bitfield were each bit represents one dedicated role. A RoutineControl with sub-function requestResults is granted access if the bit value is 1. If a bit value is 0, the routine is not allowed for that role.|
|描述|概述：DcmDspRequestRoutineResultsRole配置项用于定义诊断服务组件（Dcm）中，特定例程请求结果的角色和权限，确保只有授权的客户端可以请求和接收诊断例程的执行结果。|
|描述|注意：在配置时需确保角色与权限设置符合系统安全要求；不同的诊断例程可能需要不同的权限设置，以满足不同安全级别的需求；AUTOSAR CP 4.4标准中对于诊断服务的安全要求较高，需要特别注意权限配置的合规性。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspRequestRoutineResultsCommonAuthorizationRef|
|描述|Reference to DcmDspCommonAuthorization|
|描述|概述：DcmDspRequestRoutineResultsCommonAuthorizationRef 是一个配置项，用于引用授权配置，该配置定义了对诊断例程结果请求的访问权限。|
|描述|注意：在配置时，需要确保引用的授权配置与所需的安全级别相匹配；如果配置了不正确的授权引用，可能会导致安全访问控制不当，从而允许未授权的访问；AUTOSAR CP 4.4标准中，应当遵循相关的安全和访问控制规范来配置此项。|
|说明|Common authorization configuration taken from the referenced DcmDspRequestRoutineResultsCommonAuthorizationRef. If there is no reference, no check on the commonly defined authorization conditions shall be done to get the routine result.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspCommonAuthorization|

###### 1.3.20.1.1. DcmDspRequestRoutineResultsIn

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestRoutineResultsIn|
|描述|Provide description of input parameter of RequestResult subservice for RoutineControl service.|
|描述|概述：DcmDspRequestRoutineResultsIn配置项用于定义诊断服务处理过程中，如何获取和返回例行检查的结果给请求者。|
|描述|注意：在配置DcmDspRequestRoutineResultsIn时，需要确保返回的数据格式和内容符合ISO 14229标准中定义的UDS服务要求；此配置项对于实现诊断例行控制服务（如10 03服务）至关重要，需要精确配置以避免诊断通信错误；AUTOSAR CP 4.4标准中并未对此配置项的属性做出具体的限制或要求，但实现时应考虑与其他诊断服务的兼容性和一致性。|
|多实例个数|0 - 1|

####### 1.3.20.1.1.1. DcmDspRequestRoutineResultsInSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestRoutineResultsInSignal|
|描述|Provides description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspRequestRoutineResultsInSignal配置项用于定义诊断服务组件（Dcm）中，请求例行检查结果时所使用的信号，这些信号用于从ECU获取例行检查的结果数据。|
|描述|注意：在配置此项时，必须确保信号与ECU中例行检查结果的数据格式和长度相匹配；此配置项应与DcmDspRequestRoutineResults接口一致，以确保正确的数据交换；在配置过程中，还应注意信号的更新频率和访问权限，以满足实时性和安全性要求。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataIn_n elements in the XXX_RequestResult function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine In Signal for RequestResult subfunction.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|说明|The position is defined in bits.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.1.1.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

######### 1.3.20.1.1.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.1.1.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.1.1.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.1.1.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

###### 1.3.20.1.2. DcmDspRequestRoutineResultsOut

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestRoutineResultsOut|
|描述|Provide description of output parameter of RequestResult subservice for RoutineControl service.|
|描述|概述：DcmDspRequestRoutineResultsOut配置项用于定义诊断服务组件（Diagnostic Communication Manager）中请求例行控制结果输出的参数，这涉及到UDS服务的例行控制功能，特别是服务$31的子功能"请求结果"。|
|描述|注意：在配置DcmDspRequestRoutineResultsOut时，需要确保其与例行控制操作的其他参数和设置相匹配；此配置项应与车辆制造商的诊断需求和规范一致；AUTOSAR CP 4.4标准中对于诊断服务的配置应遵循标准的数据结构和参数定义，以确保诊断通信的正确性和互操作性。|
|多实例个数|0 - 1|

####### 1.3.20.1.2.1. DcmDspRequestRoutineResultsOutSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspRequestRoutineResultsOutSignal|
|描述|Provides description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspRequestRoutineResultsOutSignal 用于定义诊断服务中请求例程结果的输出信号，这些信号用于通知外部设备或系统例程的执行结果。|
|描述|注意：确保信号与ECU的实际输出能力相匹配；在设计时考虑信号的实时性和可靠性；遵循AUTOSAR CP 4.4标准中对诊断信号的具体要求和格式。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataOutN elements in the XXX_RequestResult function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine Out Signal for RequestResult subfunction.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|说明|The position is defined in bits.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.1.2.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

######### 1.3.20.1.2.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.1.2.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.1.2.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.1.2.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

##### 1.3.20.2. DcmDspStartRoutine

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStartRoutine|
|描述|Provides the configuration of Start subservice for RoutineControl service.|
|描述|概述：DcmDspStartRoutine配置项用于定义诊断服务组件中启动例程的参数，包括例程标识符、例程选项和例程状态管理等，以支持对车辆控制单元进行诊断和配置。|
|描述|注意：在配置DcmDspStartRoutine时，必须确保例程标识符的唯一性，避免与其他诊断例程冲突；根据AUTOSAR CP 4.4标准，需要正确配置例程的权限和安全访问级别，以保证只有授权的诊断会话能够启动特定例程；此外，对于支持异步执行的例程，应正确处理例程执行状态和结果报告，以避免诊断通信中的数据不一致。|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspStartRoutineConfirmationEnabled|
|描述|Allows to enable/disable the confirmation function to indicate the transmission of a response to a StartRoutine request|
|描述|概述：DcmDspStartRoutineConfirmationEnabled 是一个配置项，用于确定是否启用诊断服务组件（Diagnostic Service Component）中的启动例行控制操作的确认响应。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保此配置项与诊断例行控制需求相匹配；如果不需要确认响应，可以禁用以节省资源；正确配置此项对于满足诊断通信规范至关重要。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspStartRoutineConfirmationFnc|
|描述|C-function to call if a transmission confirmation is needed by the issuer (BSW module)|
|描述|概述：DcmDspStartRoutineConfirmationFnc配置项用于定义诊断服务组件（Diagnostics Communication Manager）中启动例程确认函数的名称，该函数用于确认启动例程是否成功执行。|
|描述|注意：函数名称需要遵循C语言命名规则且不应与其他函数名冲突；确保该函数实现与AUTOSAR标准中定义的启动例程确认函数的接口一致；在配置时需注意与DcmDspStartRoutine函数的配合使用，以确保例程控制逻辑的正确性。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspStartRoutineFnc|
|描述|Function name for request to application to start a routine. (Routine_Start-function)|
|描述|概述：DcmDspStartRoutineFnc配置项用于定义诊断服务中启动例程的函数，这是在诊断会话中执行特定服务例程的入口点。|
|描述|注意：确保该函数与实际的硬件或软件服务例程兼容；在配置时应遵循AUTOSAR CP 4.4的标准接口规范；在多任务环境中，注意该函数的执行时间和资源竞争问题。|
|说明|This parameter is related to the interface Xxx_Start.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspStartRoutineRole|
|描述|Bitfield were each bit represents one dedicated role. A RoutineControl with sub-function startRoutine is granted access if the bit value is 1. If a bit value is 0, the routine is not allowed for that role.|
|描述|概述：DcmDspStartRoutineRole配置项用于定义诊断服务组件（Diagnostic Communication Manager）中启动例程的角色，它指定了例程控制服务（RoutineControl）中启动例程的功能和行为。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保DcmDspStartRoutineRole的配置与例程控制请求的实际需求相匹配；例程的角色应当与实际的车辆控制策略和诊断需求一致；在配置时，应注意与其他诊断例程的角色配置不冲突，以保证诊断服务的正确执行。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspStartRoutineCommonAuthorizationRef|
|描述|Reference to DcmDspCommonAuthorization|
|描述|概述：DcmDspStartRoutineCommonAuthorizationRef 是一个配置项，用于引用在启动诊断例程之前必须满足的授权条件，以确保只有在得到适当授权后才能执行诊断服务。|
|描述|注意：在配置时，必须确保引用的授权条件已经定义在系统中；授权机制应与安全访问需求相匹配，以防止未授权的访问；在AUTOSAR CP 4.4标准中，如果该配置项的属性或使用方式与标准不一致，需要检查并更新以确保符合标准要求。|
|说明|Common authorization configuration taken from the referenced DcmDspStartRoutineCommonAuthorizationRef. If there is no reference, no check on the commonly defined authorization conditions shall be done to start the routine.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspCommonAuthorization|

###### 1.3.20.2.1. DcmDspStartRoutineIn

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStartRoutineIn|
|描述|Provide description of input parameter of Start subservice for RoutineControl service|
|描述|概述：DcmDspStartRoutineIn配置项用于定义诊断服务中启动例行控制操作的输入参数，这些参数指定了例行控制服务（RoutineControl）的启动条件和所需数据。|
|描述|注意：在配置DcmDspStartRoutineIn时，必须确保输入参数与例行控制服务的要求相匹配；参数类型和大小应符合AUTOSAR标准和具体例行控制服务的定义；在多例行控制服务中，应注意不同服务的输入参数可能会有不同的配置需求。|
|多实例个数|0 - 1|

####### 1.3.20.2.1.1. DcmDspStartRoutineInSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStartRoutineInSignal|
|描述|Provide description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspStartRoutineInSignal配置项用于定义启动诊断例程时的输入信号，它指定了在启动诊断服务例程时需要传递给例程的输入参数。|
|描述|注意：在配置DcmDspStartRoutineInSignal时，需要确保信号的数据类型、大小和格式与例程的输入参数要求相匹配；此配置项通常与DcmDspRoutineInfo相关联，需要保证它们之间的一致性；在配置过程中，还应注意AUTOSAR标准中对服务例程输入信号的任何特定要求或限制。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataInN elements in the XXX_Start function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine In Signal for Start subfunction.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|说明|The position is defined in bits.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.2.1.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

######### 1.3.20.2.1.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.2.1.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.2.1.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.2.1.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

###### 1.3.20.2.2. DcmDspStartRoutineOut

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStartRoutineOut|
|描述|Provide description of output parameter of Start subservice for RoutineControl service.|
|描述|概述：DcmDspStartRoutineOut配置项用于定义诊断服务中启动例程的输出参数，它指定了在执行启动例程服务（如ECU重置或激活某些操作）后返回给客户端（通常是诊断工具）的数据。|
|描述|注意：在配置DcmDspStartRoutineOut时，必须确保输出参数与实际启动例程的预期输出匹配；对于不同的启动例程，可能需要配置不同的输出参数；AUTOSAR CP 4.4标准中对诊断服务的参数有详细规范，需要遵守这些规范以确保诊断服务的兼容性和正确性。|
|多实例个数|0 - 1|

####### 1.3.20.2.2.1. DcmDspStartRoutineOutSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStartRoutineOutSignal|
|描述|Provide description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspStartRoutineOutSignal 用于定义诊断服务中启动例程的输出信号，这些信号用于向客户端报告例程的执行结果。|
|描述|注意：确保输出信号与诊断例程的实际功能和预期输出一致；在配置时需考虑信号的数据类型和范围，以确保正确的数据传输；在AUTOSAR CP 4.4中，应遵循标准的诊断信号配置规范。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataOutN elements in the XXX_Start function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine Out Signal for Start subfunction.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|说明|The position is defined in bits.|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.2.2.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

######### 1.3.20.2.2.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.2.2.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.2.2.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.2.2.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

##### 1.3.20.3. DcmDspStopRoutine

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStopRoutine|
|描述|Provides the configuration of Stop subservice for RoutineControl service.|
|描述|概述：DcmDspStopRoutine配置项用于定义诊断服务组件（Diagnostic Communication Manager）中的停止例程服务，它指定了当接收到停止例程请求时，应该执行的函数或操作。|
|描述|注意：在配置DcmDspStopRoutine时，需要确保引用的停止例程与实际的诊断需求和功能实现相匹配；还需注意与DcmDspStartRoutine和DcmDspRequestResultRoutine的配置一致性，以确保例程控制服务的完整性；此外，应考虑例程执行的权限管理，确保只有授权的诊断会话和安全访问级别可以执行停止例程。|
|说明|Existence indicates that the StopRoutine in the RoutineControl is supported.|
|多实例个数|0 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspStopRoutineConfirmationEnabled|
|描述|Allows to enable/disable the confirmation function to indicate the transmission of a response to a StopRoutine request|
|描述|概述：DcmDspStopRoutineConfirmationEnabled 是一个配置项，用于确定是否启用诊断例程（Routine）停止操作的确认响应，这通常用于确保例程被正确停止。|
|描述|注意：在AUTOSAR CP 4.4标准中，此配置项应当与诊断例程的需求和实现保持一致；如果例程停止操作不需要额外的确认，可能不需要启用此选项；在配置时应考虑与客户端的交互和诊断通信流程的一致性。|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspStopRoutineConfirmationFnc|
|描述|C-function to call if a transmission confirmation is needed by the issuer (BSW module)|
|描述|概述：DcmDspStopRoutineConfirmationFnc配置项用于定义诊断服务中停止例程确认函数的属性，这是在执行诊断例程停止操作后用于确认操作成功与否的函数。|
|描述|注意：确保该函数能正确处理所有可能的停止例程结果，并返回适当的诊断响应码；该函数的实现必须符合AUTOSAR CP 4.4标准中对诊断服务的要求；在多核或多任务环境中，注意该函数的线程安全和重入性。|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspStopRoutineFnc|
|描述|Function name for request to application to stop a routine. (Routine_Stop-function)|
|描述|概述：DcmDspStopRoutineFnc配置项用于定义诊断服务中用于停止诊断例程的函数指针，该函数在例程控制服务请求停止例程时被调用。|
|描述|注意：确保所引用的函数符合AUTOSAR标准中对停止诊断例程的要求；函数需要能够安全地停止例程并返回正确的诊断响应；在配置时，应注意与DcmDspStartRoutineFnc和DcmDspRequestResultRoutineFnc的关联性和一致性。|
|说明|This parameter is related to the interface Xxx_Stop.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspStopRoutineRole|
|描述|Bitfield were each bit represents one dedicated role. A RoutineControl with sub-function stopRoutine is granted access if the bit value is 1. If a bit value is 0, the routine is not allowed for that role.|
|描述|概述：DcmDspStopRoutineRole配置项定义了诊断服务中停止例程的角色和行为，用于控制和管理车辆诊断过程中的特定服务例程的停止操作。|
|描述|注意：在配置DcmDspStopRoutineRole时，需要确保其与例程标识符（Routine Identifier）匹配，以便正确实现停止例程的功能；此配置项在AUTOSAR CP 4.4中应遵循诊断例程管理规范，确保诊断通信管理逻辑的一致性；配置时还需考虑与其他诊断服务的交互和依赖关系，避免潜在的服务冲突。|
|多实例个数|0 - 1|
|取值范围|0 - 4294967295|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmDspStopRoutineCommonAuthorizationRef|
|描述|Reference to DcmDspCommonAuthorization|
|描述|概述：DcmDspStopRoutineCommonAuthorizationRef配置项用于引用授权方法，这些方法用于在执行诊断停止例程前验证是否有权限执行该操作。|
|描述|注意：确保引用的授权方法与实际的安全需求相匹配；在配置时需注意引用的授权方法必须已在系统中定义；不正确的授权配置可能导致安全风险。|
|说明|Common authorization configuration taken from the referenced DcmDspStopRoutineCommonAuthorizationRef. If there is no reference, no check on the commonly defined authorization conditions shall be done to stop the routine.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspCommonAuthorization|

###### 1.3.20.3.1. DcmDspStopRoutineIn

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStopRoutineIn|
|描述|Provide description of input parameter of Stop subservice for RoutineControl service.|
|描述|概述：DcmDspStopRoutineIn配置项用于定义诊断服务中停止例程的输入参数，确保正确的参数被传递以执行停止操作。|
|描述|注意：输入参数应与相应的服务文档或标准一致；参数类型和长度必须正确配置以避免数据解析错误；在AUTOSAR CP 4.4中，确保该配置项的使用符合诊断通信管理器（DCM）模块的规范要求。|
|多实例个数|0 - 1|

####### 1.3.20.3.1.1. DcmDspStopRoutineInSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStopRoutineInSignal|
|描述|Provide description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspStopRoutineInSignal配置项用于定义诊断服务中停止例程的信号，它指定了在执行停止例程操作时，哪些信号应当被发送给ECU以停止相应的诊断例程。|
|描述|注意：在配置DcmDspStopRoutineInSignal时，必须确保信号与所需停止的诊断例程匹配且符合ECU的处理能力；此配置项对于实现诊断服务的正确性至关重要，错误的配置可能导致诊断例程无法正确停止；AUTOSAR CP 4.4标准中对于诊断例程的信号处理有明确规范，需要确保配置符合标准要求。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataInN elements in the XXX_Stop function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine In Signal for Stop subfunction.|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|说明|The position is defined in bits.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.3.1.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|多实例个数|0 - 1|

######### 1.3.20.3.1.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.3.1.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.3.1.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.3.1.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

###### 1.3.20.3.2. DcmDspStopRoutineOut

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStopRoutineOut|
|描述|Provide description of output parameter of Stop subservice for RoutineControl service.|
|描述|概述：DcmDspStopRoutineOut配置项用于定义诊断服务中停止例程的输出参数，这些参数用于控制和监视停止例程的执行。|
|描述|注意：在配置DcmDspStopRoutineOut时，必须确保输出参数与ECU支持的停止例程相匹配；此配置项应与DcmDspStopRoutine相关配置一致，以确保正确的例程控制；在AUTOSAR CP 4.4中，确保使用正确的数据类型和长度以符合标准的要求。|
|多实例个数|0 - 1|

####### 1.3.20.3.2.1. DcmDspStopRoutineOutSignal

|容器属性|值（容器）|
|---|---|
|名称|DcmDspStopRoutineOutSignal|
|描述|Provide description of a routine signal used in RoutineControl service.|
|描述|概述：DcmDspStopRoutineOutSignal配置项用于定义诊断服务中停止例程输出信号的属性，这些属性包括信号的标识符、大小和字节顺序等。|
|描述|注意：在配置DcmDspStopRoutineOutSignal时，需要确保信号的标识符与ECU中实际信号的标识符相匹配；信号大小和字节顺序必须与ECU中信号的实际定义一致；此外，应当注意该配置项与DcmDspRoutineInfoRef的关联性，确保正确的例程信号被引用。|
|说明|The ordering defined via the index attribute of the subcontainers in this list represents the order of the dataOutN elements in the XXX_Stop function call.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalEndianness|
|描述|Defines the endianness of the data belonging to a Routine Out Signal for Stop subfunction.|
|描述|概述：DcmDspRoutineSignalEndianness配置项用于定义诊断例程信号的字节序，确保数据在不同系统间正确交换，可以是大端（Big Endian）或小端（Little Endian）。|
|描述|注意：在配置时需确保与ECU硬件架构的字节序一致；若ECU支持多字节序，则还需确保与诊断客户端的字节序匹配；在跨平台通信时特别注意字节序的一致性以避免数据解释错误。|
|多实例个数|0 - 1|
|默认值|OPAQUE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalType|
|描述|Provide the type of the signal in the RoutineControl request/response.|
|描述|概述：DcmDspRoutineSignalType配置项用于定义诊断例程中信号的类型，这些信号可以是输入信号、输出信号或者输入/输出信号，用于支持诊断服务中的例程控制。|
|描述|注意：在配置DcmDspRoutineSignalType时，需要确保信号类型与实际的例程参数匹配；此外，对于每个信号，还需要定义相应的数据长度和格式；在AUTOSAR CP 4.4标准中，应当遵循诊断服务的规范来配置这些信号类型。|
|多实例个数|1 - 1|
|默认值|UINT8|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineParameterSize|
|描述|Provide the size of a RoutineControl parameter in bytes|
|描述|概述：DcmDspRoutineParameterSize配置项用于定义诊断例程中参数的大小，这个参数可以是输入参数、输出参数或者输入/输出参数。|
|描述|注意：在配置参数大小时，需要确保与实际诊断例程中使用的参数大小一致；超出定义大小的参数值可能会导致数据截断或者缓冲区溢出；在AUTOSAR CP 4.4标准中，应当遵循诊断服务的规范来定义参数大小。|
|多实例个数|0 - 1|
|取值范围|0 - 65535|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspRoutineSignalPos|
|描述|Provide the position of the signal in the RoutineControl request/response.|
|描述|概述：DcmDspRoutineSignalPos配置项用于定义诊断例程中信号的位置，确保在诊断通信过程中正确解析和处理信号数据。|
|描述|注意：该配置项需要与DcmDspRoutine信号定义一致，确保信号位置的正确性；在配置时需注意信号的顺序和偏移，避免数据解析错误；AUTOSAR CP 4.4标准中对于诊断信号的处理和位置有明确规范，需要遵守相关规定以保证兼容性。|
|说明|The position is defined in bits.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

######## 1.3.20.3.2.1.1. DcmDspArgumentScaling

|容器属性|值（容器）|
|---|---|
|名称|DcmDspArgumentScaling|
|描述|This container contains the configuration (arguments) of an alternative Diagnosis Representation. Out if this the scaling between Diagnosis and ECU internal representation and vice versa can be calculated.|
|描述|概述：DcmDspArgumentScaling配置项用于定义诊断服务参数的缩放信息，包括缩放比例、偏移量等，以支持不同的参数表示方法和单位转换。|
|描述|注意：在定义参数缩放时，需确保缩放比例和偏移量与实际物理量和ECU内部处理逻辑相匹配；缩放配置应遵循ECU支持的精度和范围限制；AUTOSAR CP 4.4标准中，此配置项的使用应结合具体的诊断服务需求和ECU能力进行详细规划。|
|多实例个数|0 - 1|

######### 1.3.20.3.2.1.1.1. DcmDspAlternativeArgumentData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeArgumentData|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of a ArgumentDataPrototype.|
|描述|概述：DcmDspAlternativeArgumentData配置项用于定义诊断服务中备选参数数据的属性，这些备选参数数据可以在诊断请求消息中替代标准定义的参数数据。|
|描述|注意：在配置备选参数数据时，需要确保它们与诊断服务请求的数据格式和长度兼容；备选参数数据应当仅在必要时使用，以避免诊断通信中的混淆；AUTOSAR CP 4.4标准中对备选参数数据的使用可能有特定的限制或要求，需要仔细参考相关文档以确保合规。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDataElement|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ArgumentDataPrototype.|
|描述|概述：DcmDataElement配置项用于定义诊断服务中的数据元素，它指定了数据元素的类型、大小以及如何从车辆中读取或写入这些数据。|
|描述|注意：在配置DcmDataElement时，必须确保数据元素的类型和大小与实际应用中的数据类型相匹配；对于读取或写入操作的实现，需要遵循ECU软件架构中的数据访问机制；此外，应注意数据元素的安全性和访问权限设置，以防止未授权访问。|
|说明|The CompuMethod of the data type of the referenced ArgumentDataPrototype will be applied to the data type of the ArgumentDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|ARGUMENT-DATA-PROTOTYPE|

######### 1.3.20.3.2.1.1.2. DcmDspAlternativeDataType

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDataType|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of an ApplicationDataType.|
|描述|概述：DcmDspAlternativeDataType配置项用于定义诊断服务中使用的替代数据类型，允许在不同上下文中使用不同的数据表示形式，以适应特定的数据处理需求。|
|描述|注意：在定义替代数据类型时，需要确保它与原始数据类型兼容；此配置项的使用应遵循AUTOSAR标准中对数据类型替换的规定；在实际应用中，应仔细考虑替代数据类型的转换逻辑，以防止数据精度损失或解释错误。|
|说明|Additionally the definition of a text table mapping can be a defined for ApplicationDataTypes with a CompuMethod of category TEXTTABLE and SCALE_LINEAR_AND_TEXTTABLE.|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmApplicationDataType|
|描述|Alternative Diagnosis Representation for the data defined by the means of a ApplicationDataType of category VALUE, BOOLEAN or ARRAY.|
|描述|概述：DcmApplicationDataType配置项用于定义诊断服务中使用的应用数据类型，这些数据类型是诊断通信中所需的参数或数据结构的类型。|
|描述|注意：在定义DcmApplicationDataType时，需要确保数据类型与实际应用程序中使用的数据类型相匹配；此外，数据类型的定义应遵循AUTOSAR标准中规定的数据类型约束和格式；在配置过程中，还应注意数据类型的内存对齐和大小，以确保数据的正确传输和处理。|
|说明|The CompuMethod that applies to the referenced ApplicationDataType in case of category VALUE or BOOLEAN will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm.|
|多实例个数|1 - 1|
|目标类型|APPLICATION-DATA-TYPE|

########## 1.3.20.3.2.1.1.2.1. DcmDspTextTableMapping

|容器属性|值（容器）|
|---|---|
|名称|DcmDspTextTableMapping|
|描述|The purpose of the DcmDspTextTableMapping is to associate a texttable value defined in the context of the Dcm to a texttable value defined in the context of a CompuMethod referenced by a DataType that shall be taken to create a dataElement in a SenderReceiverInterface. By this means it is possible to create a primitive version of a TexttableMapping (which can only be applied if a dataElement already exists).|
|描述|概述：DcmDspTextTableMapping配置项用于定义诊断服务组件（Diagnostic Communication Manager）中，文本表的映射关系，它将特定的文本代码映射到相应的文本字符串上，以便在诊断通信中使用。|
|描述|注意：在配置DcmDspTextTableMapping时，需要确保文本代码与文本字符串的映射是唯一的，避免同一代码映射到多个字符串；此外，应当注意文本字符串的长度不应超过诊断协议允许的最大长度限制；在国际化设计中，还需考虑不同语言环境下的文本映射问题。|
|说明|In other words, the DcmDspTextTableMapping provides a similar mechanism to the TexttableMapping in a situation where the TexttableMapping cannot be applied since the SenderReceiverInterface for the PortPrototype on the Dcm ServiceComponent does not yet exist.|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspDiagnosisRepresentationDataValue|
|描述|The data value in the diagnosis representation.|
|描述|概述：DcmDspDiagnosisRepresentationDataValue 用于定义诊断服务中数据的表示方式，确保数据按照预定格式正确显示或传输。|
|描述|注意：该配置项需要与诊断请求和响应格式严格匹配；在配置时需考虑数据的大小和类型，以确保数据的准确性和完整性；在AUTOSAR CP 4.4标准中，确保遵循相关的数据表示规范。|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspInternalDataValue|
|描述|The ECU internal data value.|
|描述|概述：DcmDspInternalDataValue配置项用于定义诊断服务处理过程中，需要访问的内部数据的值，这些数据值可能用于控制策略决定或状态监测。|
|描述|注意：在配置DcmDspInternalDataValue时，需要确保引用的内部数据与实际应用程序中的数据保持一致；对于敏感或安全相关的数据，应考虑访问权限和保护机制；AUTOSAR CP 4.4标准中对于诊断数据的访问和管理有详细规定，需要遵守相关规范以确保兼容性和安全性。|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

######### 1.3.20.3.2.1.1.3. DcmDspAlternativeDiagnosticDataElement

|容器属性|值（容器）|
|---|---|
|名称|DcmDspAlternativeDiagnosticDataElement|
|描述|This container contains the configuration (parameters) of an alternative Diagnosis Representation by the means of Diagnostic Extract.|
|描述|概述：DcmDspAlternativeDiagnosticDataElement配置项用于定义诊断服务中备选的数据元素，这些备选元素可以在原始数据元素不可用时被使用，以支持诊断服务的灵活性和可靠性。|
|描述|注意：在配置备选数据元素时，必须确保它们与原始数据元素兼容，并且满足相同的诊断需求；备选数据元素的使用可能需要根据车辆的配置或状态条件来决定；在实施时应注意备选数据元素的访问权限和安全策略，以防止未授权的访问。|
|多实例个数|0 - 1|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|DcmDspDiagnosticDataElementRef|
|描述|Alternative Diagnosis Representation for the data defined by the means of a DiagnosticDataElement in the Diagnostic Extract.|
|描述|概述：DcmDspDiagnosticDataElementRef 用于引用诊断数据元素，这些元素用于存储和传输诊断信息，如故障码或车辆状态信息。|
|描述|注意：确保引用的数据元素与诊断服务的需求相匹配；引用的数据元素需要在Dcm配置中正确定义；在多服务或多客户端环境中，注意数据元素的访问冲突和同步问题。|
|说明|This EcucForeignReference enables the access to all SwDataDefProps, in particular BaseType, CompuMethod and DataConstr The CompuMethod and DataConstr that applies to the referenced DiagnosticDataElement will be applied to the data type of the VariableDataPrototype in the interface used by the Dcm. The mapped ImplementationDataType needs to match the given BaseType.|
|多实例个数|1 - 1|
|目标类型|DIAGNOSTIC-DATA-ELEMENT|

#### 1.3.21. DcmDspSecurity

|容器属性|值（容器）|
|---|---|
|名称|DcmDspSecurity|
|描述|This container contains the configuration ( DSP parameter) for security level configuration (per security level)|
|描述|概述：DcmDspSecurity配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中安全访问的参数，包括安全访问级别、种子/密钥算法、延时时间等，以控制对敏感操作或数据的访问权限。|
|描述|注意：在配置DcmDspSecurity时，需要确保安全级别与项目需求相匹配，避免设置过低的安全级别导致潜在的安全风险；种子/密钥算法应确保足够的复杂度，以防止未授权访问；AUTOSAR CP 4.4标准中对于安全延时的处理可能与早期版本有所不同，需要特别注意版本间的兼容性。|
|说明|Description This container contains Rows of DcmDspSecurityRow|
|多实例个数|1 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspSecurityMaxAttemptCounterReadoutTime|
|描述|Delay, in seconds, from startup (measured from the first call of the Dcm_MainFunction()), allowed for all AttemptCounter values to be obtained from the Application.|
|描述|概述：DcmDspSecurityMaxAttemptCounterReadoutTime配置项用于定义在诊断会话中，读取安全访问尝试计数器的最大时间。|
|描述|注意：该时间值应足够允许系统处理安全相关的数据，但也不应过长以避免延迟；确保设置的时间符合具体应用的安全要求；在AUTOSAR CP 4.4标准中，该配置项的具体数值应根据实际安全策略来设定，无默认值。|
|说明|Must be a multiple of the DcmTaskTime. min: A value equal to the DcmTaskTime|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

##### 1.3.21.1. DcmDspSecurityRow

|容器属性|值（容器）|
|---|---|
|名称|DcmDspSecurityRow|
|描述|Definition of a single Row of configuration for security level configuration (per security level)|
|描述|概述：DcmDspSecurityRow配置项定义了诊断安全访问的安全级别和相关属性，用于控制对车辆敏感数据和功能的访问。|
|描述|注意：确保每个安全级别的设置符合车辆制造商的安全要求；配置时需注意与DcmDspSecurityTable的一致性；在AUTOSAR CP 4.4标准中，安全级别的配置和管理应严格遵守标准规定，以防止未授权的访问。|
|说明|The name of this container is used to define the name of the R-Port through which the DCM accesses the interface SecurityAccess_{SecurityLevel}. The R-Port is named SecurityAccess_{SecurityLevel} where {SecurityLevel} is the name of the container DcmDspSecurityRow. If there is no reference, no check of security level shall be done.|
|多实例个数|0 - 31|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspSecurityAttemptCounterEnabled|
|描述|This configuration parameter controls the existence of the APIs to set / get the attempt counter values towards application (Xxx_SetSecurityAttemptCounter() / Xxx_GetSecurityAttemptCounter()).|
|描述|概述：DcmDspSecurityAttemptCounterEnabled配置项用于启用或禁用诊断通信管理器（Diagnostic Communication Manager）中安全访问服务的尝试次数计数器，该计数器用于跟踪安全访问尝试的次数。|
|描述|注意：在配置此项时，需要确保它与系统的安全策略一致；如果启用了尝试次数计数器，还需要配置相应的最大尝试次数和延时策略；在不同的安全级别可能需要不同的尝试次数限制。|
|说明|In case of enabled, the security attempt counter values are passed to application, whenever there is a change in the value. This allows storing the values in nonvolatile RAM and restoring them at ECU startup.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspSecurityUsePort|
|描述|Defines which kind of interface shall be used for security access.|
|描述|概述：DcmDspSecurityUsePort配置项用于定义诊断组件（Dcm）中安全服务（Security）的端口使用情况，指定安全算法和密钥管理机制如何通过端口与其他软件组件交互。|
|描述|注意：在AUTOSAR CP 4.4中，确保安全服务的端口配置与实际的安全需求和实现机制相匹配；端口配置应支持所需的安全算法和密钥管理策略；不正确的端口配置可能导致安全功能不符合预期，影响系统的安全性。|
|多实例个数|1 - 1|
|默认值|USE_ASYNCH_CLIENT_SERVER|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspSecurityDelayTime|
|描述|Delay time after failed security access in seconds.|
|描述|概述：DcmDspSecurityDelayTime配置项用于定义诊断安全访问时，客户端在发送错误的安全访问请求后，需要等待的延迟时间才能再次尝试。|
|描述|注意：该延迟时间用于防止恶意攻击，确保系统安全性；应根据项目的安全需求合理设置延迟时间；在AUTOSAR CP 4.4标准中，需确保该配置与安全策略和法规要求相符。|
|说明|This is started after DcmDspSecurityNumAttDelay number of failed security accesses. min: A negative value is not allowed.|
|多实例个数|1 - 1|
|默认值|10|
|取值范围|0 - 65535|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspSecurityDelayTimeOnBoot|
|描述|Value of the delay timer in case of 'power on' in seconds.|
|描述|概述：DcmDspSecurityDelayTimeOnBoot配置项用于定义车辆启动后，诊断安全访问服务（Security Access Service）在允许再次尝试之前必须等待的延迟时间。|
|描述|注意：该值应根据系统安全需求设定，以防止恶意攻击；在AUTOSAR CP 4.4标准中，该配置项的时间单位和最大值可能有具体要求，需要遵守这些规定；如果设置的延迟时间太长，可能会影响用户体验，因此需要在安全性和便利性之间做出平衡。|
|说明|This delay indicates the time at ECU boot power-on time during which the Dcm does not accept a security access. min: A negative value is not allowed.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 65535|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspSecurityCompareKeyFnc|
|描述|Function name to request the result of a key comparison.|
|描述|概述：DcmDspSecurityCompareKeyFnc是一个配置项，用于定义诊断安全访问时，用于比较密钥是否正确的函数。|
|描述|注意：该函数需要用户实现，确保其能够正确比较从客户端接收的密钥与系统存储的密钥；在实现时需考虑安全性，避免潜在的安全漏洞；该配置项在AUTOSAR CP 4.4中应确保与安全策略和需求相一致。|
|说明|Parameter is only relevant if DcmDspSecurityUsePort=="USE_ ASYNCH_FNC". This parameter is related to the interface Xxx_CompareKey.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspSecurityGetAttemptCounterFnc|
|描述|Function name to request the value of an attempt counter.|
|描述|概述：DcmDspSecurityGetAttemptCounterFnc配置项用于指定一个函数，该函数负责获取当前安全访问尝试次数的计数器值，通常用于防止未授权访问。|
|描述|注意：该函数需要能够可靠地返回剩余的尝试次数，并且应当在多次调用间保持一致性；在实现时应确保对尝试次数的存储是安全的，以防止潜在的篡改；根据AUTOSAR CP 4.4标准，该函数的实现应遵循模块的定义和安全要求。|
|说明|This parameter is related to the interface Xxx_ GetSecurityAttemptCounter.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspSecurityGetSeedFnc|
|描述|Callout function name used to request a seed.|
|描述|概述：DcmDspSecurityGetSeedFnc是一个配置项，用于定义在诊断通信管理（Diagnostic Communication Manager）中，当请求安全访问时，用于生成安全种子（Seed）的函数。|
|描述|注意：该函数的实现必须确保生成的种子具有足够的随机性，以防止未授权访问；在AUTOSAR CP 4.4中，确保该函数与安全算法的兼容性和性能要求相匹配；考虑到响应时间和系统资源，该函数的执行效率也需优化。|
|说明|This parameter is related to the interface Xxx_GetSeed.|
|多实例个数|0 - 1|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspSecuritySetAttemptCounterFnc|
|描述|Function name to set the value of an attempt counter.|
|描述|概述：DcmDspSecuritySetAttemptCounterFnc配置项用于指定一个函数，该函数负责设置诊断安全访问（Security Access）服务中的尝试计数器，用于跟踪安全访问尝试的次数。|
|描述|注意：在配置该函数时，需要确保它能够正确地管理尝试计数器的值，包括增加尝试次数和在成功访问后重置计数器；此外，该函数应当能够处理非易失性存储，以防止断电后尝试次数丢失；最后，确保该函数与ECU的安全策略一致，遵循AUTOSAR的安全访问规范。|
|说明|This parameter is related to the interface Xxx_ SetSecurityAttemptCounter.|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSecurityADRSize|
|描述|Size in bytes of the AccessDataRecord used in GetSeed|
|描述|概述：DcmDspSecurityADRSize配置项用于定义诊断安全访问请求消息中的ADR（AccessDataRecord）字段的大小，即客户端发送给服务器的安全密钥的长度。|
|描述|注意：在AUTOSAR CP 4.4标准中，安全访问的密钥长度应该与ECU支持的安全算法和密钥长度相匹配；配置的ADR大小必须能够容纳足够的数据以满足安全算法的要求；不正确的ADR大小配置可能导致安全访问功能不正常或安全漏洞。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSecurityKeySize|
|描述|size of the security key (in Bytes).|
|描述|概述：DcmDspSecurityKeySize配置项用于定义诊断安全访问（Security Access）服务中使用的密钥的大小，通常以字节为单位，这个参数决定了安全算法处理的密钥长度。|
|描述|注意：在AUTOSAR CP 4.4标准中，密钥大小应该与实际使用的安全算法和车辆制造商的安全要求相匹配；密钥长度的选择会影响到安全性和性能，因此需要仔细考虑；如果配置的密钥大小不支持所选的安全算法，可能会导致诊断安全访问服务无法正常工作。|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|1 - 4294967295|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSecurityLevel|
|描述|Value of Security level.|
|描述|概述：DcmDspSecurityLevel配置项定义了诊断服务中的安全访问级别，用于控制对敏感操作或数据的访问权限，确保只有经过授权的用户才能执行特定的诊断服务。|
|描述|注意：在配置DcmDspSecurityLevel时，必须确保安全级别的唯一性和递增性，避免安全级别之间的冲突；应根据实际应用需求合理设置安全级别，以满足系统的安全要求；AUTOSAR CP 4.4标准中对安全级别的具体数值和含义有明确规定，配置时需遵循这些规定以保证兼容性。|
|说明|The locked state cannot be configured explicitly. 1,2,3...63: configuration dependent - Conversion formula to calculate SecurityLevel out of tester requested SecurityAccessType parameter: SecurityLevel = (SecurityAccessType (requestSeed) + 1) / 2 Type: Dcm_SecLevelType|
|多实例个数|1 - 1|
|取值范围|0 - 63|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSecurityNumAttDelay|
|描述|Number of failed security accesses after which the delay time is activated|
|描述|概述：DcmDspSecurityNumAttDelay配置项用于定义在Diagnostics Communication Manager (DCM) 模块中，当安全访问请求失败达到一定次数后，需要等待的延迟时间才能再次尝试安全访问。|
|描述|注意：该延迟时间用于防止恶意攻击，确保车辆的诊断安全；配置的延迟时间应符合具体应用场景的安全要求；AUTOSAR CP 4.4标准中，该配置项的使用应确保与安全策略和法规要求相一致。|
|多实例个数|0 - 1|
|默认值|3|
|取值范围|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSecuritySeedSize|
|描述|size of the security seed (in Bytes).|
|描述|概述：DcmDspSecuritySeedSize配置项定义了诊断安全服务中种子（Seed）的大小，这是用于车辆诊断安全认证过程中的关键参数。|
|描述|注意：种子大小应符合车辆制造商的安全要求和标准；不正确的种子大小可能导致安全认证失败；在AUTOSAR CP 4.4中，种子大小应确保与安全算法兼容。|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|1 - 4294967295|

#### 1.3.22. DcmDspSession

|容器属性|值（容器）|
|---|---|
|名称|DcmDspSession|
|描述|Parent container holding single rows to configure particular sessions|
|描述|概述：DcmDspSession配置项用于定义诊断会话控制服务（Diagnostic Session Control, Service ID 0x10）中的会话类型，包括会话的名称、时间参数以及与会话相关的安全访问级别。|
|描述|注意：在配置DcmDspSession时，需要确保会话类型符合ISO 14229标准中定义的会话层次结构；每个会话类型应有唯一的会话控制类型标识符；还需注意会话之间的切换条件和对应的安全访问级别，以确保诊断功能的正确性和安全性。|
|多实例个数|1 - 1|

##### 1.3.22.1. DcmDspSessionRow

|容器属性|值（容器）|
|---|---|
|名称|DcmDspSessionRow|
|描述|This container holds all parameters needed to configure a single session|
|描述|概述：DcmDspSessionRow配置项定义了诊断会话控制服务（Diagnostic Session Control service）中的会话类型及其属性，用于控制诊断会话的行为和访问权限。|
|描述|注意：确保每个会话类型的配置与实际应用需求相匹配，避免配置不当导致诊断功能异常；会话类型的切换应考虑到安全性和权限管理，防止未授权访问；AUTOSAR CP 4.4中对会话的管理和配置有详细规定，需要遵守相关规范以确保兼容性。|
|多实例个数|0 - 31|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmDspSessionForBoot|
|描述|This parameter defines whether this diagnostic session allows to jump to Bootloader (OEM Bootloader or System Supplier Bootloader) and determines, from which unit the final response will be sent.|
|描述|概述：DcmDspSessionForBoot配置项用于定义诊断会话控制服务（Diagnostic Session Control service）中，用于启动引导会话的会话级别。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保配置的会话级别与系统支持的引导加载器会话一致；引导会话通常用于ECU编程，因此需要特别注意安全和授权机制；此配置项的使用应符合ECU的引导和编程策略。|
|说明|If this diagnostic session doesn't allow to jump to Bootloader the value DCM_NO_BOOT shall be chosen.|
|多实例个数|1 - 1|
|默认值|DCM_NO_BOOT|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspSessionP2ServerMax|
|描述|This is the session value for P2ServerMax in seconds (per Session).|
|描述|概述：DcmDspSessionP2ServerMax配置项定义了诊断通信控制器（Diagnostic Communication Manager）在非默认会话中等待客户端（tester）请求的最大时间（P2ServerMax时间），超过这个时间没有收到请求则会认为通信超时。|
|描述|注意：该时间值应根据具体的车辆网络环境和诊断需求进行配置；超时时间设置过短可能导致正常请求被错误地判定为超时，设置过长可能影响系统的响应性能；在AUTOSAR CP 4.4标准中，该配置项的单位通常是毫秒，确保与标准一致。|
|说明|The AUTOSAR configuration standard is to use SI units, so this parameter is defined as a float value in seconds. DCM configuration tools must convert this float value to the appropriate value format for the use in the software implementation of DCM. This value is reported to the tester within the response to the 'Session Control' service.|
|多实例个数|1 - 1|
|取值范围|0 - 1|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmDspSessionP2StarServerMax|
|描述|This is the session value for P2\*ServerMax in seconds (per Session).|
|描述|概述：DcmDspSessionP2StarServerMax配置项定义了在非默认会话中，服务器最大的P2\*定时器时间，即服务器在接收到请求后，最长可以等待多久来发送响应。|
|描述|注意：该时间必须大于或等于DcmDspSessionP2ServerMax的值；配置值应考虑网络延迟和处理时间，以避免通信超时；在配置时需确保符合具体项目或标准的要求，避免设置过短导致通信失败。|
|说明|The AUTOSAR configuration standard is to use SI units, so this parameter is defined as a float value in seconds. DCM configuration tools must convert this float value to the appropriate value format for the use in the software implementation of DCM. This value is reported to the tester within the response to the 'Session Control' service.|
|多实例个数|1 - 1|
|取值范围|0 - 100|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspSessionLevel|
|描述|subFunction value of the DiagnosticSession.|
|描述|概述：DcmDspSessionLevel配置项用于定义诊断会话控制服务（Diagnostic Session Control service）中支持的会话级别，这些级别决定了在特定会话中可以执行的诊断服务集合。|
|描述|注意：在配置DcmDspSessionLevel时，需要确保定义的会话级别与ISO 14229标准中定义的会话级别相匹配；每个会话级别应该有唯一的标识符，以避免在诊断通信中的混淆；还需要注意会话级别之间的切换条件和权限，确保诊断安全性。|
|说明|0, 127 and all values above 127 are reserved by ISO|
|多实例个数|1 - 1|
|取值范围|1 - 126|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspSessionResponseMultiplePendingFnc|
|描述|Function name to support responsing multiple pendings of service 0x10 02.|
|描述|概述：DcmDspSessionResponseMultiplePendingFnc配置项用于指定一个函数，该函数负责0x10 02服务支持多个0x78响应的回调函数。|
|描述|注意：该函数需要支持对应的协议号，在实现时应确保对协议号的使用是合法的，以防止异常的发生；根据AUTOSAR CP 4.4标准，该函数的实现应遵循模块的定义和安全要求。|
|说明|This parameter is related to the interface DspUdsDiagnosticSessionControl.|
|多实例个数|0 - 1|

#### 1.3.23. DcmDspVehInfo

|容器属性|值（容器）|
|---|---|
|名称|DcmDspVehInfo|
|描述|This container contains the configuration (parameters) for one single VehicleInfoType of service $09|
|描述|概述：DcmDspVehInfo配置项用于定义车辆信息服务（Vehicle Information Service）的参数，这些参数包括车辆制造商的信息、车辆型号、VIN码等，它们通常在诊断通信管理器（Diagnostic Communication Manager）模块中使用。|
|描述|注意：在配置DcmDspVehInfo时，需要确保所提供的车辆信息符合相关法规和标准要求；配置的信息应当与车辆实际参数一致，以避免诊断通信中的错误；此外，应注意保护车辆信息的安全性，防止通过诊断接口泄露敏感信息。|
|多实例个数|0 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspVehInfoNODIProvResp|
|描述|Indicate the Dcm, which side is responsible to fill the number of data items (NODI), Dcm or the provider of the InfoType data. In case the responsibility is on provider side, only one DcmDspVehInfoData container is allowed.|
|描述|概述：DcmDspVehInfoNODIProvResp配置项用于定义诊断通信管理器（Diagnostic Communication Manager）在处理车辆信息请求时，如果没有可提供的数据项（NODI），应如何响应。|
|描述|注意：根据AUTOSAR CP 4.4标准，必须确保在配置此项时考虑到系统的安全性和隐私要求；配置应遵循OEM的具体策略和法规要求；在设计响应策略时，应考虑到可能的网络带宽和性能影响。|
|说明|\* true: Provider is responsible for providing the number of data items parameter \* false or not existing: Dcm is responsible for providing the number of data items parameter|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspVehInfoInfoType|
|描述|value of InfoType.|
|描述|概述：DcmDspVehInfoInfoType 用于定义车辆信息服务中的信息类型，这些信息类型用于诊断通信中的车辆信息请求。|
|描述|注意：在配置DcmDspVehInfoInfoType时，确保信息类型符合ISO 14229标准中定义的车辆信息服务要求；此配置项应与车辆制造商的诊断需求一致；在AUTOSAR CP 4.4中，应注意其与DcmDspVehInfo服务的兼容性和正确实现。|
|说明|Within each DcmConfigSet all DcmDspVehInfoInfoType values shall be unique.|
|多实例个数|1 - 1|
|取值范围|0 - 255|

##### 1.3.23.1. DcmDspVehInfoData

|容器属性|值（容器）|
|---|---|
|名称|DcmDspVehInfoData|
|描述|Data Item of an InfoType; ShortName is post-fix of the port interface name.|
|描述|概述：DcmDspVehInfoData配置项用于定义车辆信息服务（Vehicle Information Service）中，特定信息类型的数据属性，如数据长度和格式，它指定了诊断服务如何读取和报告车辆的特定信息。|
|描述|注意：在配置DcmDspVehInfoData时，必须确保数据长度和格式与车辆实际可提供的信息相匹配；此配置项对于实现诊断通信中的车辆信息服务至关重要，错误的配置可能导致诊断通信失败；AUTOSAR CP 4.4标准中对于诊断数据的处理和传输有严格规定，需要仔细遵守。|
|多实例个数|1 - inf|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDspVehInfoDataUsePort|
|描述|When this parameter is set to true the DCM will access the Data using an R-Port requiring a PortInterface IInfotypeServices_{VehInfoData}.|
|描述|概述：DcmDspVehInfoDataUsePort配置项用于定义诊断服务组件（Dcm）中，车辆信息服务（Vehicle Information Service）获取数据的接口方式，指定是通过端口（Port）还是直接从内部或外部数据源读取。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保选择的数据接口方式与系统架构和数据源兼容；配置时需考虑数据实时性和安全性要求；若使用端口方式，需确保端口配置正确且与数据源接口匹配。|
|说明|The R-Port is named InfotypeServices_{VehInfoData} where {VEHINFODATA} is the name of the container DcmDspVehInfoData. In that case, the DcmDspVehInfoDataReadFnc is ignored and the RTE APIs are used. When this parameter is set to false, the DCM calls the function defined in DcmDspVehInfoDataReadFnc.|
|多实例个数|1 - 1|
|默认值|true|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmDspVehInfoDataReadFnc|
|描述|Callout function name for reading InfoType data item. Only required in case parameter 'DcmDspVehInfoDataUsePort' is set to 'false'|
|描述|概述：DcmDspVehInfoDataReadFnc配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，读取车辆信息数据的函数。|
|描述|注意：确保实现的函数符合OEM的车辆信息数据要求；函数应处理可能的错误和异常情况；在AUTOSAR CP 4.4中，该函数的接口和行为应严格遵循标准规范。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspVehInfoDataOrder|
|描述|Defines the order of the data item in the InfoType; values: 0..255; first data item having the order number 0; the next 1 and so on.|
|描述|概述：DcmDspVehInfoDataOrder配置项用于定义车辆信息服务（Vehicle Information Service）中，请求的数据元素的返回顺序。|
|描述|注意：在配置DcmDspVehInfoDataOrder时，必须确保数据元素的顺序与客户端的期望和标准文档中定义的顺序一致；如果顺序配置错误，可能会导致客户端解析数据时出现问题；AUTOSAR CP 4.4标准中对于车辆信息服务的数据顺序有明确的规定，需要遵守这些规定以保证兼容性。|
|说明|The configuration of order needs to be unique per InfoType.|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspVehInfoDataSize|
|描述|Size in bytes of the InfoType data item.|
|描述|概述：DcmDspVehInfoDataSize配置项用于定义车辆信息服务（Vehicle Information Service）中，每个车辆信息类型（Vehicle Information Type）的数据大小。|
|描述|注意：在配置DcmDspVehInfoDataSize时，需要确保数据大小与实际车辆信息类型的数据长度一致；超出或低于实际数据长度的配置可能导致数据读取错误或内存溢出；此配置项应与车辆制造商的规范和诊断需求文档保持一致。|
|多实例个数|1 - 1|
|取值范围|0 - 255|

#### 1.3.24. DcmDspVehicleSystemGroup

|容器属性|值（容器）|
|---|---|
|名称|DcmDspVehicleSystemGroup|
|描述|This container includes all Dcm related Vehicle System Groups (VSGs)|
|描述|概述：DcmDspVehicleSystemGroup配置项用于定义诊断服务组件中，与车辆系统相关的组配置信息，它允许对不同的车辆系统进行分组管理，以便在执行诊断服务时能够针对特定的系统组进行操作。|
|描述|注意：在配置DcmDspVehicleSystemGroup时，需要确保每个系统组的标识符（ID）是唯一的，以避免在诊断会话中的冲突；此配置项在AUTOSAR CP 4.4标准中可能对系统组的属性有特定要求，需仔细参考标准文档以确保兼容性；在实际应用中，应根据具体的诊断需求合理划分系统组，以优化诊断效率和准确性。|
|多实例个数|0 - 1|

##### 1.3.24.1. DcmDspVehicleSystemGroupRow

|容器属性|值（容器）|
|---|---|
|名称|DcmDspVehicleSystemGroupRow|
|描述|Represents a single Vehicle System Group (VSG) related to Dcm|
|描述|概述：DcmDspVehicleSystemGroupRow配置项用于定义诊断服务组件中，车辆系统组的属性，包括系统组的标识符和对应的服务处理函数。|
|描述|注意：确保每个DcmDspVehicleSystemGroupRow配置项中的系统组标识符唯一，以避免在诊断会话中的冲突；该配置项应与车辆的实际系统架构相匹配，确保诊断功能的正确实现；在配置时需考虑系统的安全性要求，避免未授权访问敏感系统组。|
|多实例个数|1 - 255|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmDspVehicleSystemGroupId|
|描述|Specifies an abstract ID of the corresponding Vehicle System Group.|
|描述|概述：DcmDspVehicleSystemGroupId配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，车辆系统组的唯一标识符，这有助于在执行诊断服务时区分不同的车辆系统组。|
|描述|注意：在配置DcmDspVehicleSystemGroupId时，必须确保每个系统组的标识符是唯一的，以避免在诊断过程中出现标识符冲突；此外，标识符应与车辆制造商的诊断规范保持一致，以确保诊断工具能够正确识别和访问相应的系统组；在AUTOSAR CP 4.4标准中，应当遵循相关的模块配置规则和数据约束，以保证系统的兼容性和互操作性。|
|多实例个数|1 - 1|
|取值范围|1 - 255|

### 1.4. DcmPageBufferCfg

|容器属性|值（容器）|
|---|---|
|名称|DcmPageBufferCfg|
|描述|This container contains the configuration (parameters) for Page Buffer handling|
|描述|概述：DcmPageBufferCfg是用于配置诊断通信管理器（Diagnostic Communication Manager）中分页缓冲区的属性，这些属性包括缓冲区的大小和地址，用于存储和管理诊断服务的响应数据，特别是在需要分页发送大量数据时。|
|描述|注意：在配置DcmPageBufferCfg时，必须确保缓冲区大小足够存储预期的最大响应数据量；同时，缓冲区的地址应当避免与其他系统模块的内存区域冲突；根据AUTOSAR CP 4.4标准，还需要确保配置的属性与ECU的内存管理策略和硬件能力相匹配。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmPagedBufferEnabled|
|描述|Allow to enable or disable the Paged buffer mechanism.|
|描述|概述：DcmPagedBufferEnabled 是一个配置项，用于启用或禁用诊断通信管理器（Diagnostic Communication Manager）中的分页缓冲区功能，该功能允许在发送大量诊断响应数据时进行分页处理。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在需要传输大数据量的诊断服务中启用此功能；如果ECU的资源有限，需要评估开启分页缓冲区对内存和处理能力的影响；在配置时应考虑与Dcm的其他配置参数的兼容性和依赖性。|
|说明|true = Paged buffer handling enabled false = Paged Buffer handling disabled|
|多实例个数|1 - 1|

### 1.5. DcmProcessingConditions

|容器属性|值（容器）|
|---|---|
|名称|DcmProcessingConditions|
|描述|This container contains the configuration for mode arbitration functionality of the Dcm|
|描述|概述：DcmProcessingConditions配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中处理不同诊断请求的条件，包括但不限于车辆速度、引擎状态等条件，以确保在适当的车辆状态下执行诊断服务。|
|描述|注意：在配置DcmProcessingConditions时，必须确保所有条件与实际车辆状态检测机制相匹配，避免因条件设置不当导致诊断服务无法执行；此外，AUTOSAR CP 4.4标准中对于处理条件的具体实现和支持程度可能有所不同，需要参考具体的AUTOSAR实现文档；在多条件组合时，应注意条件之间的逻辑关系，确保逻辑判断的准确性。|
|多实例个数|0 - 1|

#### 1.5.1. DcmModeCondition

|容器属性|值（容器）|
|---|---|
|名称|DcmModeCondition|
|描述|This container contains the configuration of a mode condition or an environmental conditions which can be used as argument in DcmModeRules.|
|描述|概述：DcmModeCondition配置项用于定义诊断通信管理（Diagnostic Communication Manager）中的模式条件，这些条件决定了诊断会话是否可以被激活或维持。|
|描述|注意：确保DcmModeCondition与车辆的操作模式和状态兼容；在设计时需考虑所有可能的车辆状态和模式转换，以避免诊断会话在不适当的时间被激活；AUTOSAR CP 4.4标准中对于模式条件的定义和使用应严格遵守，以保证系统的安全性和可靠性。|
|说明|One DcmModeCondition shall contain either one DcmSwcModeRef or one DcmBswModeRef or one DcmSwcSRDataElementRef. Please note that the Dcm acts as well as mode manager. Therefore the references DcmSwcModeRef or one DcmBswModeRef. might point to provided ModeDeclarationGroupPrototypes of the Dcm itself as well as to provided ModeDeclarationGroupPrototypes of other Bsw Modules or software components. In case of a configured DcmSwcModeRef or DcmBswModeRef only the DcmConditionType DCM_EQUALS or DCM_EQUALS_NOT are applicable. In case of DcmSwcSRDataElementRef all literals of DcmConditionType are possible.|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmConditionType|
|描述|This parameter specifies what kind of comparison that is made for the evaluation of the mode condition.|
|描述|概述：DcmConditionType 用于定义诊断通信管理（Diagnostic Communication Manager）中的不同条件类型，这些条件决定了诊断会话是否可以被启动或继续。|
|描述|注意：在配置DcmConditionType时，需要确保所有条件类型与系统的安全和诊断需求相匹配；此配置项应与具体的诊断需求和策略紧密相关，避免设置不恰当的条件导致诊断功能失效；AUTOSAR CP 4.4标准中对于DcmConditionType的具体实现细节有严格规定，需遵循标准指导。|
|多实例个数|1 - 1|
|默认值|DCM_EQUALS|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmProcessingConditionMode|
|描述|This parameter specifies what kind of comparison that is made for the evaluation of the mode condition.|
|描述|概述：DcmProcessingConditionMode配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中的处理条件模式，它决定了在特定条件下，诊断请求是否被接受或拒绝。|
|描述|注意：在配置DcmProcessingConditionMode时，需要确保它与系统中的安全性和诊断策略相匹配；此外，应考虑到不同诊断会话模式下的处理条件，以及与其他模块的交互可能对处理条件产生的影响；AUTOSAR CP 4.4标准中可能有具体的枚举值和参数要求，需要根据标准文档进行准确配置。|
|多实例个数|0 - 1|
|默认值|E_OK|

|配置项属性|值（函数名配置项）|
|---|---|
|名称|DcmSwcModeRef|
|描述|Specifies the function to be called on check mode condition.|
|描述|概述：DcmSwcModeRef配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中软件组件（Software Component）的模式引用，允许软件组件根据不同的诊断模式改变其行为。|
|描述|注意：在配置DcmSwcModeRef时，确保引用的模式与软件组件的实际需求相匹配；此配置项对于实现基于模式的诊断服务至关重要；在AUTOSAR CP 4.4标准中，对模式管理的支持和定义可能与早期版本有所不同，需要特别注意版本间的兼容性。|
|多实例个数|1 - 1|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|DcmSwcSRDataElementRef|
|描述|Reference to environmental conditions.|
|说明|It is possible to reference a S/R Receiver-Port to read physical values and compare (equal, greater, less,...) them with a configured value that is defined by DcmSwcDataElementValue.|
|多实例个数|0 - 1|
|目标引用|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspData/DcmDspExternalSRDataElementClass/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspPid/DcmDspPidData/DcmDspPidService01/DcmDspPidService01ExternalSRDataElementClass|

|配置项属性|值（实例引用配置项）|
|---|---|
|名称|DcmBswModeRef|
|描述|This parameter references a mode of a ModeDeclarationGroupPrototype provided by a Basic Software Module used for the condition.|
|说明|Please note that such ModeDeclarationGroupPrototype are owned by a Basic Software Module Description in the role providedModeGroup.|
|多实例个数|0 - 1|
|目标上下文|MODE-DECLARATION-GROUP-PROTOTYPE|
|目标类型|MODE-DECLARATION|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmModeConditionCertificateCompareElementRef|
|描述|Reference to a certificate data element that provides the compare value.|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/KeyM/KeyMCertificate/KeyMCertificateElement|

##### 1.5.1.1. DcmSwcDataElementValue

|容器属性|值（容器）|
|---|---|
|名称|DcmSwcDataElementValue|
|描述|This container contains the configuration of a compare value.|
|描述|概述：DcmSwcDataElementValue配置项用于定义诊断服务中软件组件（Swc）数据元素的值，这些值可以是静态的或者通过诊断会话动态改变。|
|描述|注意：在配置DcmSwcDataElementValue时，确保数据元素的类型与期望的诊断服务匹配；对于动态数据，需要实现适当的接口以在诊断会话中更新值；此配置项在AUTOSAR CP 4.4中应确保与诊断数据标识符（DID）管理和映射机制兼容。|
|多实例个数|1 - 1|

###### 1.5.1.1.1. DcmSwcDataElementArray

|容器属性|值（容器）|
|---|---|
|名称|DcmSwcDataElementArray|
|描述|This container contains the configuration of a array compare value.|
|描述|概述：DcmSwcDataElementArray配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中软件组件（Software Component, Swc）的数据元素数组，这些数据元素用于读取或更新车辆的诊断信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保数据元素的类型、大小和结构与诊断需求相匹配；数组中的数据元素应当遵循诊断服务的规范，例如UDS（统一诊断服务）；在配置数据元素数组时，应注意数据的内存映射和对齐要求，以确保诊断通信的正确性和效率。|
|多实例个数|0 - 1|

####### 1.5.1.1.1.1. DcmSwcDataElementArrayElement

|容器属性|值（容器）|
|---|---|
|名称|DcmSwcDataElementArrayElement|
|描述|This container contains the configuration of a array element compare value.|
|描述|概述：DcmSwcDataElementArrayElement配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中软件组件数据元素的数组元素属性，这些属性包括数组元素的数据类型、大小和诊断访问权限等。|
|描述|注意：在配置DcmSwcDataElementArrayElement时，需要确保数组元素的数据类型与实际软件组件中定义的类型一致；数组的大小和索引范围必须正确定义，以避免访问越界；诊断访问权限应根据安全和功能需求合理设置。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmSwcDataElementArrayElementIndex|
|描述|Index to an element of the compare value array.|
|描述|概述：DcmSwcDataElementArrayElementIndex配置项用于定义诊断服务中，软件组件数据元素数组的特定元素索引，以便于访问数组中的单个数据项。|
|描述|注意：在配置时需确保索引值在数组的有效范围内；对于非数组类型的数据元素，此配置项不应使用；在AUTOSAR CP 4.4标准中，应当遵循诊断服务的数据访问规则，确保配置的一致性和正确性。|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmSwcDataElementArrayElementValue|
|描述|Value of an array element compare value.|
|描述|概述：DcmSwcDataElementArrayElementValue配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，软件组件（Software Component）数据元素数组的具体元素值，它允许对数组中每个元素进行精确的值设定。|
|描述|注意：在配置时需确保数组索引与实际软件组件中定义的数组大小一致，避免索引越界；该配置项的使用应符合诊断数据交换的具体需求，确保数据的准确性和有效性；在AUTOSAR CP 4.4标准中，对于诊断数据的管理和配置有详细规范，需确保配置项的使用与标准一致。|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

###### 1.5.1.1.2. DcmSwcDataElementPrimitive

|容器属性|值（容器）|
|---|---|
|名称|DcmSwcDataElementPrimitive|
|描述|This container contains the configuration of a primitive compare value.|
|描述|概述：DcmSwcDataElementPrimitive配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中，软件组件（Software Component）的基本数据元素。|
|描述|注意：确保数据类型与实际应用需求一致，避免数据类型不匹配导致的运行时错误；在配置时应关注数据元素的访问权限和安全性需求；AUTOSAR CP 4.4标准中对此配置项的具体属性和使用方式有详细规定，应严格遵守。|
|多实例个数|0 - 1|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmSwcDataElementPrimitiveValue|
|描述|Primitive compare value.|
|描述|概述：DcmSwcDataElementPrimitiveValue配置项用于定义诊断服务中，软件组件数据元素的原始值，这些值通常用于读取或设置ECU中的数据。|
|描述|注意：在配置DcmSwcDataElementPrimitiveValue时，需要确保数据类型与软件组件中定义的数据类型一致；此外，还需注意数据的取值范围和精度要求，以避免在诊断通信过程中出现数据不匹配的问题；AUTOSAR CP 4.4标准中对于诊断数据元素的配置有详细的规范，需要遵循这些规范来确保诊断服务的正确性和可靠性。|
|多实例个数|1 - 1|
|取值范围|0 - 18446744073709551615|

#### 1.5.2. DcmModeRule

|容器属性|值（容器）|
|---|---|
|名称|DcmModeRule|
|描述|This container contains the configuration of a mode rule which represents a logical expression with DcmModeConditions or other DcmModeRules as arguments.|
|描述|概述：DcmModeRule配置项用于定义诊断会话控制和安全访问等模式下，诊断服务是否可用的规则，确保在特定的诊断会话层次或安全访问级别下，只有授权的诊断服务被允许执行。|
|描述|注意：在配置DcmModeRule时，需要确保规则与诊断服务的实际需求相匹配；对于每个诊断服务，都应该定义相应的模式规则，以避免在不适当的会话或安全级别下执行服务；AUTOSAR CP 4.4标准中可能对模式规则的表达方式和可用参数有具体的要求，需要遵循标准文档中的定义。|
|说明|All arguments are processed with the operator defined by DcmLogicalOperator, for instance: Argument_A AND Argument_B AND Argument_C|
|多实例个数|1 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|DcmLogicalOperator|
|描述|This parameter specifies the logical operator to be used in the logical expression. If the expression only consists of a single condition this parameter shall not be used.|
|描述|概述：DcmLogicalOperator 是一个配置项，用于定义诊断服务请求中多个条件之间的逻辑关系，例如“与”（AND）、“或”（OR）等，以支持复杂的服务请求条件组合。|
|描述|注意：在配置DcmLogicalOperator时，确保逻辑运算符的使用与服务请求的条件逻辑相匹配；逻辑运算符的组合需要遵循AUTOSAR规范中定义的语法和语义；不当的逻辑运算符配置可能导致诊断服务无法正确执行或者产生不预期的行为。|
|多实例个数|0 - 1|
|默认值|DCM_AND|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|DcmModeRuleNrcValue|
|描述|Optional parameter which defines the NRC to be sent in case the mode rule condition is not valid.|
|描述|概述：DcmModeRuleNrcValue 用于定义在诊断通信控制模块（Dcm）中，当特定模式规则不满足时返回的负面响应代码（NRC）。|
|描述|注意：确保每个模式规则关联的NRC符合ISO 14229标准中定义的错误代码；不正确的NRC设置可能导致诊断工具无法正确识别错误，影响车辆诊断过程；在配置时需考虑所有可能的模式规则和相应的诊断会话状态。|
|多实例个数|0 - 1|
|取值范围|1 - 255|

|配置项属性|值（选择引用配置项）|
|---|---|
|名称|DcmArgumentRef|
|描述|This is a choice reference either to a mode condition or a an other mode rule serving as sub-expression.|
|多实例个数|1 - inf|
|目标引用|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeCondition/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmProcessingConditions/DcmModeRule|

## 2. DcmGeneral

|容器属性|值（容器）|
|---|---|
|名称|DcmGeneral|
|描述|Contains general configuration parameters valid for the entire Dcm module.|
|描述|概述：DcmGeneral是AUTOSAR Diagnostic Communication Manager (DCM) 模块的一部分，它包含了DCM模块的通用配置参数，例如诊断会话控制、安全访问、响应时间等。|
|描述|注意：在配置DcmGeneral时，需要确保所有参数与项目的诊断需求相符合；参数的设置应遵循AUTOSAR CP 4.4标准的规范；在多个ECU中实现DCM时，应保持一致性以确保网络级诊断的互操作性。|
|多实例个数|1 - 1|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDDDIDStorage|
|描述|This configuration switch defines, whether DDDID definition is stored non-volatile or not.|
|描述|概述：DcmDDDIDStorage配置项用于定义诊断动态定义数据标识符（Dynamic Defined Data Identifier，DDDID）的存储属性，包括存储位置和存储条件，确保动态定义的数据可以在车辆诊断会话中被正确存储和访问。|
|描述|注意：在AUTOSAR CP 4.4标准中，需要确保DDDID的存储机制符合诊断服务的要求；存储位置应当保证数据的持久性和安全性；在设计存储策略时，应考虑到可能的内存限制和对存储介质的写入次数限制。|
|说明|true: DDDID are stored non-volatile false: DDDID are only maintained volatile|
|多实例个数|0 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：DcmDevErrorDetect 是一个配置参数，用于启用或禁用诊断通信管理器（Diagnostic Communication Manager）模块内部的开发错误检测机制。|
|描述|注意：在生产环境中通常禁用此功能以节省资源和提高性能；在开发和测试阶段，应启用此功能以便检测和报告潜在的错误；根据AUTOSAR CP 4.4标准，此配置项应当与系统的调试和诊断策略保持一致。|
|说明|\* true: detection and notification is enabled. \* false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmRespondAllRequest|
|描述|If set to FALSE the Dcm will not respond to diagnostic request that contains a service ID which is in the range from 0x40 to 0x7F or in the range from 0xC0 to 0xFF (Response IDs).|
|描述|概述：DcmRespondAllRequest配置项用于定义诊断通信管理器（Diagnostic Communication Manager）是否应对所有接收到的诊断请求进行响应，无论它们的来源或状态。|
|描述|注意：在配置DcmRespondAllRequest时，需要考虑安全和隐私问题，确保不会因响应所有请求而暴露敏感信息或功能；此配置项在AUTOSAR CP 4.4中应谨慎使用，以避免违反任何特定的通信协议规定；确保系统资源和性能在响应所有请求时不会受到影响。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（布尔参数配置项）|
|---|---|
|名称|DcmVersionInfoApi|
|描述|Preprocessor switch to enable or disable the output Version info of the functionality.|
|描述|概述：DcmVersionInfoApi 是一个配置选项，用于启用或禁用诊断通信管理器（Diagnostic Communication Manager）中的版本信息API，允许软件组件提供其版本信息。|
|描述|注意：在AUTOSAR CP 4.4标准中，确保在配置时考虑到系统的诊断需求和兼容性；不恰当的启用或禁用可能影响诊断工具的功能；版本信息API的使用应遵循项目的软件开发指南和规范。|
|多实例个数|1 - 1|
|默认值|false|

|配置项属性|值（浮点型参数配置项）|
|---|---|
|名称|DcmTaskTime|
|描述|Allow to configure the time for the periodic cyclic task. Please note: This configuration value shall be equal to the value in the RTE module.|
|描述|概述：DcmTaskTime配置项定义了诊断通信管理器（Diagnostic Communication Manager）模块中任务的调用周期，即Dcm主任务的执行频率。|
|描述|注意：该值必须与实际操作系统任务的调度周期相匹配；配置值过小可能导致系统过载，过大可能影响诊断响应时间；在多任务系统中，需要确保DcmTaskTime与其他任务的调度策略协调一致。|
|说明|The AUTOSAR configuration standard is to use SI units, so this parameter is defined as float value in seconds. Dcm configuration tools must convert this float value to the appropriate value format for the use in the software implementation of Dcm. min: A negative value and zero is not allowed. upperMultiplicity: Exactly one TaskTime must be specified per configuration. lowerMultiplicity: Exactly one TaskTime must be specified per configuration.|
|多实例个数|1 - 1|
|默认值|0.01|
|取值范围|0 - Inf|

|配置项属性|值（字符串参数配置项）|
|---|---|
|名称|DcmHeaderFileInclusion|
|描述|Name of the header file(s) to be included by the Dcm module containing the used C-callback declarations. Dcm_Callout_Stubs.h is generated by default and does not need to be configured separately.|
|描述|概述：DcmHeaderFileInclusion配置项用于指定在Diagnostics Communication Manager (DCM) 模块中包含的额外头文件，这些头文件可能包含用户定义的宏、类型定义或者外部函数声明。|
|描述|注意：在配置DcmHeaderFileInclusion时，确保包含的头文件与AUTOSAR标准兼容，不会引入非标准的依赖；头文件应当存在于项目的包含路径中，以避免编译错误；如果项目中使用了特定的编译器或者特殊的编译设置，需要确保这些头文件在这些环境下也能正确编译。|
|多实例个数|0 - inf|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|DcmVinRef|
|描述|Reference to the Did containing the VIN Information.|
|描述|概述：DcmVinRef配置项用于定义诊断通信管理器（Diagnostic Communication Manager）中车辆识别号（Vehicle Identification Number, VIN）的引用，确保在执行诊断服务时能够正确地访问和报告VIN信息。|
|描述|注意：在配置DcmVinRef时，需要确保引用的数据元素与实际存储VIN的内存或数据结构相匹配；此外，应当注意数据元素的访问权限，以确保在诊断会话中可以被合法访问；根据AUTOSAR CP 4.4标准，还应确保VIN的格式和长度符合相关法规和标准要求。|
|说明|This parameter is needed for function Dcm_GetVin|
|多实例个数|0 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Dcm/DcmConfigSet/DcmDsp/DcmDspDid|
