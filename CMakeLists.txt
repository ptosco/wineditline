cmake_minimum_required (VERSION 2.8.12)
project (WinEditLine)
set (WinEditLine_VERSION_MAJOR 2)
set (WinEditLine_VERSION_MINOR 2)
if (MSVC AND MSVC_USE_STATIC_RUNTIME)
foreach(flag_var
        CMAKE_C_FLAGS CMAKE_C_FLAGS_DEBUG CMAKE_C_FLAGS_RELEASE
        CMAKE_C_FLAGS_MINSIZEREL CMAKE_C_FLAGS_RELWITHDEBINFO)
   if(${flag_var} MATCHES "/MD")
      string(REGEX REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
   endif(${flag_var} MATCHES "/MD")
endforeach(flag_var)
endif()
if(NOT DEFINED LIB_SUFFIX)
  if(CMAKE_SIZEOF_VOID_P MATCHES 4)
    set(LIB_SUFFIX "32")
  else()
    set(LIB_SUFFIX "64")
  endif()
endif()
configure_file (
  "${PROJECT_SOURCE_DIR}/src/config.h.in"
  "${PROJECT_BINARY_DIR}/config.h"
)
add_subdirectory (src)
