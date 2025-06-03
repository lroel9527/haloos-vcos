# sysm_init 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `ecum_get_version_info`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, ECUM_CODE) ecum_get_version_info(Std_VersionInfoType *version_info)`|
|简要描述|获取 EcuM 版本信息 |
|详细说明|获取 EcuM 版本信息 |
|参数[输出]|`Std_VersionInfoType version_info` 指向要填充的版本信息结构的指针 |
|同步/异步|同步|
|可重入性|不可重入|

## `ecum_get_state`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, ECUM_CODE) ecum_get_state(ecum_state_t *state)`|
|简要描述|获取 EcuM 当前状态 |
|详细说明|获取 EcuM 当前状态 |
|参数[输出]|`ecum_state_t state` 指向存储 EcuM 当前状态的变量的指针 |
|返回值|E_OK 获取 EcuM 状态成功。|
|返回值|E_NOT_OK 获取 EcuM 状态失败。|
|同步/异步|同步|
|可重入性|可重入|

## `ecum_select_shutdown_target`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, ECUM_CODE) ecum_select_shutdown_target(ecum_shutdown_target_t shutdownTarget, ecum_shutdown_mode_t sleepMode)`|
|简要描述|选择对应的 ShutdownTarget |
|详细说明|用于选择EcuM不同的 ShutdownTarget 和 sleepMode |
|参数[输入]|`ecum_shutdown_target_t shutdownTarget` ShutdownTarget类型 |
|参数[输入]|`ecum_shutdown_mode_t sleepMode` Shutdown模式 |
|返回值|E_OK 选择 ShutdownTarget 成功|
|返回值|E_NOT_OK 选择 ShutdownTarget 失败|
|同步/异步|同步|
|可重入性|可重入|

## `ecum_get_shutdown_target`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, ECUM_CODE) ecum_get_shutdown_target(ecum_shutdown_target_t *shutdownTarget, ecum_shutdown_mode_t *sleepMode)`|
|简要描述|获取 ShutdownTarget |
|详细说明| 获取当前的 ShutdownTarget 和 sleepMode |
|参数[输出]|`ecum_shutdown_target_t shutdownTarget` 指向 ShutdownTarget 的变量的指针 |
|参数[输出]|`ecum_shutdown_mode_t sleepMode` 指向 sleepMode 的变量的指针 |
|返回值|E_OK 获取 ShutdownTarget 成功 |
|返回值|E_NOT_OK 获取 ShutdownTarget 失败 |
|同步/异步|同步|
|可重入性|可重入|

## `ecum_get_last_shutdown_target`

|属性|描述|
|---|---|
|函数定义|`FUNC(Std_ReturnType, ECUM_CODE) ecum_get_last_shutdown_target(ecum_shutdown_target_t *shutdownTarget, ecum_shutdown_mode_t *sleepMode)`|
|简要描述|获取上一次的 ShutdownTarget |
|详细说明|此函数用于获取上一次的 ShutdownTarget 和 sleepMode |
|参数[输出]|`ecum_shutdown_target_t shutdownTarget` 指向上一次 ShutdownTarget 的变量的指针 |
|参数[输出]|`ecum_shutdown_mode_t sleepMode` 指向上一次 sleepMode 的变量的指针 |
|返回值|E_OK 获取上一次的 ShutdownTarget 成功 |
|返回值|E_NOT_OK 获取上一次的 ShutdownTarget 失败 |
|同步/异步|同步|
|可重入性|可重入|

## `ecum_get_pending_wakeup_events`

|属性|描述|
|---|---|
|函数定义|`FUNC(ecum_wakeup_source_t, ECUM_CODE) ecum_get_pending_wakeup_events(void)`|
|简要描述|获取当前挂起的唤醒事件 |
|详细说明|获取当前的唤醒事件 |
|同步/异步|同步|
|可重入性|不可重入|

## `ecum_get_status_of_wakeup_source`

|属性|描述|
|---|---|
|函数定义|`FUNC(ecum_wakeup_status_t, ECUM_CODE) ecum_get_status_of_wakeup_source(ecum_wakeup_source_t sources)`|
|简要描述|获取当前唤醒源的状态 |
|详细说明|此函数用于获取当前唤醒源的状态 |
|参数[输入]|`ecum_wakeup_source_t sources` 唤醒源 |
|同步/异步|同步|
|可重入性|不可重入|

## `has_run_requests`

|属性|描述|
|---|---|
|函数定义|`FUNC(boolean, ECUM_CODE) has_run_requests(void)`|
|简要描述|判断当前是否有用户存在用户 RUN 请求 |
|详细说明|判断当前是否有用户存在用户 RUN 请求 |
|同步/异步|同步|
|可重入性|不可重入|

## `ecum_error_hook`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, ECUM_CODE) ecum_error_hook(uint16 reason)`|
|简要描述|EcuM 通过此函数向DET报告错误 |
|详细说明|EcuM 向DET报告错误 |
|参数[输入]|`uint16 reason` 错误原因代码 |
|同步/异步|同步|
|可重入性|不可重入|

## `ecum_determine_pb_configuration`

|属性|描述|
|---|---|
|函数定义|`FUNC(struct ecum_config_s *, ECUM_CODE) ecum_determine_pb_configuration(void)`|
|简要描述|获取保存各模块的配置指针 |
|详细说明|此函数用于获取保存各个模块配置的全局配置指针。|
|同步/异步|同步|
|可重入性|可重入|

## `ecum_check_ram_hash`

|属性|描述|
|---|---|
|函数定义|`FUNC(uint8, ECUM_CODE) ecum_check_ram_hash(void)`|
|简要描述|通过检查哈希值来验证 RAM 数据完整性 |
|详细说明|休眠 Halt 模式下用于检验哈希值来验证 RAM 数据完整性。|
|返回值|0 RAM 完整性测试失败。|
|返回值|非0 RAM 完整性测试成功。|
|同步/异步|同步|
|可重入性|不可重入|

## `ecum_on_wakeup_reaction`

|属性|描述|
|---|---|
|函数定义|`FUNC(ecum_wakeup_reaction_t, ECUM_CODE) ecum_on_wakeup_reaction(ecum_wakeup_reaction_t wact)`|
|简要描述|标记唤醒验证结果 |
|详细说明|在唤醒验证流程中，用于提示处于唤醒验证结果反馈阶段。|
|参数[输入]|`ecum_wakeup_reaction_t wact` 唤醒反馈动作类型。 |
|同步/异步|同步|
|可重入性|不可重入|
