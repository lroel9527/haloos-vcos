# det 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `Det_Init`

|属性|描述|
|---|---|
|函数定义|`void Det_Init(const Det_ConfigType* ConfigPtr)`|
|简要描述|初始化det模块 |
|详细说明|初始化det模块 |
|参数[输入]|`ConfigPtr` det配置指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `Det_DeInit`

|属性|描述|
|---|---|
|函数定义|`void Det_DeInit(void)`|
|简要描述|反初始化det模块 |
|详细说明|反初始化det模块 |
|同步/异步|同步|
|可重入性|不可重入|

## `Det_Start`

|属性|描述|
|---|---|
|函数定义|`void Det_Start(void)`|
|简要描述|det模块开始工作 |
|详细说明|det模块开始工作，在Det_Init后调用 |
|同步/异步|同步|
|可重入性|不可重入|

## `Det_ReportError`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType Det_ReportError(uint16 ModuleId, uint8 InstanceId, uint8 ApiId, uint8 ErrorId)`|
|简要描述|开发错误上报 |
|详细说明|开发错误上报 |
|参数[输入]|`ModuleId` 模块Id号 |
|参数[输入]|`InstanceId` 实例Id号，Bsw模块对应的就是多核多Application实例化 |
|参数[输入]|`ApiId` 发生错误所在的API Id号 |
|参数[输入]|`ErrorId` 发生错误的错误类型号 |
|返回值|E_OK 故障上报成功 |
|返回值|E_NOT_OK 故障上报失败 |
|同步/异步|异步|
|可重入性|可重入|

## `Det_ReportRuntimeError`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType Det_ReportRuntimeError(uint16 ModuleId, uint8 InstanceId, uint8 ApiId, uint8 ErrorId)`|
|简要描述|运行错误上报 |
|详细说明|运行错误上报，通常是运行时产生的错误，如通信丢包 |
|参数[输入]|`ModuleId` 模块Id号 |
|参数[输入]|`InstanceId` 实例Id号，Bsw模块对应的就是多核多Application实例化 |
|参数[输入]|`ApiId` 发生错误所在的API Id号 |
|参数[输入]|`ErrorId` 发生错误的错误类型号 |
|返回值|E_OK RuntimeError故障上报成功 |
|返回值|E_NOT_OK RuntimeError故障上报失败 |
|同步/异步|异步|
|可重入性|可重入|

## `Det_ReportTransientFault`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType Det_ReportTransientFault(uint16 ModuleId, uint8 InstanceId, uint8 ApiId, uint8 FaultId)`|
|简要描述|瞬态错误上报 |
|详细说明|瞬态错误上报，例如存储等产生的读写错误 |
|参数[输入]|`ModuleId` 模块Id号 |
|参数[输入]|`InstanceId` 实例Id号，Bsw模块对应的就是多核多Application实例化 |
|参数[输入]|`ApiId` 发生错误所在的API Id号 |
|参数[输入]|`ErrorId` 发生错误的错误类型号 |
|返回值|E_OK TransientFault故障上报成功 |
|返回值|E_NOT_OK TransientFault故障上报失败 |
|同步/异步|异步|
|可重入性|可重入|

## `Det_ReportErrorWithInfo`

|属性|描述|
|---|---|
|函数定义|`Std_ReturnType Det_ReportErrorWithInfo(uint32 errorId, uint8* info,uint8 len)`|
|简要描述|错误码上报 |
|详细说明|错误码上报，可以携带不大于20字节的额外信息吐出 |
|参数[输入]|`errorId` 发生错误的错误类型号 |
|参数[输入]|`info` 指针,指向想要发送的数据 |
|参数[输入]|`len` 发送的数据长度,最大不超过20字节 |
|返回值|E_OK TransientFault故障上报成功 |
|返回值|E_NOT_OK TransientFault故障上报失败 |
|同步/异步|异步|
|可重入性|可重入|

## `Det_GetVersionInfo`

|属性|描述|
|---|---|
|函数定义|`void Det_GetVersionInfo(Std_VersionInfoType* vi)`|
|简要描述|获取版本号 |
|详细说明|版本号获取 |
|参数[输入]|`vi` 版本号结构体指针 |
|同步/异步|同步|
|可重入性|可重入|

## `Det_SetTokenBucketCapacity`

|属性|描述|
|---|---|
|函数定义|`void Det_SetTokenBucketCapacity(sint32 cap)`|
|简要描述|设置令牌桶流量大小 |
|详细说明|设置令牌桶流量大小，设置时自动补满令牌 |
|参数[输入]|`cap` 容量 |
|同步/异步|同步|
|可重入性|可重入|

## `Det_GetTokenBucketCapacity`

|属性|描述|
|---|---|
|函数定义|`sint32 Det_GetTokenBucketCapacity(void)`|
|简要描述|获取令牌桶Det流量控制阈值大小 |
|详细说明|获取令牌桶Det流量控制阈值大小 |
|返回值|sint32 令牌桶容量大小 |
|同步/异步|同步|
|可重入性|可重入|
