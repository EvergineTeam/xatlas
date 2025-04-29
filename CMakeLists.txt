cmake_minimum_required(VERSION 3.15)
project(xatlas LANGUAGES CXX)

# 1) Collect sources
file(GLOB_RECURSE XATLAS_HEADERS
     "${CMAKE_CURRENT_SOURCE_DIR}/source/xatlas/*.h")
file(GLOB_RECURSE XATLAS_SOURCES
     "${CMAKE_CURRENT_SOURCE_DIR}/source/xatlas/*.cpp")

# 2) Create a shared library
add_library(xatlas SHARED
    ${XATLAS_SOURCES}
    ${XATLAS_HEADERS}
)

# 3) Ensure PIC (for Linux/macOS) and automatic exports on Windows
set_target_properties(xatlas PROPERTIES
    POSITION_INDEPENDENT_CODE ON
    WINDOWS_EXPORT_ALL_SYMBOLS ON
)

# 4) Force the base name “xatlas” on all platforms
set_target_properties(xatlas PROPERTIES
    OUTPUT_NAME "xatlas"
    # On macOS you may want a versioned dylib:
    # VERSION ${PROJECT_VERSION}
    # SOVERSION ${PROJECT_VERSION_MAJOR}
)

# 5) Install rules (if you plan to `make install`)
install(TARGETS xatlas
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)
