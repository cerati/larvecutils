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

project(larvecutils VERSION 09.32.01 LANGUAGES CXX C)

# cetbuildtools contains our cmake modules
# find_package(cetbuildtools REQUIRED)
find_package(cetmodules REQUIRED)

list(APPEND CMAKE_MODULE_PATH $ENV{CANVAS_ROOT_IO_DIR}/Modules $ENV{ART_DIR}/Modules)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
#find_ups_product( larsoft )
#find_ups_product( nutools )
#find_ups_product( art )
#find_ups_product( cetbuildtools ) # LIBRARY_OUTPUT_DIRECTORY, etc.

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(larvecutils)

# tests
add_subdirectory(test)

# ups - table and config files
#add_subdirectory(ups)

# packaging utility
#include(UseCPack)
