project(game.libretro.desmume)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

include(ExternalProject)
externalproject_add(desmume
                    GIT_REPOSITORY https://github.com/libretro/desmume-libretro
                    GIT_TAG 40f9af5
                    PREFIX desmume
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -f Makefile.libretro
                    BUILD_IN_SOURCE 1)

set(DESMUME_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/desmume/src/desmume/desmume_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                          game.libretro.desmume${CMAKE_SHARED_LIBRARY_SUFFIX} desmume)

build_addon(game.libretro.desmume DESMUME DEPLIBS)
add_dependencies(game.libretro.desmume desmume)

include(CPack)
