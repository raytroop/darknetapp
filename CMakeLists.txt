cmake_minimum_required(VERSION 3.5.1)

# Define variables:

# Project name.
set(PROJ_NAME DarknetApp)
# Path to Darknet project folder.
set(DARKNET_PATH /home/raytroop/messy/DroNet)
# Give a custom name to shared library which is provided by Darkned when the one compiled.
set(DARKNET_LIB_NAME darknet)
# Define C++ level, could be 11 or 17 as well.
set(CMAKE_CXX_STANDARD 14)
# Define compiler optimization level.
set(CMAKE_CXX_FLAGS "-O3")
# Do print warnings uppon compilation, let's keep our code as clean as possible.
set(CMAKE_CXX_FLAGS "-Wall -Wextra")
# Apply flags.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

project(${PROJ_NAME})

find_library(DARKNET_LIB  NAMES ${DARKNET_LIB_NAME} HINTS ${DARKNET_PATH})

# Note: We do not recommend using GLOB or GLOB_RECURSE to collect a list of source files from your source tree.
# If no CMakeLists.txt file changes when a source is added or removed then the generated build system cannot know
# when to ask CMake to regenerate.
file(GLOB_RECURSE SOURCE_FILES "src/*")

add_executable(${PROJ_NAME} ${SOURCE_FILES})
# Link Darknet library' include folder.
target_include_directories(${PROJ_NAME} PUBLIC ${DARKNET_PATH}/include)
# Link all libraries together.
target_link_libraries(${PROJ_NAME} ${DARKNET_LIB})