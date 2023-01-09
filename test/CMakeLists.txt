cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(mozyTest)

include(../cmakescript/CPM.cmake)

CPMAddPackage("gh:cpm-cmake/testpack-fibonacci@2.0")
CPMAddPackage("gh:nlohmann/json@3.11.2")

CPMAddPackage(
        NAME googletest
        GITHUB_REPOSITORY google/googletest
        GIT_TAG release-1.12.1
        VERSION 1.12.1
        OPTIONS "INSTALL_GTEST OFF" "gtest_force_shared_crt"
)
CPMAddPackage(
        NAME ffmpeg   # 添加依赖库：googletest
        GITHUB_REPOSITORY FFmpeg/FFmpeg # GitHub仓库是：FFmpeg/FFmpeg
        GIT_TAG release/5.1 # Git标签是release/5.1
        VERSION 5.1 # 版本号是5.1

)

# ---- Create binary ----

add_executable(mozyTest test.cpp)
target_link_libraries(mozyTest fibonacci gtest gtest_main gmock nlohmann_json::nlohmann_json ffmpeg)
target_compile_features(mozyTest PRIVATE cxx_std_17)

# ---- Enable testing ----

enable_testing()
add_test(mozyTest mozyTest)