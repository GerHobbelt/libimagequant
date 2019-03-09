cmake_minimum_required(VERSION 2.6)

project(imagequant C)
include(GNUInstallDirs)

option(BUILD_WITH_SSE "Use SSE" ON)

if(BUILD_WITH_SSE)
  add_definitions(-DUSE_SSE=1)
endif()

include_directories(${CMAKE_SOURCE_DIR})

if(CMAKE_COMPILER_IS_GNUCC)
  add_compile_options("-std=c99")
endif()

set(SOURCE 
  libimagequant.c
  blur.c
  mediancut.c
  mempool.c
  nearest.c
  pam.c
  kmeans.c)
set(HEADER
  libimagequant.h
  blur.h
  mediancut.h
  mempool.h
  nearest.h
  pam.h
  kmeans.h)
  
add_library(imagequant STATIC ${SOURCE} ${HEADER})
target_include_directories(imagequant PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

install(FILES ${HEADER} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/imagequant)
install(TARGETS imagequant ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
