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

set(fcl_dir job)
set(gdml_dir gdml)
find_package( cetmodules )

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
#find_package( PostgreSQL REQUIRED )
find_package( Range-v3 )
find_package( lardataobj REQUIRED)
find_package( lardataalg REQUIRED)
find_package( larcore  REQUIRED)
find_package( nutools  REQUIRED)

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(larvecutils)

# tests
add_subdirectory(test)

add_subdirectory(cmakeConfig)

