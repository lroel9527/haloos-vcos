# 工程编译

如果您仅需要编译VCOS相关代码，请按本文使用haloosspace/vcos/build/vcos_build.py指定工程进行编译，编译说明参考[VCOS工程编译说明](https://gitee.com/haloos/vcos_build/blob/master/README.md)；如果需要编译全量的HaloOS代码，请跳转至[HaloOS工程编译](https://gitee.com/haloos/docs/blob/master/quick_start/02_compiling.md)

## 1. 编译环境准备

### 1.1. 安装编译环境

> 安装编译环境前，需要先按照[配置工具安装](./02_installing.md)执行Studio依赖插件安装！

在`haloosspace`根目录，执行以下命令安装编译工具链：

```bash
python ./vcos/build/compiling_env.py
```

该命令依次执行以下安装步骤：

- 安装CMake工具，并将安装路径添加到PATH环境变量
- 安装kconfiglib工具
- 安装make工具，并设置`NINJA_TOOL_PATH`环境变量
- 安装ninja工具，并设置`NINJA_TOOL_PATH`环境变量
- 安装tricore-gcc编译工具链，并将安装路径添加到PATH环境变量
- 安装arm-gcc编译工具链，并将安装路径添加到PATH环境变量
- 安装docker工具

## 2. 编译

### 2.1. 一键编译

- 切换到`haloosspace/vcos/build`目录：

  ```bash
  cd ./vcos/build
  ```

- 编译memory_demo应用：配置使用A2G_TC397_5V_TFT板级配置，使用gcc编译器，使用ninja作为make工具，使用实际开发板运行

  ```bash
  python3 vcos_build.py -app_name memory_demo -board_name A2G_TC397_5V_TFT -compiler gcc -maketool ninja -sim 0 -all
  ```
  该命令会依次执行memory_demo应用对应的A2G_TC397_5V_TFT板子配置生成动态代码，cmake执行ninja编译脚本生成，并执行编译生成镜像。
  编译产物生成在`haloosspace/vcos/output/memory_demo_A2G_TC397_5V_TFT_gcc`目录下。

### 2.2. 编译命令说明
- 添加应用子目录，重新生成cmake：
  ```bash
  python3 vcos_build.py -app_name memory_demo -board_name A2G_TC397_5V_TFT -clean  # 清除编译产物
  python3 vcos_build.py -app_name memory_demo -board_name A2G_TC397_5V_TFT -gcmake  # 生成cmake
  python3 vcos_build.py -app_name memory_demo -board_name A2G_TC397_5V_TFT -fc  # 执行全量编译
  ```
- 修改应用代码后增量编译：
  ```bash
  python3 vcos_build.py -app_name memory_demo -board_name A2G_TC397_5V_TFT -ic
  ```
