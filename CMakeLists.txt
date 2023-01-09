cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(mozy)

include(cmakescript/CPM.cmake)

CPMAddPackage("gh:nlohmann/json@3.11.2")
CPMAddPackage(
        NAME ffmpeg   # 添加依赖库：googletest
        GITHUB_REPOSITORY FFmpeg/FFmpeg # GitHub仓库是：FFmpeg/FFmpeg
        GIT_TAG release/5.1 # Git标签是release/5.1
        VERSION 5.1 # 版本号是5.1

)

add_executable(mozy src/main.cpp)
target_compile_features(mozy PRIVATE cxx_std_17)
target_link_libraries(mozy nlohmann_json::nlohmann_json ffmpeg)