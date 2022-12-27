cmake_minimum_required(VERSION 3.23)
set(CMAKE_CXX_STANDARD 17)
project(SimpleFarming)

if (APPLE)
    message("Detected macOS. Using macOS libraries...")

    set(SFML_DIR "lib/SFML-2.5.1OSX/Frameworks/SFML.framework/Resources/CMake")
    link_directories("lib/SFML-2.5.1OSX/lib")
    include_directories("lib/SFML-2.5.1OSX/include")

endif(APPLE)

if(WIN32)
    message("Detected Windows. Using Windows libraries...")

    set(SFML_DIR lib/SFML-2.5.1/lib/cmake/SFML)
    include_directories(lib/SFML-2.5.1/include)
endif(WIN32)

if(WIN32)
    find_package(SFML REQUIRED system window graphics network audio)
endif(WIN32)

if(APPLE)
    find_package(SFML 2.5.1 COMPONENTS REQUIRED system window graphics network audio)
endif(APPLE)

set(dir ${CMAKE_CURRENT_SOURCE_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${dir}/bin")

set(sources
        src/main.cpp)

add_executable(SimpleFarming ${sources})

#MAKE SURE TO INCLUDE -mwindows and -lsfml-main TO REMOVE THE CONSOLE WINDOW WHEN IN GUI.
target_link_libraries(SimpleFarming sfml-graphics sfml-window sfml-system)
target_link_options(SimpleFarming PRIVATE -static)
