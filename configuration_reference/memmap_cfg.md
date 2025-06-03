# Memmap 配置项参考文档

| 容器属性 | 值（容器） |
|-|-|
|名称|Memmap|
|描述|Configuration of the Memmap module.|
|描述|概述：Memmap 模块的配置|
|多实例个数|0 - 1|

## 1. MemmapLayer

| 容器属性 | 值（容器） |
|-|-|
|名称|MemmapLayer|
|描述|Defines the name of the memmap layer provided.|
|描述|概述：MemmapLayer 配置项用于指定内存映射中的软件层级，允许多个内存映射软件层级。|
|描述|注意：用户必须配置至少一个内存映射软件层级，并存在唯一一个内部软件层级，作为内部底层的软件层级。|
|多实例个数|1 - 16|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|InternalLayer|
|描述|true: the layer is defined as the internal memmap layer.|
|描述|概述：InternalLayer说明该层级作为内部底层的内存映射软件层级。|
|描述|注意：必须存在唯一一个InternalLayer。|
|说明|false: the layer is not used as an internal memmap layer.|
|多实例个数|1 - 1|
|默认值|false|

## 2. MemmapModule

| 容器属性 | 值（容器） |
|-|-|
|名称|MemmapModule|
|多实例个数|0 - 65535|
|描述|Defines the name of a memmap module.|
|描述|概述：MemmapModule 配置项用于指定内存映射中的用户自定义模块的模块名称。|
|描述|注意：用户可自定义多个内存映射模块，操作系统会为每一个模块生成对应的模块头文件供用户使用。|

| 配置项属性 | 值（布尔参数配置项） |
|-|-|
|名称|MemmapUseCalibration|
|描述|true: generate calibration mapping for the module.|
|描述|概述：MemmapUseCalibration说明该模块需要生成calibration段。|
|描述|注意：如果在不需要calibration段的情况下，打开了这个选项，会造成冗余代码。|
|说明|false: the module doesn't require calibration mapping.|
|多实例个数|1 - 1|
|默认值|false|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|MemmapApplicationRef|
|描述|Defines the name of the applications the module is related to.|
|描述|概述：MemmapApplicationRef 配置项用于指定模块相关的applications。|
|描述|注意：用户可以配置关联多个application，根据无关联，单关联或多关联，会产生不一样的内存映射宏供用户使用。|
|多实例个数|0 - 512|
|目标引用项的路径|/AUTOSAR/EcucDefs/Os/OsApplication|

| 配置项属性 | 值（关联引用配置项） |
|-|-|
|名称|MemmapUseLayer|
|描述|Defines the name of the memmap layer the module is related to.|
|描述|概述：MemmapUseLayer 配置项用于指定模块关联的内存映射软件层级。|
|描述|注意：用户必须将配置的内存映射模块定义到一个内存映射软件层级上。|
|多实例个数|1 - 1|
|目标引用项的路径|/AUTOSAR/EcucDefs/Memmap/MemmapLayer|
