cmake_minimum_required(VERSION 3.12)

project(tiniergltf
  VERSION 1.0.0
  LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)
FetchContent_Declare(
	jsoncpp
	GIT_REPOSITORY https://github.com/appgurueu/jsoncpp.git
	GIT_TAG 37dab289d99f463662c2bac8bd06622fbeeb4339
)
FetchContent_MakeAvailable(jsoncpp)

add_library(tiniergltf OBJECT tiniergltf.hpp base64.cpp base64.h)
add_library(tiniergltf::tiniergltf ALIAS tiniergltf)

get_target_property(JSON_INCLUDE_DIR jsoncpp_lib INTERFACE_INCLUDE_DIRECTORIES)

target_include_directories(tiniergltf
  INTERFACE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
	"${JSON_INCLUDE_DIR}"
)

target_link_libraries(tiniergltf jsoncpp_lib)
