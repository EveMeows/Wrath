cmake_minimum_required(VERSION 3.15)
project(Wrath LANGUAGES CXX VERSION 0.1)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Asan and Atan for debug builds.
if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(SANITIZER_FLAGS "-fsanitize=address,undefined -fno-omit-frame-pointer")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${SANITIZER_FLAGS}")
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${SANITIZER_FLAGS}")
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${SANITIZER_FLAGS}")
endif()

find_package(SFML COMPONENTS Network Graphics Window Audio System CONFIG REQUIRED)

add_library(${PROJECT_NAME} STATIC
  wrath/source/entity.cpp
  wrath/source/planet.cpp
  wrath/source/universe.cpp

  wrath/source/renderer.cpp
  wrath/source/shapes.cpp

  wrath/source/game.cpp
  wrath/source/content.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC
  wrath/include
)

target_link_libraries(${PROJECT_NAME} PRIVATE
  SFML::Network SFML::Graphics SFML::Window SFML::Audio SFML::System
)
