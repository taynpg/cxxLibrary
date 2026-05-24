# 示例代码

```c++
#include <spdlog/spdlog.h>
#include <spdlog/sinks/daily_file_sink.h>
#include <spdlog/sinks/stdout_color_sinks.h>

bool initLogger()
{
    try {
        spdlog::level::level_enum lv = spdlog::level::trace;
        
        // auto file_sink = std::make_shared<spdlog::sinks::rotating_file_sink_mt>("xx", 1024 * 50, 3);
        auto file_sink = std::make_shared<spdlog::sinks::daily_file_sink_mt>(logPath_, 0, 0);
        auto console_sink = std::make_shared<spdlog::sinks::stdout_color_sink_mt>();

        file_sink->set_pattern("[%Y-%m-%d %H:%M:%S.%e][%l]: %v\n    =>%s:%#");
        console_sink->set_pattern("%^[%H:%M:%S.%e][%l]: %v%$\n    =>%s:%#");
        std::vector<spdlog::sink_ptr> sinks{file_sink, console_sink};
        logger_ = std::make_shared<spdlog::logger>(markStr_, sinks.begin(), sinks.end());

        spdlog::register_logger(logger_);
        spdlog::set_default_logger(logger_);
        spdlog::set_level(lv);

        return true;
    } catch (const std::exception& e) {
        std::cerr << __FUNCTION__ << ":" << e.what() << std::endl;
        return false;
    }
}

// SPDLOG_INFO("log测试ttt。。。");
```

