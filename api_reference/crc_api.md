# crc 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `crc_calculate_8`

|属性|描述|
|---|---|
|函数定义|`uint8 crc_calculate_8(const uint8 *data_ptr, uint32 len, uint8 start_val, boolean is_first_call)`|
|简要描述|CRC8计算 |
|详细说明|针对 8-bit SAE J1850标准的CRC8计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint8 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_8_h2f`

|属性|描述|
|---|---|
|函数定义|`uint8 crc_calculate_8_h2f(const uint8 *data_ptr, uint32 len, uint8 start_val, boolean is_first_call)`|
|简要描述|CRC8H2F计算 |
|详细说明|针对 8-bit 0x2F J1850标准的CRC8计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint8 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_16`

|属性|描述|
|---|---|
|函数定义|`uint16 crc_calculate_16(const uint8 *data_ptr, uint32 len, uint16 start_val, boolean is_first_call)`|
|简要描述|CRC16计算 |
|详细说明|针对 16-bit CCITT-FALSE J1850标准的CRC8计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint16 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_16_arc`

|属性|描述|
|---|---|
|函数定义|`uint16 crc_calculate_16_arc(const uint8 *data_ptr, uint32 len, uint16 start_val, boolean is_first_call)`|
|简要描述|CRC16ARC计算 |
|详细说明|针对 16-bit ARC J1850标准的CRC8计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint16 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_32`

|属性|描述|
|---|---|
|函数定义|`uint32 crc_calculate_32(const uint8 *data_ptr, uint32 len, uint32 start_val, boolean is_first_call)`|
|简要描述|CRC32计算 |
|详细说明|针对 32-bit Ethernet标准的CRC32计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint32 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_32_p4`

|属性|描述|
|---|---|
|函数定义|`uint32 crc_calculate_32_p4(const uint8 *data_ptr, uint32 len, uint32 start_val, boolean is_first_call)`|
|简要描述|CRC32P4计算 |
|详细说明|针对 32-bit 0xF4ACFB13标准的CRC32计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint32 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|

## `crc_calculate_64`

|属性|描述|
|---|---|
|函数定义|`uint32 crc_calculate_64(const uint8 *data_ptr, uint32 len, uint64 start_val, boolean is_first_call)`|
|简要描述|CRC32P4计算 |
|详细说明|针对 32-bit 0xF4ACFB13标准的CRC32计算 |
|参数[输入]|`uint8 data_ptr` 指向输入数据的指针 |
|参数[输入]|`uint32 len` 输入数据的长度 |
|参数[输入]|`uint64 start_val` 该标准下的初始值 |
|参数[输入]|`boolean is_first_call` 是否首次计算crc |
|返回值|返回crc计算结果|
|同步/异步|同步|
|可重入性|可重入|
