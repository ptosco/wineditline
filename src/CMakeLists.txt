include(GenerateExportHeader)

set (WINEDITLINE_PRIVATE_SOURCES
  editline.c
  fn_complete.c
  history.c
  editline/wineditline.h
  editline/readline.h
)

add_library(edit_static STATIC)
add_library(WinEditLine::edit_static ALIAS edit_static)

set_target_properties(edit_static PROPERTIES
  PUBLIC_HEADER editline/readline.h)

target_sources(edit_static 
  PRIVATE 
    ${WINEDITLINE_PRIVATE_SOURCES}
  PUBLIC
    ${WINEDITLINE_PUBLIC_SOURCES}
  )

add_library(edit SHARED)
add_library(WinEditLine::edit ALIAS edit)
target_sources(edit 
  PRIVATE 
    ${WINEDITLINE_PRIVATE_SOURCES}
    libedit.def
  PUBLIC
    ${WINEDITLINE_PUBLIC_SOURCES}
  )

target_include_directories(edit PUBLIC 
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:include>
)

target_include_directories(edit_static PUBLIC 
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:include>
)

set_target_properties(edit PROPERTIES PREFIX "")
GENERATE_EXPORT_HEADER(edit
  BASE_NAME edit
  EXPORT_MACRO_NAME edit_EXPORT
  EXPORT_FILE_NAME edit_Export.h
  STATIC_DEFINE edit_BUILT_AS_STATIC
)

add_executable(edit_test libedit_test.c)
target_link_libraries(edit_test edit)
add_executable(edit_test_dll libedit_test_dll.c)
target_link_libraries(edit_test_dll edit)
# install (TARGETS edit edit_test edit_test_dll
#   DESTINATION "${CMAKE_INSTALL_PREFIX}/bin${LIB_SUFFIX}")
install (TARGETS edit_static edit edit_test edit_test_dll
  LIBRARY DESTINATION lib${LIB_SUFFIX}
  ARCHIVE DESTINATION lib${LIB_SUFFIX}
  RUNTIME DESTINATION bin${LIB_SUFFIX}
  PUBLIC_HEADER DESTINATION include
)

install(
  FILES
    $<TARGET_PDB_FILE:edit> 
    $<TARGET_PDB_FILE:edit_test>
    $<TARGET_PDB_FILE:edit_test_dll>
  DESTINATION bin${LIB_SUFFIX}
  OPTIONAL)

