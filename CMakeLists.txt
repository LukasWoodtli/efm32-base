# Base EFM32 CMake file
#
# This can be used as is as a project base, or by adding the efm32-base
# repository as a submodule to another project, copying this CMakeLists file
# to the top level directory, and updating the BASE_LOCATION variable to reflect this
# change
#
## Copyright (c) 2016 Ryan Kurte
# This file is covered under the MIT license available at: https://opensource.org/licenses/MIT

###### Project Environment #####

# Set minimum CMake version
cmake_minimum_required(VERSION 2.8.4)

# Set efm32-base project location
set(BASE_LOCATION .)

# Set the compiler (must be prior to project setup)
include(${BASE_LOCATION}/toolchain/arm-gcc.cmake)

##### Project Setup #####

# Set our output target
set(TARGET FreeRtosExamples)

# Configure project and languages
project(${TARGET} C CXX ASM)

# Set device
set(DEVICE EFM32TG840F32)

add_definitions(-DEFM32TG840F32)
add_definitions(-DGCC_ARMCM3)
add_definitions(-DDEBUG)
add_definitions(-DDEBUG_EFM)


# Set build
if(NOT CMAKE_BUILD_TYPE)
set(CMAKE_BUILD_TYPE DEBUG)
endif()

##### Modules #####

# Libraries can be added to the LIBS variable
# or manually included here.

# Add base libs (emlib, CMSIS, device files)

include(${BASE_LOCATION}/bsp/bsp.cmake)

include(${BASE_LOCATION}/emdrv/emdrv.cmake)

include(${BASE_LOCATION}/toolchain/efm32-base.cmake)

include(${BASE_LOCATION}/cmsis/cmsis.cmake)

include(${BASE_LOCATION}/FreeRTOS/freertos.cmake)


##### Files #####



# projects
add_subdirectory("source")





##### Post build #####

# Add post build commands
include(${BASE_LOCATION}/toolchain/post-build.cmake)

# Add JLink commands
include(${BASE_LOCATION}/toolchain/jlink.cmake)

