# nm 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `nm_init`

|属性|描述|
|---|---|
|函数定义|`nm_init(void)`|
|简要描述|Nm Init |
|详细说明|初始化 |
|参数[输入]|`未知类型 id_net` Communication channel handle |
|同步/异步|Synchronous|
|可重入性|Reentrant|

## `nm_pas_stup`

|属性|描述|
|---|---|
|函数定义|`nm_pas_stup(const network_handle_type id_net)`|
|简要描述|Nm passive start up |
|详细说明|被动启动|
|参数[输入]|`未知类型 id_net` Communication channel handle @ret_val E_OK Passive start successful Passive start failed |
|同步/异步|Synchronous|
|可重入性|Reentrant|
