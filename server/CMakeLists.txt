#
# irony-server executable build file
#
find_package (LibClang REQUIRED)
find_package (Threads REQUIRED)

include_directories (${LibClang_INCLUDE_DIRS})
include_directories (${IRONY_UTILS_INCLUDES})
include_directories (${CMAKE_CURRENT_SOURCE_DIR})

#
# irony-server executable
#
add_executable (irony-server
  # Main sources
  IPlugin.h
  IPlugin.cpp
  Server.cpp
  Server.h
  TUManager.cpp
  TUManager.h
  main.cpp

  # "Built-in" plugins sources
  plugins/CodeCompletion.cpp
  plugins/CodeCompletion.h
  plugins/SyntaxChecker.cpp
  plugins/SyntaxChecker.h
  )

add_dependencies (irony-server
  # Dependencies
  irony-utils
  )

target_link_libraries (irony-server
  irony-utils
  ${LibClang_LIBRARIES}
  ${CMAKE_THREAD_LIBS_INIT}
  )

install (TARGETS irony-server
  RUNTIME DESTINATION ${IRONY_SOURCE_DIR}/bin)