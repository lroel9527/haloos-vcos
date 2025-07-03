# dem 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `dem_master_pre_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_master_pre_init(const dem_config_type *config_ptr)`|
|简要描述|dem master预初始化|
|详细说明|dem master预初始化|
|参数[输入]|`config_ptr` dem配置指针config_ptr|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_satellite_pre_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_satellite_pre_init(dem_satellite_id_type satellite_id)`|
|简要描述|dem satellite预初始化|
|详细说明|dem satellite预初始化|
|参数[输入]|`satellite_id` satellite的id|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_pre_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_pre_init(const dem_config_type *config_ptr)`|
|简要描述|dem预初始化|
|详细说明|dem预初始化，单核场景使用|
|参数[输入]|`config_ptr` dem配置指针config_ptr|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_master_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_master_init(const dem_config_type *config_ptr)`|
|简要描述|dem master初始化|
|详细说明|dem master初始化|
|参数[输入]|`config_ptr` dem配置指针config_ptr|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_satellite_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_satellite_init(dem_satellite_id_type satellite_id)`|
|简要描述|dem satellite初始化|
|详细说明|dem satellite初始化|
|参数[输入]|`satellite_id` satellite的id|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_init`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_init(const dem_config_type *config_ptr)`|
|简要描述|dem初始化|
|详细说明|dem初始化，单核场景使用|
|参数[输入]|`config_ptr` dem配置指针config_ptr|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_shutdown`

|属性|描述|
|---|---|
|函数定义|`FUNC(void, DEM_CODE) dem_shutdown(void)`|
|简要描述|dem关闭|
|详细说明|dem关闭|
|参数[输入]|void|
|返回值|void|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_indicator_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_indicator_status(uint8 indicator_id, dem_indicator_status_type *indicator_status)`|
|简要描述|dem获取指示器状态|
|详细说明|dem获取指示器状态|
|参数[输入]|`indicator_id` 指示器id|
|参数[输出]|`indicator_status` 指示器状态|
|返回值|E_OK 获取指示器状态成功|
|返回值|E_NOT_OK 获取指示器状态失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_event_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_event_status(dem_event_id_type event_id, dem_event_status_type event_status)`|
|简要描述|dem设置事件状态|
|详细说明|dem设置事件状态|
|参数[输入]|`event_id` 事件id|
|参数[输出]|`event_status` 事件状态|
|返回值|E_OK 设置事件状态状态成功|
|返回值|E_NOT_OK 设置事件状态状态失败|
|同步/异步|异步|
|可重入性|相同event_id不可重入，不同event_id可重入|

## `dem_reset_event_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_reset_event_status(dem_event_id_type event_id)`|
|简要描述|dem重置事件状态|
|详细说明|dem重置事件状态|
|参数[输入]|`event_id` 事件id|
|返回值|E_OK 设置事件状态状态成功|
|返回值|E_NOT_OK 设置事件状态状态失败|
|同步/异步|异步|
|可重入性|相同event_id不可重入，不同event_id可重入|

## `dem_get_event_uds_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_event_uds_status(dem_event_id_type event_id, dem_uds_status_byte_type *uds_status_byte)`|
|简要描述|dem获取事件UDS状态|
|详细说明|dem获取事件UDS状态|
|参数[输入]|`event_id` 事件id|
|参数[输入]|`uds_status_byte` UDS状态|
|返回值|E_OK 获取事件UDS状态成功|
|返回值|E_NOT_OK 获取事件UDS状态失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_fdc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_fdc(dem_event_id_type event_id, sint8 *fault_detection_counter)`|
|简要描述|dem获取事件故障检测计数器|
|详细说明|dem获取事件故障检测计数器|
|参数[输入]|`event_id` 事件id|
|参数[输入]|`fault_detection_counter` 故障检测计数器|
|返回值|E_OK 获取事件故障检测计数器成功|
|返回值|E_NOT_OK 获取事件故障检测计数器失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_opcycle_state`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_opcycle_state(dem_opcycle_id_type opcycle_id, dem_opcycle_state_type cycle_state)`|
|简要描述|dem设置操作周期状态|
|详细说明|dem设置操作周期状态|
|参数[输入]|`opcycle_id` 操作周期id|
|参数[输入]|`cycle_state` 操作周期状态|
|返回值|E_OK 设置操作周期状态成功|
|返回值|E_NOT_OK 设置操作周期状态失败|
|同步/异步|异步|
|可重入性|不可重入|

## `dem_restart_opcycle`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_restart_opcycle(uint8 opcycle_id)`|
|简要描述|dem重启操作周期|
|详细说明|dem重启操作周期|
|参数[输入]|`opcycle_id` 操作周期id|
|返回值|E_OK 重启操作周期成功|
|返回值|E_NOT_OK 重启操作周期失败|
|同步/异步|异步|
|可重入性|不可重入|

## `dem_get_dtc_of_event`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_dtc_of_event(dem_event_id_type event_id, dem_dtc_format_type dtc_format, uint32 *dtc_of_event)`|
|简要描述|dem获取事件的dtc|
|详细说明|dem获取事件的dtc|
|参数[输入]|`event_id` 事件id|
|参数[输入]|`dtc_format` dtc格式|
|参数[输出]|`dtc_of_event` 事件dtc|
|返回值|E_OK 获取事件的dtc成功|
|返回值|E_NOT_OK 获取事件的dtc失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_dtc_status_availability_mask`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_dtc_status_availability_mask(uint8 client_id, uint8 *dtc_status_mask)`|
|简要描述|dem获取dtc状态可用掩码|
|详细说明|dem获取dtc状态可用掩码|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`dtc_status_mask` dtc状态可用掩码|
|返回值|E_OK 获取dtc状态可用掩码成功|
|返回值|E_NOT_OK 获取dtc状态可用掩码失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_dtc_filter`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_dtc_filter(uint8 client_id, uint8 dtc_status_mask, dem_dtc_format_type dtc_format, dem_dtc_origin_type dtc_origin, boolean filter_with_severity, dem_dtc_severity_type dtc_severity_mask, boolean filter_for_fault_detection_counter)`|
|简要描述|dem设置dtc过滤器|
|详细说明|dem设置dtc过滤器|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`dtc_status_mask` dtc状态掩码|
|参数[输入]|`dtc_format` dtc格式|
|参数[输入]|`dtc_origin` dtc来源|
|参数[输入]|`filter_with_severity` 是否使用严重性过滤|
|参数[输入]|`dtc_severity_mask` 严重性掩码|
|参数[输入]|`filter_for_fault_detection_counter` 是否过滤故障检测计数器|
|返回值|E_OK 设置dtc过滤器成功|
|返回值|E_NOT_OK 设置dtc过滤器失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_status_of_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_status_of_dtc(uint8 client_id, dem_event_status_rec_type *dtc_status)`|
|简要描述|dem获取dtc状态|
|详细说明|dem获取dtc状态|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`dtc_status` dtc状态|
|返回值|E_OK 获取dtc状态成功|
|返回值|E_NOT_OK 获取dtc状态失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_number_of_filtered_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_number_of_filtered_dtc(uint8 client_id, uint16 *number_of_filtered_dtc)`|
|简要描述|dem获取符合过滤器的dtc数量|
|详细说明|dem获取符合过滤器的dtc数量|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`number_of_filtered_dtc` dtc数量|
|返回值|E_OK 获取符合过滤器的dtc数量成功|
|返回值|E_NOT_OK 获取符合过滤器的dtc数量失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_next_filtered_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE)dem_get_next_filtered_dtc(uint8 client_id, uint32 *dtc, dem_event_status_rec_type *dtc_status)`|
|简要描述|dem获取下一个符合过滤器的dtc|
|详细说明|dem获取下一个符合过滤器的dtc|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`dtc` dtc|
|参数[输出]|`dtc_status` dtc状态|
|返回值|E_OK 获取下一个符合过滤器的dtc成功|
|返回值|E_NOT_OK 获取下一个符合过滤器的dtc失败|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_translation_type`

|属性|描述|
|---|---|
|函数定义|`FUNC(dem_dtc_translation_format_type, DEM_CODE) dem_get_translation_type(uint8 client_id)`|
|简要描述|dem获取dtc转换格式类型|
|详细说明|dem获取dtc转换格式类型|
|参数[输入]|`client_id` 客户端id|
|返回值|dtc转换格式类型|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_clear_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_clear_dtc(uint8 client_id)`|
|简要描述|dem清除dtc|
|详细说明|dem清除dtc|
|参数[输入]|`client_id` 客户端id|
|返回值|清除dtc成功与否结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_disable_dtc_setting`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_disable_dtc_setting(uint8 client_id)`|
|简要描述|dem关闭dtc设置|
|详细说明|dem关闭dtc设置|
|参数[输入]|`client_id` 客户端id|
|返回值|关闭dtc设置结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_enable_dtc_setting`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_enable_dtc_setting(uint8 client_id)`|
|简要描述|dem开启dtc设置|
|详细说明|dem开启dtc设置|
|参数[输入]|`client_id` 客户端id|
|返回值|开启dtc设置结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_ext_data_record_by_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(dem_return_get_ext_data_record_by_dtc_type, DEM_CODE) dem_get_ext_data_record_by_dtc(uint32 dtc, dem_dtc_origin_type dtc_origin, uint8 ext_data_number, uint8 *dest_buffer, uint16 *buf_size)`|
|简要描述|dem获取扩展dtc数据|
|详细说明|dem获取扩展dtc数据|
|参数[输入]|`dtc` dtc|
|参数[输入]|`dtc_origin` dtc来源|
|参数[输入]|`ext_data_number` 扩展数据号|
|参数[输入]|`dest_buffer` 返回buffer地址|
|参数[输入]|`buf_size` buffer长度|
|返回值|获取扩展dtc数据结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_ff_data_by_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(dem_return_get_ff_data_by_dtc_type, DEM_CODE) dem_get_ff_data_by_dtc(uint32 dtc, dem_dtc_origin_type dtc_origin, uint8 recnum, uint8 *dest_buffer, uint16 *buf_size)`|
|简要描述|dem获取dtc冻结帧|
|详细说明|dem获取dtc冻结帧|
|参数[输入]|`dtc` dtc|
|参数[输入]|`dtc_origin` dtc来源|
|参数[输入]|`recnum` 记录号|
|参数[输入]|`dest_buffer` 返回buffer地址|
|参数[输入]|`buf_size` buffer长度|
|返回值|获取dtc冻结帧结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_ff_record_filter`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_ff_record_filter(uint8 client_id, dem_dtc_format_type dtc_format)`|
|简要描述|dem设置冻结帧记录过滤器|
|详细说明|dem设置冻结帧记录过滤器|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`dtc_format` dtc格式|
|返回值|设置冻结帧记录过滤器结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_number_of_ff_records`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_number_of_ff_records(uint8 client_id, uint16 *number_of_filtered_records)`|
|简要描述|dem获取冻结帧记录数量|
|详细说明|dem获取冻结帧记录数量|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`number_of_filtered_records` 冻结帧记录数量|
|返回值|获取冻结帧记录数量结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_next_filtered_record`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_next_filtered_record(uint8 client_id, uint32 *dtc, uint8 *recnum)`|
|简要描述|dem获取下一个符合过滤器的记录|
|详细说明|dem获取下一个符合过滤器的记录|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`dtc` dtc|
|参数[输出]|`recnum` 记录数|
|返回值|获取下一个符合过滤器的记录结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_enable_condition`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_enable_condition(uint8 condition_id, boolean condition_fulfilled)`|
|简要描述|dem设置使能条件|
|详细说明|dem设置使能条件|
|参数[输入]|`condition_id` 条件id|
|参数[输入]|`condition_fulfilled` 使能条件满足与否|
|返回值|设置使能条件结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_storage_condition`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_storage_condition(uint8 condition_id, boolean condition_fulfilled)`|
|简要描述|dem设置存储条件|
|详细说明|dem设置存储条件|
|参数[输入]|`condition_id` 条件id|
|参数[输入]|`condition_fulfilled` 存储条件满足与否|
|返回值|设置存储条件结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_event_memory_overflow`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_event_memory_overflow(uint8 client_id, dem_dtc_origin_type dtc_origin, boolean *overflow_indication)`|
|简要描述|dem获取事件存储溢出状态|
|详细说明|dem获取事件存储溢出状态|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`dtc_origin` dtc来源|
|参数[输出]|`overflow_indication` 溢出状态|
|返回值|获取事件存储溢出状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_dtc_suppression`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_dtc_suppression(uint8 client_id, boolean suppression_status)`|
|简要描述|dem设置dtc抑制状态|
|详细说明|dem设置dtc抑制状态|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`suppression_status` 抑制状态|
|返回值|设置dtc抑制状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_dtc_suppression`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_dtc_suppression(uint8 client_id, boolean *suppression_status)`|
|简要描述|dem获取dtc抑制状态|
|详细说明|dem获取dtc抑制状态|
|参数[输入]|`client_id` 客户端id|
|参数[输出]|`suppression_status` 抑制状态|
|返回值|获取dtc抑制状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_set_event_available`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_set_event_available(dem_event_id_type event_id, boolean available_status)`|
|简要描述|dem设置事件可用状态|
|详细说明|dem设置事件可用状态|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`available_status` 可用状态|
|返回值|设置事件可用状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_monitor_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_monitor_status(dem_event_id_type event_id, dem_monitor_status_type *monitor_status)`|
|简要描述|dem获取事件监控状态|
|详细说明|dem获取事件监控状态|
|参数[输入]|`event_id` 事件id|
|参数[输出]|`monitor_status` 监控状态|
|返回值|获取事件监控状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_opcycle_state`

|属性|描述|
|---|---|
|函数定义|`FUNC(dem_opcycle_state_type, DEM_CODE) dem_get_opcycle_state(uint8 opcycle_id)`|
|简要描述|dem获取操作周期状态|
|详细说明|dem获取操作周期状态|
|参数[输入]|`opcycle_id` 操作周期id|
|返回值|操作周期状态|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_reset_event_debounce_status`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_reset_event_debounce_status(dem_event_id_type event_id, dem_debounce_reset_status_type debounce_reset_status)`|
|简要描述|dem重置事件去抖状态|
|详细说明|dem重置事件去抖状态|
|参数[输入]|`event_id` 事件id|
|参数[输入]|`debounce_reset_status` 去抖状态|
|返回值|重置事件去抖状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_select_dtc`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_select_dtc(uint8 client_id, uint32 dtc, dem_dtc_format_type dtc_format, dem_dtc_origin_type dtc_origin)`|
|简要描述|dem选择dtc|
|详细说明|dem选择dtc|
|参数[输入]|`client_id` 客户端id|
|参数[输入]|`dtc` dtc|
|参数[输入]|`dtc_format` dtc格式|
|参数[输入]|`dtc_origin` dtc来源|
|返回值|选择dtc结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_get_debouncing_of_event`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_get_debouncing_of_event(dem_event_id_type event_id, dem_debouncing_state_type *debouncing_state)`|
|简要描述|dem获取事件去抖状态|
|详细说明|dem获取事件去抖状态|
|参数[输入]|`event_id` 事件id|
|参数[输出]|`debouncing_state` 去抖状态|
|返回值|获取事件去抖状态结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_prestore_ff`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_prestore_ff(dem_event_id_type event_id)`|
|简要描述|dem预存储冻结帧|
|详细说明|dem预存储冻结帧|
|参数[输入]|`event_id` 事件id|
|返回值|预存储冻结帧结果|
|同步/异步|同步|
|可重入性|不可重入|

## `dem_clear_prestored_ff`

|属性|描述|
|---|---|
|函数定义|`FUNC(std_return_type, DEM_CODE) dem_clear_prestored_ff(dem_event_id_type event_id)`|
|简要描述|dem清除预存储冻结帧|
|详细说明|dem清除预存储冻结帧|
|参数[输入]|`event_id` 事件id|
|返回值|清除预存储冻结帧结果|
|同步/异步|同步|
|可重入性|不可重入|
