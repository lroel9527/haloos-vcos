# dcm 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `dcm_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DCM_CODE) dcm_init(const dcm_config_type *config_ptr)`|
|简要描述|dcm初始化|
|详细说明|dcm初始化|
|参数[输入]|`config_ptr` 配置指针|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dcm_de_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DCM_CODE) dcm_de_init(uint8 value)`|
|简要描述|dcm去初始化|
|详细说明|dcm去初始化|
|参数[输入]|`value` 去初始化值|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dcm_start_of_reception`

|属性|描述|
|---|---|
|函数定义|`FUNC(BufReq_ReturnType, DCM_CODE) dcm_start_of_reception(PduIdType dcm_rx_pdu_id, const PduInfoType *info, PduLengthType tp_sdu_length, PduLengthType *rx_buffer_size_ptr)`|
|简要描述|dcm开始接收数据|
|详细说明|dcm开始接收数据|
|参数[输入]|`dcm_rx_pdu_id` 配置接收的pdu id|
|参数[输入]|`info` pdu信息结构体指针|
|参数[输入]|`tp_sdu_length` 数据长度|
|参数[输入]|`rx_buffer_size_ptr` 接收数据区buffer长度指针|
|返回值|开始接收数据结果|
|同步/异步|同步|
|可重入性|可重入|

## `dcm_copy_rx_data`

|属性|描述|
|---|---|
|函数定义|`FUNC(BufReq_ReturnType, DCM_CODE) dcm_copy_rx_data(PduIdType dcm_rx_pdu_id, const PduInfoType *pdu_info_ptr, PduLengthType *rx_buffer_size_ptr)`|
|简要描述|dcm拷贝接收数据|
|详细说明|dcm拷贝接收数据|
|参数[输入]|`dcm_rx_pdu_id` 配置接收的pdu id|
|参数[输入]|`pdu_info_ptr` pdu数据源|
|参数[输出]|`rx_buffer_size_ptr` 接收数据区buffer长度指针|
|返回值|拷贝接收数据结果|
|同步/异步|同步|
|可重入性|可重入|

## `dcm_tp_rx_indication`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DCM_CODE) dcm_tp_rx_indication(PduIdType dcm_rx_pdu_id, NotifResultType result)`|
|简要描述|dcm接收数据完成|
|详细说明|dcm接收数据完成|
|参数[输入]|`dcm_rx_pdu_id` 配置接收的pdu id|
|参数[输入]|`result` 接收结果|
|返回值|void|
|同步/异步|同步|
|可重入性|可重入|

## `dcm_copy_tx_data`

|属性|描述|
|---|---|
|函数定义|`FUNC(BufReq_ReturnType, DCM_CODE) dcm_copy_tx_data(PduIdType dcm_tx_pdu_id, const PduInfoType *pdu_info_ptr, const RetryInfoType *retry, PduLengthType *tx_data_cnt_ptr)`|
|简要描述|dcm拷贝发送数据|
|详细说明|dcm拷贝发送数据|
|参数[输入]|`dcm_tx_pdu_id` 配置发送的pdu id|
|参数[输入]|`pdu_info_ptr` pdu数据源|
|参数[输入]|`retry` 重试次数|
|参数[输出]|`tx_data_cnt_ptr` 发送数据计数|
|返回值|拷贝发送数据结果|
|同步/异步|同步|
|可重入性|可重入|

## `dcm_tp_tx_confirmation`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DCM_CODE) dcm_tp_tx_confirmation(PduIdType dcm_tx_pdu_id, NotifResultType result)`|
|简要描述|dcm发送数据确认|
|详细说明|dcm发送数据确认|
|参数[输入]|`dcm_tx_pdu_id` 配置发送的pdu id|
|参数[输入]|`result` 发送结果|
|返回值|void|
|同步/异步|同步|
|可重入性|可重入|
