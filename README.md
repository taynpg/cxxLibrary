# cxxLibray

## cmake常用

部分一：

```cmake
cmake_minimum_required(VERSION 3.16)

project(Demo VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(MSVC)
    add_compile_options(/utf-8)
    #add_compile_options(/source-charset:utf-8)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
    add_definitions(-D_WIN32_WINNT=0x0601)
endif()

include_directories(C:/local/cxxLibrary/include)
add_executable(Demo main.cpp)
```

部分二：

```cmake
if (CMAKE_CXX_COMPILER_ID MATCHES "GNU" AND CMAKE_SYSTEM_NAME MATCHES "Windows")
    MESSAGE(STATUS "Csp Add MinGW Param.")
    add_compile_options(-finput-charset=utf-8)
    add_compile_options(-fexec-charset=gbk)
    set(COMPILER_ID "mingw")
    get_filename_component(CXX_COMPILER_PATH ${CMAKE_CXX_COMPILER} DIRECTORY)
    set(MINGW32_DLLS 
    "${CXX_COMPILER_PATH}/libgcc_s_dw2-1.dll"
    "${CXX_COMPILER_PATH}/libstdc++-6.dll"
    "${CXX_COMPILER_PATH}/libwinpthread-1.dll")
    install(FILES ${MINGW32_DLLS} DESTINATION bin)
endif()
```

部分三：

```cmake
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_CURRENT_LIST_DIR}/3rd/binary/mingw64)

set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib/${CMAKE_BUILD_TYPE})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE}/)
```



## CXX常用

```c++
#pragma once

#if defined(_WIN32) || defined(_WIN64)
#ifdef LIBRARY_EXPORTS
#define EXPORT_API __declspec(dllexport)
#else
#define EXPORT_API __declspec(dllimport)
#endif
#else
#define EXPORT_API __attribute__((visibility("default")))
#endif

#ifdef __cplusplus
extern "C" {
#endif

EXPORT_API int add(int a, int b);

#ifdef __cplusplus
}
#endif
```

## nlohmann/json

[Release JSON for Modern C++ version 3.12.0 · nlohmann/json](https://github.com/nlohmann/json/releases/tag/v3.12.0)

## fmtlib/fmt

[Release 12.1.0 · fmtlib/fmt](https://github.com/fmtlib/fmt/releases/tag/12.1.0)

- Optional header-only configuration enabled with the `FMT_HEADER_ONLY` macro

## CLIUtils/CLI11

[Release v2.6.1 · CLIUtils/CLI11 · GitHub](https://github.com/CLIUtils/CLI11/releases/tag/v2.6.1)

## leethomason/tinyxml2

[11.0.0](https://github.com/leethomason/tinyxml2/releases/tag/11.0.0)

## gabime/spdlog

[Version 1.17.0](https://github.com/gabime/spdlog/releases/tag/v1.17.0)

## chriskohlhoff/asio

[tag 1.38.0](https://github.com/chriskohlhoff/asio/tree/asio-1-38-0)


## 一些小说明

### spdlog

如果使用WriteConsoleW，定义：

```cmake
add_definitions(-DSPDLOG_UTF8_TO_WCHAR_CONSOLE)
add_definitions(-DSPDLOG_WCHAR_TO_UTF8_SUPPORT)

# 如果需要Debug和Trace生效，还需要
add_definitions(-DSPDLOG_ACTIVE_LEVEL=SPDLOG_LEVEL_TRACE)
```