# time_tsync 接口参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `cantsyn_init`

|属性|描述|
|---|---|
|函数定义|`void cantsyn_init(const cantsyn_config_type *config_ptr)`|
|简要描述|初始化函数 |
|详细说明|cantsyn初始化函数|
|参数[输入]|`const cantsyn_config_type *config_ptr` config_ptr 配置指针 |
|同步/异步|同步|
|可重入性|不可重入|
