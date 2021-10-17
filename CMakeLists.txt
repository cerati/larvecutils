# ======================================================================
#  larvecutils main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larvecutils/ups/setup_for_development <-d|-p>
#  cmake [-DCMAKE_INSTALL_PREFIX=/install/path]
#        -DCMAKE_BUILD_TYPE=$CETPKG_TYPE
#        $CETPKG_SOURCE
#  make
#  make test
#  make install
#  make package (builds distribution tarfile)
# ======================================================================


cmake_minimum_required(VERSION 3.19 FATAL_ERROR)

project(larvecutils VERSION 09.32.01 LANGUAGES CXX)

find_package(cetmodules REQUIRED)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
find_package( art )
find_package( art_root_io )
find_package(canvas_root_io)
find_package( canvas )
find_package( PostgreSQL )
find_package( Range-v3 )

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
#include(BuildPlugins)

# source
add_subdirectory(larvecutils)

# tests
#add_subdirectory(test)

add_subdirectory(cmakeConfig)
cet_cmake_config()
