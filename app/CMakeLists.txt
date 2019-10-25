cmake_minimum_required(VERSION 3.4.1)

find_library(log-lib log)

set(libs_include_DIR src/main/cpp/opus src/main/cpp/opus/arm)
include_directories(${libs_include_DIR})
ADD_DEFINITIONS(
        -DOPUS_BUILD
        -DDISABLE_FLOAT_API
        -DFIXED_POINT
        -DHAVE_ALLOCA_H
        -DUSE_ALLOCA
        -DCONFIG_OPUS_MODE=1
        -DCONFIG_OPUS_MODE_CELT=1
        -DCONFIG_OPUS_MODE_SILK=2
        -DCELT_C
        -D__CC_ARM
)
file(GLOB native_srcs "src/main/cpp/opus-lib.cpp" "src/main/cpp/opus/*.c")
add_library(opusJni SHARED ${native_srcs})
target_link_libraries(opusJni ${log-lib})
