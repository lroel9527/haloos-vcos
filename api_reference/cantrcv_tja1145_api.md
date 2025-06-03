# cantrcv_tja1145 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `cantrcv_tja1145_init`

|属性|描述|
|---|---|
|函数定义|`cantrcv_tja1145_init(const cantrcv_cfg_t *cfg_ptr)`|
|简要描述|CanTrcv1145初始化函数 |
|详细说明| 初始化函数 |
|同步/异步|同步|
|可重入性|不支持重入|

## `cantrcv_tja1145_op_mode_set`

|属性|描述|
|---|---|
|函数定义|`cantrcv_tja1145_op_mode_set(uint8 cantrcv_idx`|
|简要描述|CanTrcv1145设置控制器模式函数 |
|详细说明|CanTrcv1145设置控制器模式函数 |
|返回值|E_OK 控制器模式请求已被接受 |
|返回值|E_NOT_OK 控制器模式请求未被接受 |
|同步/异步|同步|
|可重入性|不支持重入|
