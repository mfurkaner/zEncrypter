
cmake_minimum_required(VERSION 3.11)

project(zEncrypter LANGUAGES CXX)

#add_compile_options(-O3)
#add_compile_options(-Wall)
add_compile_options(-std=c++11)

set(SRC
    ../src/main.cpp 
    ../src/application.cpp 
    ../src/mangler.cpp 
    ../src/encryptengine.cpp 
    ../src/hash.cpp
    ../src/filehandler.cpp
    ../src/configuration.cpp
)

set(INC
    ../inc/application.hpp 
    ../inc/ascii_avoid_list.hpp
    ../inc/encryptengine.hpp 
    ../inc/filehandler.hpp
    ../inc/mangler.hpp 
    ../inc/configuration.hpp
)

# For multi-config generators like Visual Studio, specify different output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_SOURCE_DIR}/Debug/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_SOURCE_DIR}/Release/lib)

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_SOURCE_DIR}/Debug/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_SOURCE_DIR}/Release/bin)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_SOURCE_DIR}/Debug/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_SOURCE_DIR}/Release/bin)

include_directories(inc)

add_executable(zEncrypter ${INC} ${SRC})


# Post-build copy command
add_custom_command(
    TARGET zEncrypter POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE}/zEncrypter.exe
    ${CMAKE_SOURCE_DIR}/../zEncrypter.exe

    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG}/zEncrypter.exe
    ${CMAKE_SOURCE_DIR}/../zEncrypter_dbg.exe

    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE}/zEncrypter.exe
    ${CMAKE_SOURCE_DIR}/../zEncryptUI/zEncryptUI/resources/zEncrypter.exe
)