cmake_minimum_required(VERSION 3.16.0)

project(SFML_ProjectTemplate)

set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/build/bin)

set(SFML_DIR ${PROJECT_SOURCE_DIR}/3rdparty/SFML/lib/cmake/SFML)
set(SFML_SHARED_LIBRARIES_DIR ${PROJECT_SOURCE_DIR}/3rdparty/SFML/bin)

set(SFML_BUILD_NETWORK OFF)
set(SFML_BUILD_EXAMPLES OFF)
set(SFML_BUILD_DOC OFF)

find_package(SFML 2.5 COMPONENTS system graphics audio REQUIRED)

include_directories(${PROJECT_SOURCE_DIR}/src)

add_executable(
    SFML_ProjectTemplate
    ${PROJECT_SOURCE_DIR}/src/Main.cpp
)

target_link_libraries(
    SFML_ProjectTemplate
    sfml-graphics
)

add_custom_command(
    TARGET ${CMAKE_PROJECT_NAME}
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${SFML_SHARED_LIBRARIES_DIR}"
        "$<TARGET_FILE_DIR:${CMAKE_PROJECT_NAME}>"    
)
