# Crc 配置项参考文档

|容器属性|值（容器）|
|---|---|
|名称|Crc|
|描述|Configuration of the Crc (Crc routines) module.|
|多实例个数|1 - 1|

## 1. CrcGeneral

|容器属性|值（容器）|
|---|---|
|名称|CrcGeneral|
|描述|General configuration of CRC module|
|多实例个数|1 - 1|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc16ARCMode|
|描述|基于CRC 16-bit ARC (polynomial 8005)标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_16_ARC_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc16Mode|
|描述|基于CRC 16-bit (CCITT)标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_16_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc32Mode|
|描述|基于CRC 32-bit (IEEE-802.3 CRC32 Ethernet Standard)标准，选择table计算或者runtime计算模式 ||
|多实例个数|1 - 1|
|默认值|CRC_32_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc32P4Mode|
|描述|基于CRC 32-bit (E2E Profile 4)标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_32P4_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc64Mode|
|描述|基于CRC 64-bit标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_64_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc8H2FMode|
|描述|基于CRC 8-bit (2Fh polynomial)标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_8H2F_TABLE|

|配置项属性|值（枚举参数配置项）|
|---|---|
|名称|Crc8Mode|
|描述|基于 CRC 8-bit (SAE J1850)标准，选择table计算或者runtime计算模式 |
|多实例个数|1 - 1|
|默认值|CRC_8_TABLE|
