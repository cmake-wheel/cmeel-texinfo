cmake_minimum_required(VERSION 3.20)

set(NAME texinfo)
set(VERSION 7.0.3)

project(cmeel-${NAME} VERSION ${VERSION})

execute_process(
  COMMAND "curl" "https://ftp.gnu.org/gnu/${NAME}/${NAME}-${VERSION}.tar.xz"
          --output "${NAME}-${VERSION}.tar.xz" COMMAND_ERROR_IS_FATAL ANY
  WORKING_DIRECTORY "${CMAKE_BINARY_DIR}")
execute_process(
  COMMAND "tar" "xf" "${NAME}-${VERSION}.tar.xz" COMMAND_ERROR_IS_FATAL ANY
  WORKING_DIRECTORY "${CMAKE_BINARY_DIR}")
execute_process(
  COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
          COMMAND_ERROR_IS_FATAL ANY
  WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/${NAME}-${VERSION}")
execute_process(COMMAND "make" COMMAND_ERROR_IS_FATAL ANY
                WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/${NAME}-${VERSION}")
execute_process(COMMAND "make" "install" COMMAND_ERROR_IS_FATAL ANY
                WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/${NAME}-${VERSION}")

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-${NAME}/)
