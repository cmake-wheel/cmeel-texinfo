cmake_minimum_required(VERSION 3.20)

set(NAME texinfo)
set(VERSION 7.0.3)

project(cmeel-${NAME} VERSION ${VERSION})

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://ftp.gnu.org/gnu/${NAME}/${NAME}-${VERSION}.tar.xz"
  URL_HASH "SHA1=356a623b88401d7c993408f33450c8104aad9df8"
  DOWNLOAD_EXTRACT_TIMESTAMP OFF
  BUILD_IN_SOURCE ON
  CONFIGURE_COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
  BUILD_COMMAND "make"
  INSTALL_COMMAND "make" "install")

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-${NAME}/)
