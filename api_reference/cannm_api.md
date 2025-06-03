# cannm 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `cannm_init`

|属性|描述|
|---|---|
|函数定义|`cannm_init(const cannm_cate_cfg *const cannm_config)`|
|简要描述|Initialize the CanNm module. |
|详细说明|Set the local network flag in the control bit vector |
|参数[输入]|`未知类型 cannm_config` config ptr |
|同步/异步|Synchronous|
|可重入性|Non reentrant|

## `cannm_pas_stup`

|属性|描述|
|---|---|
|函数定义|`cannm_pas_stup(const network_handle_type nm_id)`|
|简要描述|CanNm passive start up. |
|详细说明|Package receiving process |
|参数[输入]|`未知类型 nm_id` channel id @ret_val E_OK Passive startup successfully @ret_val E_NOT_OK Passive startup failed |
|同步/异步|Synchronous|
|可重入性|Non reentrant|

## `cannm_rx_indication`

|属性|描述|
|---|---|
|函数定义|`cannm_rx_indication(PduIdType cannm_rx_pdu_id`|
|简要描述|Indication of a received PDU from a lower layer communication interface module. |
|详细说明|Indication of confirmation the transmission of a PDU |
|参数[输入]|`未知类型 pdu_info_ptr` Contains the length (SduLength) of the received PDU, a pointer to a buffer |
|同步/异步|Synchronous|
|可重入性|Reentrant for different PduIds. Non reentrant for the same PduId.|
