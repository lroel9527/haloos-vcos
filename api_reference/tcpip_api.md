# TcpIp API参考文档

> 提示：本API参考文档仅代表功能栈的接口描述和功能说明，帮助开发者快速了解接口作用。应用开发者应通过服务映射调用对应的RTE接口，而非直接调用本文接口

## `bsw_tcpip_init`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `void bsw_tcpip_init(const tcpip_config_type *config_ptr)`        |
| 简要描述      | 初始化TcpIp             |
| 详细说明      | 获取TcpIp的配置信息,初始化TcpIp相关结构体    |
| 参数[输入] | `const tcpip_config_type * config_ptr` TcpIp配置信息结构体指针  |
| 同步/异步     | 同步 |
| 可重入性     | 不可重入 |


## `tcpip_close`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_close(tcpip_socket_id_type socket_id, boolean abort)`        |
| 简要描述      | 关闭一个已有的TcpIp套接字             |
| 详细说明      | 协议栈关闭套接字并释放套接字资源    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `boolean abort` 是否通过发送RST报文强制关闭套接字  |
| 返回值 | Std_ReturnType E_OK 关闭套接字成功 |
| 返回值 | Std_ReturnType E_NOT_OK 关闭套接字失败,可能的原因是套接字不存在或者套接字已经被关闭 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_bind`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_bind(tcpip_socket_id_type socket_id, tcpip_local_addr_id_type local_addr_id, const uint16 *port_ptr)`        |
| 简要描述      | 绑定一个TcpIp套接字             |
| 详细说明      | 协议栈绑定一个TcpIp套接字,并申请套接字资源    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `tcpip_local_addr_id_type local_addr_id` 本地地址索引  |
| 参数[输入] | `const uint16 * port_ptr` 端口号指针  |
| 返回值 | Std_ReturnType E_OK 绑定套接字成功 |
| 返回值 | Std_ReturnType E_NOT_OK 绑定套接字失败,可能的原因是套接字不存在或者套接字已经被绑定 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_tcp_connect`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_tcp_connect(tcpip_socket_id_type socket_id, const tcpip_sock_addr_type *remote_addr_ptr)`        |
| 简要描述      | 连接一个远程TCP服务器             |
| 详细说明      | 协议栈通过一个已有套接字连接远程的TCP服务器    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `const tcpip_sock_addr_type * remote_addr_ptr` 远程地址指针  |
| 返回值 | Std_ReturnType E_OK 连接成功 |
| 返回值 | Std_ReturnType E_NOT_OK 连接失败,可能的原因是套接字不存在或者套接字已经被连接 |
| 同步/异步     | 异步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_tcp_listen`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_tcp_listen(tcpip_socket_id_type socket_id, uint16 max_channels)`        |
| 简要描述      | 监听一个TCP套接字             |
| 详细说明      | 协议栈监听一个TCP套接字,等待TCP客户端连接    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `uint16 max_channels` 最大连接数  |
| 返回值 | Std_ReturnType E_OK 监听成功 |
| 返回值 | Std_ReturnType E_NOT_OK 监听失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_tcp_received`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_tcp_received(tcpip_socket_id_type socket_id, uint32 length)`        |
| 简要描述      | 通知协议栈数据已经收到             |
| 详细说明      | 上层应用通知协议栈数据已经收到,协议栈将根据套接字类型进行相应的处理    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `uint32 length` 数据长度  |
| 返回值 | Std_ReturnType E_OK 协议栈通知成功 |
| 返回值 | Std_ReturnType E_NOT_OK 协议栈通知失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_change_parameter`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_change_parameter(tcpip_socket_id_type socket_id, tcpip_param_id_type parameter_id, const uint8 *parameter_value)`        |
| 简要描述      | 修改套接字参数             |
| 详细说明      | 修改一个已有协议栈套接字的属性    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字的索引  |
| 参数[输入] | `tcpip_param_id_type parameter_id` 参数类型的索引  |
| 参数[输入] | `const uint8 * parameter_value` 参数的值指针  |
| 返回值 | Std_ReturnType E_OK 修改参数成功 |
| 返回值 | Std_ReturnType E_NOT_OK 修改参数失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_get_ip_addr`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_get_ip_addr(tcpip_local_addr_id_type local_addr_id, tcpip_sock_addr_type *ip_addr_ptr, uint8 *netmask_ptr, tcpip_sock_addr_type *default_router_ptr)`        |
| 简要描述      | 获取IP地址             |
| 详细说明      | 获取本地的IP地址,掩码,默认路由信息    |
| 参数[输入] | `tcpip_local_addr_id_type local_addr_id` 本地地址索引  |
| 参数[输出] | `tcpip_sock_addr_type * ip_addr_ptr` 获取的IP地址指针  |
| 参数[输出] | `uint8 * netmask_ptr` 获取的掩码指针  |
| 参数[输出] | `tcpip_sock_addr_type * default_router_ptr` 获取的默认路由指针  |
| 返回值 | Std_ReturnType E_OK 获取IP地址成功 |
| 返回值 | Std_ReturnType E_NOT_OK 获取IP地址失败 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |


## `tcpip_get_phys_addr`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_get_phys_addr(tcpip_local_addr_id_type local_addr_id, uint8 *phys_addr_ptr)`        |
| 简要描述      | 获取MAC地址             |
| 详细说明      | 获取本地的MAC地址    |
| 参数[输入] | `tcpip_local_addr_id_type local_addr_id` 本地地址索引  |
| 参数[输出] | `uint8 * phys_addr_ptr` 获取的MAC地址指针  |
| 返回值 | Std_ReturnType E_OK 获取MAC地址成功 |
| 返回值 | Std_ReturnType E_NOT_OK 获取MAC地址失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不可重入 |


## `tcpip_get_ctrl_idx`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_get_ctrl_idx(tcpip_local_addr_id_type local_addr_id, uint8 *ctrl_idx_ptr)`        |
| 简要描述      | 获取控制器索引             |
| 详细说明      | 获取某个IP地址索引对应的控制器索引    |
| 参数[输入] | `tcpip_local_addr_id_type local_addr_id` 本地地址索引  |
| 参数[输出] | `uint8 * ctrl_idx_ptr` 获取的控制器索引指针  |
| 返回值 | Std_ReturnType E_OK 获取控制器索引成功 |
| 返回值 | Std_ReturnType E_NOT_OK 获取控制器索引失败 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |


## `tcpip_udp_transmit`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_udp_transmit(tcpip_socket_id_type socket_id, const uint8 *data_ptr, const tcpip_sock_addr_type *remote_addr_ptr, uint16 total_length)`        |
| 简要描述      | 发送一帧UDP报文             |
| 详细说明      | 协议栈往指定的远端地址发送一帧UDP报文    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字ID  |
| 参数[输入] | `const uint8 * data_ptr` 待发送的数据指针  |
| 参数[输入] | `const tcpip_sock_addr_type * remote_addr_ptr` 远端地址指针  |
| 参数[输入] | `uint16 total_length` 待发送的数据长度  |
| 返回值 | Std_ReturnType E_OK UDP报文发送成功 |
| 返回值 | Std_ReturnType E_NOT_OK UDP报文发送失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_udp_gen_packet`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_udp_gen_packet(const tcpip_sock_addr_type *src_addr_ptr, const tcpip_sock_addr_type *dst_addr_ptr, uint16 vlan_id, eth_data_type *buf_ptr, const uint8 *data_ptr, uint16 *data_len)`        |
| 简要描述      | 组一帧UDP报文             |
| 详细说明      | 组一帧UDP报文，可绕过协议栈通过驱动接口直接发送    |
| 参数[输入] | `const tcpip_sock_addr_type * src_addr_ptr` 源地址信息，包含IP地址和端口  |
| 参数[输入] | `const tcpip_sock_addr_type * dst_addr_ptr` 目的地址信息，包含IP地址和端口  |
| 参数[输入] | `uint16 vlan_id` VLAN ID  |
| 参数[输入] | `eth_data_type * buf_ptr` 报文数据缓冲区指针  |
| 参数[输入] | `const uint8 * data_ptr` UDP报文数据指针  |
| 参数[输入] | `uint16 * data_len` UDP报文数据长度指针  |
| 返回值 | Std_ReturnType E_OK UDP组包成功 |
| 返回值 | Std_ReturnType E_NOT_OK UDP组包失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不可重入 |


## `tcpip_tcp_transmit`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_tcp_transmit(tcpip_socket_id_type socket_id, const uint8 *data_ptr, uint32 available_length, boolean force_retrieve)`        |
| 简要描述      | 发送一帧TCP报文             |
| 详细说明      | 协议栈通过套接字往已经建立连接的远端地址发送一帧TCP报文    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字ID  |
| 参数[输入] | `const uint8 * data_ptr` 待发送的数据指针  |
| 参数[输入] | `uint32 available_length` 待发送的数据长度  |
| 参数[输入] | `boolean force_retrieve` 暂不生效  |
| 返回值 | Std_ReturnType E_OK TCP报文发送成功 |
| 返回值 | Std_ReturnType E_NOT_OK TCP报文发送失败 |
| 同步/异步     | 异步 |
| 可重入性     | 不同的套接字可重入,同一个套接字不可重入 |


## `tcpip_get_socket_state_of_socket_tcp`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `tcpip_socket_state_type tcpip_get_socket_state_of_socket_tcp(tcpip_socket_id_type socket_id)`        |
| 简要描述      | 获取TCP套接字的状态             |
| 详细说明      | 获取协议栈TCP套接字的状态    |
| 参数[输入] | `tcpip_socket_id_type socket_id` 套接字ID  |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_INVALID 无效套接字 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_LISTEN 套接字处于listen状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_SYNSENT 套接字处于SYN已发送状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_SYNRCVD 套接字处于SYN已收到状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_ESTABLISHED 套接字处于已建立连接状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_CLOSEWAIT 套接字处于FIN_WAIT1状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_LASTACK 套接字处于LAST_ACK状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_FINWAIT1 套接字处于FIN_WAIT1状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_FINWAIT2 套接字处于FIN_WAIT2状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_CLOSING 套接字处于关闭中状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_TIMEWAIT 套接字处于TIME_WAIT状态 |
| 返回值 | tcpip_socket_state_type TCPIP_TCP_SOCK_STATE_CLOSED 套接字处于关闭状态 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |


## `tcpip_request_com_mode`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_request_com_mode(uint8 ctrl_idx, tcpip_state_type state)`        |
| 简要描述      | 请求改变TCPIP的状态             |
| 详细说明      | 请求改变指定控制器的TCPIP状态    |
| 参数[输入] | `uint8 ctrl_idx` 控制器索引  |
| 参数[输入] | `tcpip_state_type state` 请求的状态  |
| 返回值 | Std_ReturnType E_OK 请求改变TCPIP状态成功 |
| 返回值 | Std_ReturnType E_NOT_OK 请求改变TCPIP状态失败 |
| 同步/异步     | 同步 |
| 可重入性     | 不可重入 |


## `tcpip_get_socket`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `Std_ReturnType tcpip_get_socket(uint8 socket_owner_id, tcpip_domain_type domain, tcpip_protocol_type protocol, tcpip_socket_id_type *socket_id_ptr)`        |
| 简要描述      | 申请一个新套接字             |
| 详细说明      | 上层模块通过协议栈申请套接字资源    |
| 参数[输入] | `uint8 socket_owner_id` 套接字所属者序号  |
| 参数[输入] | `tcpip_domain_type domain` IP地址族  |
| 参数[输入] | `tcpip_protocol_type protocol` 套接字协议  |
| 参数[输出] | `tcpip_socket_id_type * socket_id_ptr` 套接字序号  |
| 返回值 | Std_ReturnType E_OK 申请套接字成功 |
| 返回值 | Std_ReturnType E_NOT_OK 申请套接字失败 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |


## `tcpip_get_assignment_state_of_local_addr`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `tcpip_ip_addr_state_type tcpip_get_assignment_state_of_local_addr(uint8 addr_id)`        |
| 简要描述      | 获取IP地址分配状态             |
| 详细说明      | 获取协议栈指定IP地址的分配状态    |
| 参数[输入] | `uint8 addr_id` 地址索引  |
| 返回值 | tcpip_ip_addr_state_type E_OK 获取IP地址分配状态成功 |
| 返回值 | tcpip_ip_addr_state_type E_NOT_OK 获取IP地址分配状态失败 |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |


## `tcpip_get_state`

| 属性         | 描述                |
|--------------|---------------------|
| 函数定义      | `sint32 tcpip_get_state(NetworkHandleType network_handle)`        |
| 简要描述      | 获取协议栈状态             |
| 详细说明      | 获取协议栈状态，DDS使用    |
| 参数[输入] | `NetworkHandleType network_handle` 网络句柄  |
| 返回值 | sint32 0 协议栈ONLINE |
| 返回值 | sint32 1 协议栈OFFLINE |
| 同步/异步     | 同步 |
| 可重入性     | 可重入 |
