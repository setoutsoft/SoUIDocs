# 2、SOUI 的编译

2.1 获取 SOUI 的源代码

SOUI 是开源软件,可以通过 git 客户端获取稳定版本：<https://github.com/setoutsoft/soui>

这里主要包含两个目录：
trunk 及 third-part。

trunk 目录保存 SOUI 项目的全部代码，
third-part 保存 soui 系统使用到的不方便放到 trunk 的第三方库，目前只有一个 WKE(一
个精简的 webkit)的源代码。一般情况下只获取 trunk 的代码就行。

2.2 编译 SOUI 界面库

SOUI 项目采用 QT 的 qmake 管理项目文件，qmake 已经从 QT 中分离出来，不需要你
的机器上安装 QT。（项目中也包含了网友提供的 cmake 编译脚本）
如果你在使用 vs2015，建议直接使用 build.bat 来编译 SOUI 库。

首先运行“vs2015 开发人员命令提示”，如果提示无法找到路径之类的提示，请用管理
员权限运行，这种情况大部分是在远程桌面编译 SOUI 库时出现。

使用“cd /d ”命令，把当前路径，切换至 SOUI 项目文件夹，运行 build.bat 批处理。

根据自己的需要配置编译选项；

配置完成后，会询问是打开 sln 文件、直接编译、或者退出批处理。

可以直接选择直接编译，省得还用 vs2015 打开 sln 文件进行编译。

不知道 vs2015 编译比较严格，还是什么原因，在编译过程中可能会出现很多的 waring。
等待编译完成后，会提示成功 35 个，这说明已经成功编译 SOUI 界面库了（如下图）：

==================附、作者微博提供的编译教程=================
如果你的机器上安装了 VS2008，可以直接打开 trunk 的根目录下的 soui.08.sln 来编译，
这个项目中各工程的编译依赖已经设置好，直接 F7 就可以全部完成编译。

如果你的机器安装的是其它版本（支持 vs2005-vs2015)，可以采用 trunk 目录下的
make(*).bat 来生成对应版本的项目文件，项目文件生成成功后会在根目录生成一个
soui.sln，打开该 sln 即可。VS2010+的版本需要先生成 VS2010 的项目文件，再用 VS
打开并升级。要生成 vs2005，可以手动修改 make(*).bat 中的参数。

如果安装的是 vs2008 或者 vs2010 还可以使用 buildAll_x86.bat 来生成项目文件并使用
命名行完成编译。
打开 make(dll-win32-vs08).bat 可以看到里面只有两行代码：

call "%VS90COMNTOOLS%..\..\VC\vcvarsall.bat" x86
tools\qmake -tp vc -r -spec .\tools\mkspecs\win32-msvc2008 "CONFIG +=
DLL_SOUI USING_MT CAN_DEBUG"

第一行通过 VS 的环境变量加载 VS 的 PATH 信息。

第二行调用 qmake 生成项目文件： -spec 后面的参数指定生成的项目文件 VS 版本
(03,05,08,10)，CONFIG += ***用来控制如何生成项目文件。项目文件支持 4 个预定义参
数：

DLL_SOUI:代表将 SOUI 模块编译生成一个 DLL，没有该参数则生成 LIB；

USING_MT:代表使用 MT 方式连接 CRT，否则采用 MD 方式；

CAN_DEBUG:为 release 版本生成调试符号；

USING_CLR:项目提供“公共语言运行时”支持；

如果需要其它配置，可以手动修改 common.pri。

- SOUI提供了多种编译方式包括qmake,cmake,nmake等等.我们推荐使用qmake方式生成符合自己的Visual Studio 版本项目工程文件,当然,如果你有兴趣也可以尝试cmake与nmake两种方式

## qmake(推荐)

    使用 git 摘取代码后,进入代码根目录,双击运行"build.bat"

- `1.选择编译版本[1=x86;2=x64;3=x86+x64]:`选择需要编译的cpu架构(eg:1则表示生成win32的可执行文件)
- `2.选择开发环境[1=2008;2=2010;3=2012;4=2013;5=2015;6=2017;7=2005]:`选择对应的 Visual Studio 版本(eg:1表示选择使用 Visual Studio 2008)注意SOUI至少需要Visual Studio 2008 SP1及以上的 Visual Studio 版本
- `3.选择SOUI编译模式[1=全模块DLL;2=全模块LIB;3=内核LIB,组件DLL(不能使用LUA脚本模块)]:`选择生成内核的文件方式(eg:1表示所生成的内核文件及组件均为dll)
- `4.选择字符集[1=UNICODE;2=MBCS]:`(推荐选1)
- `5.将WCHAR作为内建类型[1=是;2=否]:`(推荐选1)
- `6.选择CRT链接模式[1=静态链接(MT);2=动态链接(MD)]:`(根据自大项目需求选择)
- `7.是否为release版本生成调试信息[1=生成;2=不生成]:`(根据自大项目需求选择)
- `open[o], compile[c] "soui.sln" or quit(q) [o,c or q]?`输入英文字母o表示打开工程项目,c表示直接编译debug与release,q表示直接退出当前窗口

- ### `nmake`(目前仅支持编译成dll形式)

  - 打开编译工具命令控制台窗口,输入"nmake",默认生成 x86 release 的 soui 内核依赖与两个渲染组件(gdi各skia) 图片解码组件为 png 还有 demo 运行程序,CRT为动态链接
  - 其它额外编译参数如下:

    - `nmake TYPE=Debug` 表示生成 x86 debug 模式
    - `nmake ABI=x64` 表示生成 x64 的 release 模式,如果需要 debug 模式在后面增加 `TYPE=Debug` 即可
    - `nmake CRT=-MT` 表示静态链接CRT  

- ### `cmake`

  - 从cmake官网下载cmake的最新Release版本,这里以cmake-3.15.4-win64-x64.zip举例。

  - 将cmake-3.15.4-win64-x64.zip解压后运行bin目录下的cmake-gui.exe。

  - 选择soui源码目录和cmake临时文件生成目录，点击Configure。

  