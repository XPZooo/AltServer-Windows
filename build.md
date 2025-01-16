# 0.
git submodule update --init --recursive

vcpkg安装-关于Visual Studio：vcpkg：
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg; .\bootstrap-vcpkg.bat

# 3.
vcpkg install cpprestsdk cpprestsdk:x86-windows
vcpkg install dirent dirent:x86-windows
vcpkg install mdnsresponder mdnsresponder:x86-windows

# 4.
./Dependencies/libmobiledevice-vs/get-source.cmd



# 5. 下载并编译WinSparkle；您需要将生成的 LIB 复制到 (root)\Dependencies\release 中



+  （1）程序中Dependencies好像已经有相关库了

+  （2）https://github.com/vslavik/winsparkle 手动编译，以下配置完成打开 `WinSparkle.sln` 可直接编译成功

  ```
  $ git clone https://github.com/vslavik/winsparkle.git
  $ cd winsparkle
  $ git submodule init
  $ git submodule update
  ```

+ + 

  

# 6. 在项目 LDID 中将语言标准从 c++14 更改为 c++17，关闭智能感知错误（误导）并修复[此 PR中修复的两个错误](https://github.com/rileytestut/AltServer-Windows/pull/1)

## 尝试编译

+ AltServer-Windows-env\Dependencies\libimobiledevice-vs\libimobiledevice\common\userpref.c(45,10): error C1083: 无法打开包括文件: “openssl/bn.h”: No such file or directory
  + 解决方法，下载`openssl sdk`
  + vcpkg install openssl openssl:x86-windows
  + `AltServer AltSign imobiledevice ldid` 项目都需要配置openSSL

## 处理LDID编译报错问题

+ LLID 编译环境配置

  + https://blog.csdn.net/m0_47587308/article/details/141132952

  + 主要处理1，下载安装 [Clang.exe](https://github.com/llvm/llvm-project/releases/)

  + 主要处理2

    创建`*Directory.build.props*`文件，添加到程序`sln`目录中

    ```
    <Project>
      <PropertyGroup>
        <LLVMInstallDir>C:\MyLLVMRootDir</LLVMInstallDir>
        <LLVMToolsVersion>17.0.6</LLVMToolsVersion>
      </PropertyGroup>
    </Project>
    ```

## 

# 7. 在 Connection.cpp 中添加以下导入：`#include <codecvt>`







# 依赖库处理

+ 附加库目录添加：`D:\A-D2\workspace\IOS\ipa-sign\AltServer-Windows-env-build\vcpkg\installed\x86-windows\lib`

+ `openssl` 依赖库问题处理

  附加依赖项添加： 

  ```
  libcrypto.lib;libeay32.lib;libssl.lib;ssleay32.lib;
  zlib.lib
  cpprest_2_10.lib
  zlib.lib
  cpprest_2_10.lib
  ```

# 运行问题处理

+ 确定exe目录，确定添加的`dll`最好匹配添加的依赖库`.lib`
+ 添加`D:\A-D2\workspace\IOS\ipa-sign\AltServer-Windows-env\Dependencies\Libraries`中所有`dll`
+ 添加`D:\A-D2\workspace\IOS\ipa-sign\AltServer-Windows-env-build\vcpkg\installed\x86-windows\bin`中所有`dll`

+ `libmobiledevice`相关依赖：`D:\A-D2\workspace\IOS\ipa-sign\AltServer-Windows-env\Win32\Release`中所有`dll`







​		
