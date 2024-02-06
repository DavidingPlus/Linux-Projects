# Database_System

老白课程的期末实战项目，自己准备实现一份，用`cmake`工具进行编写构建.

- 自己将整个架构设计成为了`CS`架构的客户端-服务端，已经做完了，在处理表命令的时候是硬解析的，没有用更好的正则表达式或者其他办法来解析，因为我不会正则表达式；所以处理表的部分现在是正确的命令可用(但是还是要在条件之内)，处理了一部分不正确的命令。（可以，成功写成了一坨屎山。。。）索引目前没有考虑，我不想做了，就这样吧...

- 项目要求目录中就是本项目的要求和一些提交模板.

- 其余部分就是`cmake`构建的整体项目架构:

    - `include/`：头文件的存放位置

    - `res/`:一些资源文件的存放位置

    - `src/`:源文件的存放位置，其实我不想把这坨屎山暴露出来，这也是为什么我把头文件和源文件分离了，这样我可以打一个静态库来屏蔽我的源文件代码，当然我把这个静态库打包放在`res/`中了

    - `test/`：主程序文件，客户端`client.cpp`和服务端`server.cpp`

- 在`CMakeLists.txt`中添加了一些额外的东西：

    - 设置`C++`标准，整个项目的`C++`标准我用的是`C++20`(但是我还没来得及使用`format`库...)

      ```cmake
      set(CMAKE_CXX_STANDARD 20)
      ```

    - 添加内存消毒器，为了规范我们的代码

      ```cmake
      set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
      ```

    - 设置`CMake_Build_Type`

      ```cmake
      set(CMAKE_BUILD_TYPE Debug)
      ```

- 新建了一个`make/`目录，用来存放`Makefile`，我们不能把`Makefile`放在根目录，因为项目的构建需要在根目录的一级目录下面，包括代码中的各种路径都是这么定义的，这也是为什么我们这么强调代码的架构以及`CMake`要默认选择在`build`目录编译的原因。这个`Makefile`编译找的是`include/`的头文件和`res/`中封装好的静态库，静态库可能不会实时更新，可能哪天我想起了就会更新，我只是试一下用`Makefile`构建一下，当然用全自动的`CMake`构建是最好的。

- 后续会做一些演示和测试工作，这个到时候再说，应该会在项目的`test`目录中放一些测试的`sql`语句，包括正确的和错误的，当然不可能保证命令百分百全覆盖，只能说我想的范围内的命令都基本覆盖了，当然用户一般也不会脑洞那么大去尝试一些奇怪的操作...

