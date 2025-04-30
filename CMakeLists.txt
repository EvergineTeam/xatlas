cmake_minimum_required(VERSION 3.12)
project(xatlas LANGUAGES CXX)
 
# Shared library
add_library(xatlas SHARED)
 
# C++11 standard
target_compile_features(xatlas PUBLIC cxx_std_11)
 
# Disable exceptions and RTTI
target_compile_options(xatlas PRIVATE
    $<$<CXX_COMPILER_ID:GNU,Clang>:-fno-exceptions -fno-rtti -Wall -Wextra -Wshadow>
    $<$<CXX_COMPILER_ID:MSVC>:/EHs- /GR- /W4>
)
 
# Defines
target_compile_definitions(xatlas PRIVATE
    XATLAS_C_API=1
    XATLAS_EXPORT_API=1
)
 
# Source files
file(GLOB XATLAS_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/source/xatlas/*.*")
target_sources(xatlas PRIVATE ${XATLAS_SOURCES})
 
# Optional: Sanitizers (if needed)
option(ENABLE_SANITIZERS "Enable sanitizers" OFF)
 
if(ENABLE_SANITIZERS)
    target_compile_options(xatlas PRIVATE -fsanitize=address,undefined)
    target_link_options(xatlas PRIVATE -fsanitize=address,undefined)
endif()