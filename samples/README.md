# OpenVR Samples: CMake build guide.

## Support

|      Configuration      |    32     |    64     |
| ----------------------- |:---------:|----------:|
| GNU/Linux   (gcc 4.8+)  |   OK      |    OK     |
| Windows     (msvc 2022) |   OK      |    OK     |
| OSX         (clang)     |   ~       |    ~      |


## Dependencies

* Qt 6.x
* GLEW 1.11+
* SDL2
* OpenVR

The only general external dependency is [Qt6](https://www.qt.io/download-open-source).<br/>
On GNU/Linux, you will need GLEW 1.11 (available on most package manager).<br/>
On Windows x64, you will need the SDL2 runtime library.

## Build

**Important:**<br/>
*you might need to specify Qt6 cmake module path manually when generating the cache for the first time using the __CMAKE_PREFIX_PATH__ macro (see examples below).*

We will use the command-line on Unix and [Git Bash](https://git-for-windows.github.io/) on Windows.

First, move from the repository root to the samples directory to create a build directory:
```
cd samples
mkdir build; cd build
```

Then, depending on your system:

### Unix

Generate the CMake cache using Makefile:
```
cmake .. -G Makefile -DCMAKE_PREFIX_PATH=/opt/Qt/6.9.2/gcc_64/lib/cmake -DCMAKE_BUILD_TYPE=Release
```

To build type:
```
make -j4
```


### Windows

Generate the CMake cache using MSVC 2022 for x64:
```
cmake .. -G "Visual Studio 17 2022 Win64" -DCMAKE_PREFIX_PATH=C:/Qt/6.9.2/msvc2022_64/lib/cmake
```

Alternatively, you can force the compilation on x86 architectures by using the **PLATFORM** property (*be sure to use the right generator and Qt binaries*):
```
cmake .. -G "Visual Studio 17 2022" -DCMAKE_PREFIX_PATH=C:/Qt/6.9.2/msvc2022_64/lib/cmake -DPLATFORM=32
```

To build, simply type:
```
cmake --build . --target all --config Release
```

*Note : using CMake, the build configuration type (ie. Debug, Release) is set at Build Time with MSVC and at Cache Generation Time with Makefile.*

To run the application, several DLL files from Qt6 are needed. Here's an example for Windows:

In the samples/bin/win64 directory, delete all Qt5 DLL files.

Then copy the following files and folder from <qt install dir>/<version>/<msvc2022_64> to the samples/bin/win64 directory:
- bin/Qt6Widgets.dll
- bin/Qt6Core.dll
- bin/Qt6Gui.dll
- bin/Qt6OpenGL.dll
- bin/Qt6OpenGLWidgets.dll
- bin/Qt6Widgetsd.dll
- bin/Qt6OpenGLd.dll
- bin/Qt6Guid.dll
- bin/Qt6Cored.dll
- plugins/platforms directory

---
