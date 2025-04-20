#  MemIf 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|MemIf|
|描述|Configuration of the MemIf (Memory Abstraction Interface) module.|
|描述|概述：MemIf是一个模块接口，它为上层模块（如NvM）提供了统一的接口来访问底层存储驱动，例如EEPROM和Flash驱动。|
|描述|注意：在配置MemIf时，需要确保它正确地映射到底层存储驱动；MemIf配置应与底层驱动的能力和要求保持一致；MemIf的配置参数应遵循标准规定的属性和数据类型。|
|多实例个数|0 - 1|

## 1. MemIfGeneral

| 容器属性 | 值（容器） |
|-|-|
|名称|MemIfGeneral|
|描述|Configuration of the memory abstraction interface (Memif) module.|
|描述|概述：MemIfGeneral 是一个配置容器，包含了用于存储管理接口（Memory Interface）的全局配置参数，这些参数影响存储设备（如EEPROM或Flash）的管理和访问。|
|描述|注意：需要确保MemIfGeneral中的参数与所使用的存储设备的特性相匹配；此外，配置参数应当满足系统的性能和可靠性要求；在配置时，还应注意与其他BswM模块的兼容性和交互。|
|多实例个数|1 - 1|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|MemIfDevErrorDetect|
|描述|Switches the development error detection and notification on or off.|
|描述|概述：MemIfDevErrorDetect是一个配置参数，用于启用或禁用内存映射接口（Memory Mapping Interface，MemIf）层的开发错误检测功能，以便在开发阶段发现潜在错误。|
|描述|注意：当设置为启用（TRUE）时，系统将检查API调用的参数有效性等；在生产代码中，通常建议禁用此功能以优化性能；确保与底层存储驱动的错误处理机制兼容。|
|说明|* true: detection and notification is enabled. * false: detection and notification is disabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|MemIfVersionInfoApi|
|描述|Pre-processor switch to enable / disable the API to read out the modules version information.|
|描述|概述：MemIfVersionInfoApi是一个配置选项，用于启用或禁用内存抽象接口（Memory Abstraction Interface）的版本信息API，允许软件组件获取当前内存接口模块的版本信息。|
|描述|注意：启用此API可能会增加代码的ROM占用；如果系统对内存空间非常敏感，需要仔细考虑是否启用；此API主要用于开发和测试阶段，以便于诊断和兼容性检查。|
|说明|true: Version info API enabled. false: Version info API disabled.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（整型参数配置项） |
|-|-|
|名称|MemIfNumberOfDevices|
|描述|Concrete number of underlying memory abstraction modules.|
|描述|概述：MemIfNumberOfDevices 配置项用于定义系统中可用的内存设备的数量，这有助于内存管理接口模块正确管理各个内存设备。|
|描述|注意：确保此配置项的值正确反映了实际硬件中存在的内存设备数量；过多或过少的设备数量配置可能导致内存管理错误；此配置项应与实际硬件和系统需求严格对应。|
|说明|Calculation Formula: Count number of configured EA and FEE modules.|
|多实例个数|1 - 1|
|取值范围|1 - 2|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|MemIfUseEepromStore|
|描述|MemIf Use Eeprom to store data.|
|描述|概述：MemIf模块使用Eeprom的硬件和驱动去存储数据。|
|描述|注意：需要保证实际软件中已具备Eeprom的驱动。|
|说明|true: Use Eeprom to store. false: not Use Eeprom to store.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|MemIfUseFlashStore|
|描述|MemIf Use Flash to store data.|
|描述|概述：MemIf模块使用Flash的硬件和驱动去存储数据。|
|描述|注意：需要保证实际软件中已具备Flash的驱动。|
|说明|true: Use Flash to store. false: not Use Flash to store.|
|多实例个数|1 - 1|
|默认值|false|

