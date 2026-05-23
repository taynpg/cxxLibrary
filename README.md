# cxxLibray

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


## 一些小说明

### spdlog

如果使用WriteConsoleW，定义：

```cmake
add_definitions(-DSPDLOG_UTF8_TO_WCHAR_CONSOLE)
add_definitions(-DSPDLOG_WCHAR_TO_UTF8_SUPPORT)
```