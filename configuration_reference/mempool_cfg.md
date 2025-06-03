# MemPool 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|MemPool|
|描述|Configuration of the MemPool (Memory Pool) module.|
|描述|概述：MemPool是AUTOSAR软件架构中的一个核心组件，负责给底层基础软件提供内存分配功能|
|多实例个数|0 - 1|

## 1. MemModule

|容器属性|值（容器）|
|---|---|
|名称|MemModule|
|描述|This container contains the configuration of the mempool modules and their subcontainers. It is responsible for managing and configuring memory pool-related parameters while providing necessary resources and functionality to other modules. This module helps optimize memory usage and enhances system performance.|
|描述|概述：该容器包含了内存池模块的配置及其子容器。它用于管理和配置内存池相关的参数，并为其他模块提供必要的资源和功能支持。通过该模块，可以有效地优化内存使用，并提高系统性能。|
|描述|注意：在配置模块时，务必确保模块名称具有唯一性和标识性，以避免在软件架构中引发混淆。|
|多实例个数|0 - inf|

|配置项属性|值（外部引用配置项）|
|---|---|
|名称|BswModuleRef|
|描述|Represents one instance of a Bsw-Module configured on one ECU.|
|描述|概述：BswModuleRef用于定义Bsw模块实例，它指定了基础软件模块实例的配置，包括其名称和相关属性，以便在运行时环境中进行管理和调度。|
|描述|注意：在配置BswModuleRef时，确保模块实例名称的唯一性，避免与其他Bsw模块实例名称冲突；在多模块系统中，合理规划每个模块实例的资源和优先级，以保证系统的稳定性和性能。|
|多实例个数|1 - 1|
|目标类型|ECUC-MODULE-CONFIGURATION-VALUES|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|OsApplicationRef|
|描述|The owner application of the current isolate module.|
|描述|概述：OsApplicationRef配置项用于指定当前软件组件所部署的OsApplication的引用。|
|描述|注意：在配置OsApplicationRef时，需要确保引用的OS应用程序已经在系统中定义；此外，该引用必须符合操作系统的隔离和保护级别要求；在多核系统中，还需考虑应用程序与特定核心的绑定关系。|
|多实例个数|1 - 31|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsApplication|

|配置项属性|值（关联引用配置项）|
|---|---|
|名称|MemPoolRef|
|描述|The MemPoolRef configuration is used to reference already created memory pools, enabling easier management and operation of the memory pool within the application.|
|描述|概述：MemPoolRef 配置用于引用已创建的内存池，便于在应用中进行内存池的管理与操作。|
|描述|注意：在配置 MemPoolRef 时，需确保被引用的内存池 (mempool) 满足当前模块的业务需求，以保证系统的正常运行和性能优化。|
|多实例个数|1 - inf|
|目标引用项的路径|/AUTOSAR/EcucDefs/MemPool/MemPool|

## 2. MemPool

|容器属性|值（容器）|
|---|---|
|名称|MemPool|
|描述|MemPool is used to configure specific memory pool-related information, allowing the system to manage and allocate memory resources according to the specific needs of the application.|
|描述|概述：Module配置项在AUTOSAR中用于定义软件模块的属性，包括模块的名称、供应商信息、版本号等，是软件组件描述文件中的一个基本构成部分。|
|描述|注意：在配置Module时，确保模块名称的唯一性和标识性，以避免在软件架构中产生混淆；遵循AUTOSAR规定的版本号格式，以确保兼容性和追溯性；供应商信息应准确无误，以便于模块的管理和维护。|
|多实例个数|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|MemBlockCount|
|描述|MemBlockCount is used to define the number of memory blocks.|
|描述|概述：MemBlockCount 用于定义内存块的数量。|
|描述|注意：MemBlockCount 和 MemBlockSize 一起决定了内存的总大小。因此，在配置时，需要根据实际物理内存大小进行评估和调整。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|MemBlockSize|
|描述|MemBlockSize is used to define the size of a single memory block.|
|描述|概述：MemBlockSize 用于定义单个内存块的大小。|
|描述|注意：MemBlockCount 和 MemBlockSize 一起决定了内存的总大小。因此，在配置时，需要根据实际物理内存大小进行评估和调整。|
|多实例个数|1 - 1|
|默认值|0|
|取值范围|0 - inf|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|MemAlignment|
|描述|MemAlignment is used to define the memory alignment method. Proper configuration of MemAlignment ensures that memory is allocated according to specific alignment rules, improving memory access efficiency and avoiding potential performance issues.|
|描述|概述：MemAlignment 用于定义内存对齐的方式。通过合理配置 MemAlignment，可以确保内存按特定的对齐规则进行分配，从而提升内存访问效率并避免潜在的性能问题。|
|描述|注意：MemAlignment 用于定义内存对齐的方式。通常，MemAlignment 最好是 4 的倍数，因为 4 字节对齐可以减少内存空间的浪费，优化内存的使用效率，避免不必要的内存碎片。|
|多实例个数|1 - 1|
|默认值|4|
|取值范围|0 - inf|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|MemType|
|描述|MemType is used to define the type of the memory pool. By configuring MemType, the specific type of the memory pool can be specified to meet the requirements of different application scenarios, enabling more efficient memory management and resource utilization.|
|描述|概述：MemType 用于定义内存池的类型。通过配置 MemType，可以指定内存池的具体类型，以满足不同应用场景的需求，从而实现更高效的内存管理和资源利用。|
|描述|注意：MemType 用于定义内存池的类型，配置项的值通常包括 AUTOMATIC、GLOBAL 和 CORE，当值为 AUTOMATIC 时，系统会自动判断是 GLOBAL 还是 PRIVATE 模式；PRIVATE 模式下仅关联相同应用的模块能访问，GLOBAL 模式下所有模块可访问，CORE 模式下仅在同一核心上的关联应用模块可访问。|
|多实例个数|1 - 1|
|默认值|AUTOMATIC|

|配置项属性|值（整型参数配置项）|
|---|---|
|名称|CoreID|
|描述|CoreID is used to define the specific core to which the memory pool is associated.|
|描述|概述：CoreID 用于定义内存池关联的具体核心。|
|描述|注意：当配置了 CoreID 后，内存池将被限定在指定的核心上，以确保只有在该核心上的应用模块才能访问该内存池，其他核心上的模块将无法访问该内存池。|
|多实例个数|0 - 1|
|默认值|0|
|取值范围|0 - 255|
