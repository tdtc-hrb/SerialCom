Qt development environment with Visual Studio
====
- Qt online installer: v4.8.0
- Visual Studio 2019: v16.11

## [Qt在线安装程序](https://download.qt.io/official_releases/online_installers/)
Qt6.5.3 -> MSVC 2019 64-bit    
![qt-online-msvc2019](https://raw.githubusercontent.com/tdtc-hrb/cnblogs/master/images/qt-online48-msvc2019.png)    
以下几项为安装程序默认勾选:    
![qt-online-creator](https://raw.githubusercontent.com/tdtc-hrb/cnblogs/master/images/qt-online48-creator.png)
![qt-online-cmake](https://raw.githubusercontent.com/tdtc-hrb/cnblogs/master/images/qt-online48-cmake.png)

### Additional Libraries
在Qt6中需要勾选: Qt Serial Port
![serial port - qt online](https://raw.githubusercontent.com/tdtc-hrb/cnblogs/master/images/qt-online48-serial_port.png)

## Download options for VS
```bash
.\vs_Community.exe --layout D:\win10soft\vs2019 `
--add Microsoft.VisualStudio.Component.CoreEditor `
--add Microsoft.VisualStudio.Workload.CoreEditor `
--add Microsoft.VisualStudio.Component.Roslyn.Compiler `
--add Microsoft.Component.MSBuild `
--add Microsoft.VisualStudio.Component.TextTemplating `
--add Microsoft.VisualStudio.Component.VC.CoreIde `
--add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 `
--add Microsoft.VisualStudio.Component.Windows10SDK.19041 `
--add Microsoft.VisualStudio.Component.VC.Redist.14.Latest `
--add Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core `
--add Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset `
--add Microsoft.VisualStudio.Component.VC.Llvm.Clang `
--add Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang `
--add Microsoft.VisualStudio.Workload.NativeDesktop --lang en-US
```

## CMake in Qt Creator
程序设置：
```bash
-GNinja
-DCMAKE_BUILD_TYPE:STRING=Release
-DCMAKE_PROJECT_INCLUDE_BEFORE:PATH=%{IDE:ResourcePath}/package-manager/auto-setup.cmake
-DQT_QMAKE_EXECUTABLE:STRING=%{Qt:qmakeExecutable}
-DCMAKE_PREFIX_PATH:STRING=%{Qt:QT_INSTALL_PREFIX}
-DCMAKE_C_COMPILER:STRING=%{Compiler:Executable:C}
-DCMAKE_CXX_COMPILER:STRING=%{Compiler:Executable:Cxx}
```

## Deploy
```bash
C:\Qt\6.5.3\msvc2019_64\bin\windeployqt --qmldir C:\Users\tdtc\Documents\SerialCom\SerialCom\QtRaspberry C:\Users\tdtc\Documents\SerialCom_qml\serialCom.exe
```
