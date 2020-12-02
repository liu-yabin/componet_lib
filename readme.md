# componet_lib

演示了使用 cmake 创建一个带 componet 的库。为了简化起见，去除了无关的选项，如是否编译动态库、是否编译测试等常用选项和功能。这个库在编译安装以后会生成一个 `my_componet_lib` 的库，其中包括 `componet1` 和 `componet2` 两个组件。你可以使用 `find_package(my_componet_lib REQUIRED COMPONENTS componet2 componet1)` 来查找这个库。具体的使用示例可以参考 *use_my_componet_lib* 文件夹。
