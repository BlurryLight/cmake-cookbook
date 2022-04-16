# 简短展示XXXConfig.Cmake的编写例子

首先需要编译hello_lib

```
cd hello_lib
mkdir build
cd build
cmake .. -GNinja -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=.... 
ninja && ninja install
```

把库安装到prefix在的目录后
编译hello_exe，在find_package的时候调整到config模式，并给定hints目录。
有许多方案。比如从环境变量读取。

