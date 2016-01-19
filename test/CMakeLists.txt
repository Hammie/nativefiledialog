cmake_minimum_required (VERSION 2.6)
project (NativeFileDialog)

if(MSVC OR MSVC80)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /W4")

  set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /MD")
  set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /O2")

  set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} /MDd")
  set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} /Z7")
elseif(CMAKE_COMPILER_IS_GNUC OR APPLE)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -pedantic")

  set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3")

  set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g")
endif()

if(APPLE)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fcolor-diagnostics")
endif()

if(APPLE)
  list(APPEND TEST_SOURCE_FILES "nfd_cocoa.m")
endif()

include_directories(../src/include)

find_library(APPKIT AppKit)

set(BUNDLE_OPTION "")

if(APPLE)
  set(BUNDLE_OPTION "MACOSX_BUNDLE")
endif()

add_executable(test_opendialog ${BUNDLE_OPTION} "test_opendialog.c")
target_link_libraries(test_opendialog nfd ${APPKIT})

add_executable(test_opendialogmultiple ${BUNDLE_OPTION} "test_opendialogmultiple.c")
target_link_libraries(test_opendialogmultiple nfd ${APPKIT})

add_executable(test_savedialog ${BUNDLE_OPTION} "test_savedialog.c")
target_link_libraries(test_savedialog nfd ${APPKIT})
