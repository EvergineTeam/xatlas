cmake_minimum_required(VERSION 3.10)
project(xatlas LANGUAGES C CXX)

# Force C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Where to find headers
include_directories(
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/source/xatlas>
  $<INSTALL_INTERFACE:include>
)

# Gather sources
set(XATLAS_SRCS
  source/xatlas/xatlas.cpp
)

set(XATLAS_HDRS
  source/xatlas/xatlas.h
  source/xatlas/xatlas_c.h
)

# Build static library
add_library(xatlas STATIC
  ${XATLAS_SRCS}
  ${XATLAS_HDRS}
)

# Install rules (if you ever want to 'make install')
install(TARGETS xatlas
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)
install(FILES ${XATLAS_HDRS} DESTINATION include/xatlas)
