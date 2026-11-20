cmake_minimum_required(VERSION 3.10)

# Load the PSP platform configuration BEFORE project()
set(CMAKE_SYSTEM_CMAKE_PLATFORM_PATH "${CMAKE_SOURCE_DIR}/cmake")

project(M3D C CXX ASM)

subdirs(external/oslib)

# Always export a compilation database; run-cppcheck.sh analyses through it.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Set C and C++ standards
set(CMAKE_C_STANDARD 23)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

# Set the output library
set(TARGET_LIB M3D)
add_library(${TARGET_LIB} STATIC)

# Specify the output directory for the .a file (project root directory)
set_target_properties(${TARGET_LIB} PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
)

# Include directories
include_directories(
    INTERFACE PUBLIC_HEADER  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    src
    ${PROJECT_SOURCE_DIR}/external/bullet3/src
    ${PROJECT_SOURCE_DIR}/external/oslib/src
)


# Define the source files
set(SOURCE_DIR src)

set(LIB_SOURCES 
${SOURCE_DIR}/AMG_3D.cpp
${SOURCE_DIR}/AMG_3D.h
${SOURCE_DIR}/AMG_Error_Image.png
${SOURCE_DIR}/AMG_Error_Image_B.png
${SOURCE_DIR}/AMG_Error_Sound.mp3
${SOURCE_DIR}/AMG_Font1.png
${SOURCE_DIR}/AMG_Font2.png
${SOURCE_DIR}/AMG_Model.cpp
${SOURCE_DIR}/AMG_Model.h
${SOURCE_DIR}/AMG_ModelAnim.cpp
${SOURCE_DIR}/AMG_Multimedia.cpp
${SOURCE_DIR}/AMG_Multimedia.h
${SOURCE_DIR}/AMG_Physics.cpp
${SOURCE_DIR}/AMG_Physics.h
${SOURCE_DIR}/AMG_Texture.cpp
${SOURCE_DIR}/AMG_Texture.h
${SOURCE_DIR}/AMG_TriParticle.h
${SOURCE_DIR}/AMG_User.cpp
${SOURCE_DIR}/AMG_User.h
${SOURCE_DIR}/AMG_VFPU.cpp
${SOURCE_DIR}/AMG_TriParticle.cpp
${SOURCE_DIR}/AMG_TriParticle.h
${SOURCE_DIR}/Makefile
${SOURCE_DIR}/lightmap.h
${SOURCE_DIR}/pspDveManager.S
)

# Specify that stub.S is an assembly file
set_source_files_properties(${SOURCE_DIR}/pspDveManager.S PROPERTIES LANGUAGE ASM)

# Suppress warnings for third-party library sources. Like the Makefile's CFLAGS_THIRD_PARTY,
# they don't get _PSP_FW_VERSION: libccc would switch to its sceIo path, which isn't the tested one
set_source_files_properties(
    PROPERTIES
    COMPILE_FLAGS "-w -U_PSP_FW_VERSION"
)

# Add sources to the target
target_sources(${TARGET_LIB} PRIVATE
    ${LIB_SOURCES}
)

# Installation instructions
install(TARGETS ${TARGET_LIB} DESTINATION ${PSPDIR}/lib)

