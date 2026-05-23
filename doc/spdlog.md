# 示例代码

```c++
#include <spdlog/spdlog.h>
#include <spdlog/sinks/daily_file_sink.h>
#include <spdlog/sinks/stdout_color_sinks.h>

bool initLogger()
{
    try {
        // auto file_sink = std::make_shared<spdlog::sinks::rotating_file_sink_mt>("xx", 1024 * 50, 3);
        auto file_sink = std::make_shared<spdlog::sinks::daily_file_sink_mt>("Demo.log", 0, 0);
        auto console_sink = std::make_shared<spdlog::sinks::stdout_color_sink_mt>();

        file_sink->set_pattern("[%Y-%m-%d %H:%M:%S.%e] [%s:%#] [%l]: %v");
        console_sink->set_pattern("%^[%H:%M:%S.%e] [%s:%#] [%l]: %v%$");
        std::vector<spdlog::sink_ptr> sinks{file_sink, console_sink};
        logger = std::make_shared<spdlog::logger>("Demo", sinks.begin(), sinks.end());
        logger->set_level(spdlog::level::debug);
        spdlog::register_logger(logger);
        spdlog::set_default_logger(logger);
        return true;
    }
    catch (const std::exception& e) {
        return false;
    }
}

// SPDLOG_INFO("log测试ttt。。。");
```

