# e2e 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `e2e_p01_protect`

|属性|描述|
|---|---|
|函数定义|`e2e_p01_protect(const e2e_p01_config_type *config_ptr, e2e_p01_protect_state_type *state_ptr, uint8 *data_ptr)`|
|简要描述|E2E profile 1的保护函数 |
|详细说明|使用e2e profile 1保护要传输的数组/缓冲区|
|参数[输入]|`e2e_p01_config_type config_ptr` 指向静态配置的指针 |
|参数[输出]|`e2e_p01_protect_state_type state_ptr` 指向通信状态的指针 |
|参数[输出]|`uint8 * data_ptr` 指向要保护的数据的指针 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_INTERR 内部库错误|
|返回值|E2E_E_OK 保护成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p01_check`

|属性|描述|
|---|---|
|函数定义|`e2e_p01_check(const e2e_p01_config_type *config_ptr, e2e_p01_check_state_type *state_ptr, const uint8 *data_ptr)`|
|简要描述|E2E profile 1的检查函数 |
|详细说明|使用e2e profile 1对接收到的数据进行检查。包括crc计算、处理计数器和数据id|
|参数[输入]|`e2e_p01_config_type config_ptr` 指向配置文件的指针，用于配置检查规则 |
|参数[输出]|`e2e_p01_check_state_type state_ptr` 指向通信状态的指针，用于记录检查状态 |
|参数[输出]|`const uint8 * data_ptr` 指向要检查的数据的指针 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_INTERR 内部库错误|
|返回值|E2E_E_OK 检查成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p01_map_status_to_sm`

|属性|描述|
|---|---|
|函数定义|`e2e_p01_map_status_to_sm(Std_ReturnType check_return, uint8 check_status, boolean profile_behavior)`|
|简要描述|E2E profile 1的状态映射函数 |
|详细说明|将profile 1的检查状态映射为通用的检查状态，可由e2e状态机的检查函数使用 E2E profile 1提供了更精细的状态，但对于e2e状态机来说这并不相关|
|参数[输入]|`Std_ReturnType check_return` e2e_p01_check的返回值 |
|参数[输入]|`uint8 check_status` 通信状态 |
|参数[输入]|`boolean profile_behavior` FALSE: r4.2之前的逻辑 TRUE: r4.2之后的逻辑 |
|返回值|用于e2elib状态机的标准状态值|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p02_protect`

|属性|描述|
|---|---|
|函数定义|`e2e_p02_protect(const e2e_p02_config_type *config_ptr, e2e_p02_protect_state_type *state_ptr, uint8 *data_ptr)`|
|简要描述|E2E profile 2的保护函数 |
|详细说明|使用e2e profile 2保护要传输的数组/缓冲区|
|参数[输入]|`e2e_p02_config_type config_ptr` 指向静态配置的指针 |
|参数[输出]|`e2e_p02_protect_state_type state_ptr` 指向通信状态的指针 |
|参数[输出]|`uint8 * data_ptr` 指向要保护的数据的指针 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_OK 保护成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p02_check`

|属性|描述|
|---|---|
|函数定义|`e2e_p02_check(const e2e_p02_config_type *config_ptr, e2e_p02_check_state_type *state_ptr, const uint8 *data_ptr)`|
|简要描述|E2E profile 2的检查函数 |
|详细说明|使用e2e profile 2对接收到的数据进行检查。包括crc计算、处理计数器和数据id|
|参数[输入]|`e2e_p02_config_type config_ptr` 指向配置文件的指针，用于配置检查规则 |
|参数[输出]|`e2e_p02_check_state_type state_ptr` 指向通信状态的指针，用于记录检查状态 |
|参数[输出]|`const uint8 * data_ptr` 指向要检查的数据的指针 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_OK 检查成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p02_map_status_to_sm`

|属性|描述|
|---|---|
|函数定义|`e2e_p02_map_status_to_sm(Std_ReturnType check_return, uint8 check_status, boolean profile_behavior)`|
|简要描述|E2E profile 2的状态映射函数 |
|详细说明|将profile 2的检查状态映射为通用的检查状态，可由e2e状态机的检查函数使用 E2E profile 2提供了更精细的状态，但对于e2e状态机来说这并不相关|
|参数[输入]|`Std_ReturnType check_return` e2e_p02_check的返回值 |
|参数[输入]|`uint8 check_status` 通信状态 |
|参数[输入]|`boolean profile_behavior` FALSE: r4.2之前的逻辑 TRUE: r4.2之后的逻辑 |
|返回值|用于e2elib状态机的标准状态值|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p04_protect`

|属性|描述|
|---|---|
|函数定义|`e2e_p04_protect(const e2e_p04_config_type *config_ptr, e2e_p04_protect_state_type *state_ptr, uint8 *data_ptr, uint16 length)`|
|简要描述|E2E profile 4的保护函数 |
|详细说明|使用e2e profile 4保护要传输的数组/缓冲区|
|参数[输入]|`e2e_p04_config_type config_ptr` 指向静态配置的指针 |
|参数[输出]|`e2e_p04_protect_state_type state_ptr` 指向通信状态的指针 |
|参数[输出]|`uint8 * data_ptr` 指向要保护的数据的指针 |
|参数[输入]|`uint16 length` 数据数组长度 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_INTERR 内部库错误|
|返回值|E2E_E_OK 保护成功|
|同步/异步|同步|
|可重入性|不可重入|

## `e2e_p04_check`

|属性|描述|
|---|---|
|函数定义|`e2e_p04_check(const e2e_p04_config_type *config_ptr, e2e_p04_check_state_type *state_ptr, const uint8 *data_ptr, uint16 length)`|
|简要描述|E2E profile 2的检查函数 |
|详细说明|使用e2e profile 2对接收到的数据进行检查。包括crc计算、处理计数器和数据id|
|参数[输入]|`e2e_p04_config_type config_ptr` 指向配置文件的指针，用于配置检查规则 |
|参数[输出]|`e2e_p04_check_state_type state_ptr` 指向通信状态的指针，用于记录检查状态 |
|参数[输出]|`const uint8 * data_ptr` 指向要检查的数据的指针 |
|参数[输入]|`uint16 length` 数据数组长度 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_OK 检查成功|
|同步/异步|同步|
|可重入性|不可重入|

## `e2e_p04_map_status_to_sm`

|属性|描述|
|---|---|
|函数定义|`e2e_p04_map_status_to_sm(Std_ReturnType check_return, uint8 check_status)`|
|简要描述|E2E profile 4的状态映射函数 |
|详细说明|将profile 4的检查状态映射为通用的检查状态，可由e2e状态机的检查函数使用 E2E profile 4提供了更精细的状态，但对于e2e状态机来说这并不相关|
|参数[输入]|`Std_ReturnType check_return` e2e_p04_check的返回值 |
|参数[输入]|`uint8 check_status` 通信状态 |
|返回值|用于e2elib状态机的标准状态值|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p05_check`

|属性|描述|
|---|---|
|函数定义|`e2e_p05_check(const e2e_p05_config_type *config_ptr, e2e_p05_check_state_type *state_ptr, const uint8 *data_ptr, uint16 length)`|
|简要描述|E2E profile 5的检查函数 |
|详细说明|使用e2e profile 5对接收到的数据进行检查。包括crc计算、处理计数器和数据id|
|参数[输入]|`e2e_p05_config_type config_ptr` 指向配置文件的指针，用于配置检查规则 |
|参数[输出]|`e2e_p05_check_state_type state_ptr` 指向通信状态的指针，用于记录检查状态 |
|参数[输出]|`const uint8 * data_ptr` 指向要检查的数据的指针 |
|参数[输入]|`uint16 length` 数据数组长度 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_OK 检查成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p05_protect`

|属性|描述|
|---|---|
|函数定义|`e2e_p05_protect(const e2e_p05_config_type *config_ptr, e2e_p05_protect_state_type *state_ptr, uint8 *data_ptr, uint16 length)`|
|简要描述|E2E profile 5的保护函数 |
|详细说明|使用e2e profile 4保护要传输的数组/缓冲区|
|参数[输入]|`e2e_p05_config_type config_ptr` 指向静态配置的指针 |
|参数[输出]|`e2e_p05_protect_state_type state_ptr` 指向通信状态的指针 |
|参数[输出]|`uint8 * data_ptr` 指向要保护的数据的指针 |
|参数[输入]|`uint16 length` 数据数组长度 |
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_INTERR 内部库错误|
|返回值|E2E_E_OK 保护成功|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_p05_map_status_to_sm`

|属性|描述|
|---|---|
|函数定义|`e2e_p05_map_status_to_sm(Std_ReturnType check_return, uint8 check_status)`|
|简要描述|E2E profile 5的状态映射函数 |
|详细说明|将profile 5的检查状态映射为通用的检查状态，可由e2e状态机的检查函数使用 E2E profile 5提供了更精细的状态，但对于e2e状态机来说这并不相关|
|参数[输入]|`Std_ReturnType check_return` e2e_p05_check的返回值 |
|参数[输入]|`uint8 check_status` 通信状态 |
|返回值|用于e2elib状态机的标准状态值|
|同步/异步|同步|
|可重入性|可重入|

## `e2e_sm_check`

|属性|描述|
|---|---|
|函数定义|`e2e_sm_check(uint8 profile_status, const e2e_sm_config_type *config_ptr, e2e_sm_check_state_type *state_ptr)`|
|简要描述|检查本次profile调用的结果，并根据结果更新状态机状态 |
|详细说明||
|参数[输入]|`uint8 profile_status` 本次状态 |
|参数[输入]|`e2e_sm_config_type config_ptr` 指向配置文件的指针，用于配置检查规则 |
|参数[输出]|`e2e_sm_check_state_type state_ptr` 指向通信状态的指针，用于记录检查状态 |
|返回值|E2E_E_INTERR 函数运行异常|
|返回值|E2E_E_INPUTERR_NULL 指针参数为空|
|返回值|E2E_E_INPUTERR_WRONG 参数错误|
|返回值|E2E_E_OK 检查成功|
|同步/异步|同步|
|可重入性|不可重入|