cmake_minimum_required(VERSION 3.5)

project(FFPlayer VERSION 0.0.1 )

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#ffmpeg
set(FFMPEG_PREFIX_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libs/ffmpeg")
message("FFMPEG_PREFIX_DIR=${FFMPEG_PREFIX_DIR}")
set(FFMPEG_INCLUDE_DIRS "${FFMPEG_PREFIX_DIR}/include/")
set(FFMPEG_LIB_DIRS "${FFMPEG_PREFIX_DIR}/lib/")

#SDL2
set(SDL2_PREFIX_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libs/SDL2")
set(SDL2_INCLUDE_DIRS "${SDL2_PREFIX_DIR}/include/SDL2")
set(SDL2_LIBS_DIRS "${SDL2_PREFIX_DIR}/lib/")

set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)
set(UTILS_DIR ${SRC_DIR}/utils)

message("SDL2_PREFIX_DIR: ${SDL2_PREFIX_DIR}")
message("SDL2_INCLUDE_DIRS: ${SDL2_INCLUDE_DIRS}")

include_directories(${UTILS_DIR})
include_directories(${FFMPEG_INCLUDE_DIRS})
include_directories(${SRC_DIR})
include_directories(${SDL2_INCLUDE_DIRS})

link_directories(${FFMPEG_LIB_DIRS})
link_directories(${SDL2_LIBS_DIRS})

set(PROJECT_SOURCES
        src/cmdutils.c
        src/ffplay.c
        src/utils/log4z.cpp
        )
add_executable(FFPlayer
        ${PROJECT_SOURCES}
        )

target_link_libraries(FFPlayer PRIVATE
        #FFmpeg 支持
        avcodec avdevice avfilter avformat avutil swscale swresample SDL2
        )


