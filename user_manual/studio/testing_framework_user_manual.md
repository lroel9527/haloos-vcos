# 测试框架开发者手册

## 1.简介

VCOS自动化测试框架及代码仓库vcos_tests，包含了测试应用(examples)，测试框架(test_frameworks)和测试用例(testcases)。

测试应用(examples)中提供了可供测试的典型应用场景。

测试框架(test_frameworks)中集成了支撑测试运行的基础框架，包括vmtest, vctest和vptest, 支持离板测试和上板测试。

测试用例(testcases)中包含了C代码测试用例和python代码测试用例，支持mock测试, 单元测试，功能测试，集成测试等多个维度的测试类型。

## 2. 代码目录

测试框架及用例源代码在haloosspace/vcos/tests目录下, 目录结构如下图所示：

```plaintext
tests
├── CMakeLists.txt
├── examples                        # 测试应用目录
│   ├── CMakeLists.txt
│   └── tc397_rt_framework_tests    # 内核测试应用
├── README.md
├── testcases                       # 测试用例
│   ├── CMakeLists.txt
│   ├── commands                    # 测试命令行
│   ├── configs                     # 测试配置
│   ├── pytest                      # pytest测试用例
│   └── units                       # units测试用例
└── test_frameworks                 # 自动化测试框架
    ├── CMakeLists.txt
    └── unity                       # unity测试框架
```

## 3. 用例开发指导

### 约束

在开发测试用例之前，请确认已知悉如何开始vcos系统的开发和调试。参考：
[源码下载流程](../../quick_start/01_downloading.md)
[环境部署流程](../../quick_start/02_installing.md)
[工程编译流程](../../quick_start/03_compiling.md)
[物理开发板烧录运行流程](https://gitee.com/haloos/docs/blob/master/quick_start/03_%E9%83%A8%E7%BD%B2%E8%BF%90%E8%A1%8C%E6%B5%81%E7%A8%8B.md#1-%E5%9C%A8%E5%BC%80%E5%8F%91%E6%9D%BF%E4%B8%8A%E8%BF%90%E8%A1%8C)
[模拟器烧录运行流程](https://gitee.com/haloos/docs/blob/master/quick_start/03_%E9%83%A8%E7%BD%B2%E8%BF%90%E8%A1%8C%E6%B5%81%E7%A8%8B.md#2-%E5%9C%A8%E6%A8%A1%E6%8B%9F%E5%99%A8%E4%B8%8A%E8%BF%90%E8%A1%8C%E6%97%A0%E9%9C%80%E7%A1%AC%E4%BB%B6)

### 用例说明

| 用例范围 | 测试范围               | 测试含义                                                                   |
|-----| ----------------- |------------------------------------------------------------------------|
| Radius0   | 针对单个功能模块或组件的单元测试，验证最小代码单元的正确性。          | 基础测试，通过表示模块功能可运                                   |
| Radius1   | 测试多个功能模块的集成测试，验证组件间的交互逻辑，覆盖端到端流程         | 综合测试，通过表示整体功能基本可正常使用。                        |
| Radius2   | 模拟用户实际使用场景，验证系统在复杂交互下的功能或者性能表现。        | 复杂测试，用户复杂使用场景的各种正常、异常下的组合测试。          |
| Radius3   | 验证极端条件下的健壮性测试，如长时间运行、高负载、异常恢复等。         | 极端测试，用户难以触及的异常组合下的系统测试。          |

### tests/examples开发说明

应用开发请参考[examples仓库说明]()

### units用例说明

units测试用例基于vctest测试框架运行，以group->suite->testcase这样的层次结构进行注册管理。

| 层次结构 | 层次含义               |
|-----| ----------------- |
| group   | 测试组，同一个组件(component)对应的测试用例，应在同一个group中。          |
| suite   | 测试套，同一个功能模块(moduler)对应的测试用例，应该在同一个suite中。        |
| testcase   | 测试用例，对函数或功能模块级别进行测试。        |

#### 添加units测试用例

**添加测试group**
在register_group.c中，注册新增的测试group：

```c
void register_groups(void) {
    REGISTER_GROUP("group_kernel", register_group_kernel);
    REGISTER_GROUP("your_group_name", register_your_group); // 新增测试group
}
```

在units目录下，新增group对应目录以及对应文件：

```plaintext
units
├── kernel
├── your_group                  # 新增group对应目录
    ├── CMakeLists.txt          # CMakeLists文件
    ├── Kconfig                 # Kconfig配置文件
    ├── register_your_group.c   # group内的测试套注册管理文件
```

在Kconfig中，添加测试group的控制开关：

```kconfig
config UNIT_GROUP_YOUR_GROUP
 bool "unit group your group"
 default n
 ---help---
  Enable the UNIT_GROUP_YOUR_GROUP.
```

**添加测试suite**
完成新增测试group添加后，在register_your_group.c中，注册新增的测试suite：

```c
void register_your_group(char *group_name) {
    add_group_to_registry(group_name, group_setup, group_teardown);
    REGISTER_SUITE(group_name, "your_suite_name", register_your_suite); // 新增测试suite
}
```

在your_group目录下，新增suite对应目录以及对应文件：

```plaintext
units
├── your_group
    ├── your_suite
        ├── CMakeLists.txt
        ├── src
            ├── register_your_suite.c
        ├── inc
```

**添加测试testcase**
完成新增测试suite添加后，在register_your_suite.c中，注册新增的测试testcase：

```c
void register_your_suite(const char * group_name, const char * suite_name) {
    test_suite_s* this_suite = add_suite_to_group(group_name, suite_name, suite_setup, suite_teardown);
    REGISTER_TESTCASE(this_suite, "your_testcase_name", test_your_testcase, UNIT_CASE_R0); // 新增测试testcase
}
```

实现test_your_testcase函数：

```c
void test_your_testcase(void)
{
    /* 添加测试代码 */
    TEST_ASSERT_TRUE(...); // 测试断言
}
```

**断言函数**
所有断言函数均在unity.h中定义，常见断言列表如下:

| 断言类型 | 示例               |
|-----| ----------------- |
| 布尔条件   | TEST_ASSERT_TRUE(condition)          |
| 指针验证   | TEST_ASSERT_NULL(pointer)        |
| 值相等   | TEST_ASSERT_EQUAL_INT(expected, actual)        |
| 字符串相等   | TEST_ASSERT_EQUAL_STRING(expected, actual)        |

#### 运行units测试用例

将镜像烧录进开发板，并使用串口工具登录开发板。在串口中，通过ut命令运行units测试用例：

```shell
Usage: ut show [verbose]
       ut run [-g group_num] [-s suite_num] [-t testcase_num] [-R testcase_radius]
```

运行示例：

```shell
nsh> ut run -g 1 -s 2 -t 1
--- Running Tests ---

Group 1: group_kernel
    Suite 2: os_event_common
     Test: test_os_event_clearevent_001  ... PASSED

Summary
-----------------------
1 Tests 0 Failures 0 Ignored
```

### pytest用例说明

pytest测试用例中的基本结构如下所示：

```plaintext
tests
├── testcases/
    ├── pytest/
        ├── pytest.ini                       # pytest设置文件
        ├── conftest.py                      # 全局前后置文件
        ├── base/                            # 测试用例依赖的基础库
        ├── env/                             # 测试用例依赖的环境设置
        |   ├── environment.json5            # 环境设置
        |   ├── requirements.txt             # 依赖的python库
        ├── interaction/                     # 需要下位机的交互用例
        |   ├── basic_tests/                 # 基础测试
        |   ├── component1/                  # component目录
        |   |   ├── conftest.py              # component1前后置函数
        |   |   ├── moduler1/                # moduler1目录
        |   |   ├── moduler2/                # moduler2目录
        |   ├── component2/                  # component2目录
        ├── scripts/                         # 放置脚本，例如烧录脚本
        ├── studio/                          # 纯上位机用例，不依赖下位机交互
```

#### 添加pytest测试用例

在需要测试的模块底下，添加对应的pytest测试用例。pytest测试用例的基础模板如下所示：

```python
import pytest

from base.shell import shell

@pytest.mark.R0
class TestBasicFunctions:
    def test_hello(self):
        shell.write_shell("hello", clear_history=True)
        assert "Hello, World" in shell.read_shell(), "no reply from command 'hello'"
```

#### 运行pytest测试用例

**设置运行环境**

1. 进入tests/testcases/pytest/env目录下，安装运行pytest测试用例所需要的python库：

    ```shell
    python -m pip install requirements.txt
    ```

2. 修改修改environment.json5，进行对应的环境配置，例如配置开发板的串口号("SHELL":"PORT")：

```json5
{
    /* 当前的测试环境, HW: 硬件开发板, SIM: 模拟器 */
    "RUNNING_ENV": "HW",
    /* 测试的芯片架构 */
    "TARGET": "",
    /* 测试的demo工程 */
    "APPS_NAME": "tc397_demo",
    /* shell设置, PORT为串口设备名, BAUDRATE为波特率, PROMOT为shell提示符 */
    "SHELL": {
        "PORT": "COM6",
        "BAUDRATE": 115200,
        "PROMOT": "nsh> "
    }
}
```

**运行测试用例**
在tests/testcases/pytest目录下，通过pytest命令运行测试用例，例如：

```shell
pytest -m "your_marker" -k "your_keyword" 测试用例文件或路径
```

运行示例：

```shell
> pytest -m "R0" -k "test_hello" interaction/
============================================================================== test session starts ===============================================================================
interaction/basic_tests/test_startup.py::test_hello
--------------------------------------------------------------------------------- live log setup ---------------------------------------------------------------------------------
[INFO - 17:56:06] open shell successful: COM8 115200
[INFO - 17:56:06] Shell Input:

[INFO - 17:56:06] System is up!
--------------------------------------------------------------------------------- live log call ----------------------------------------------------------------------------------
[INFO - 17:56:06]
[INFO - 17:56:06] 开始测试
[INFO - 17:56:07] Shell Input: hello
PASSED                                                                                                                                                                      [100%]
======================================================================== 1 passed, 53 deselected in 7.44s ========================================================================
```
