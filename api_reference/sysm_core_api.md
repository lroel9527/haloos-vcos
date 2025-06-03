# sysm_core 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `bswm_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void,) bswm_init(const bswm_config_type *config_ptr)`|
|简要描述|初始化 BswM |
|详细说明|请求模式的通用函数调用|
|参数[输入]|`config_ptr` 配置指针 |
|同步/异步|同步|
|可重入性|可重入|

## `bswm_get_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType,) bswm_get_status(bswm_init_status_t *bswm_status)`|
|简要描述|获取BswM的初始化状态 |
|详细说明|获取BswM的初始化状态|
|参数[输入]|`bswm_status` BswM状态指针 |
|同步/异步|同步|
|可重入性|可重入|
