cmake_minimum_required(VERSION 3.24)

set(VCPKG_ROOT "$ENV{VCPKG_ROOT}")

if (NOT CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "${VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake"
            CACHE FILEPATH "CMake toolchain file")
    message(STATUS "vcpkg toolchain found: ${CMAKE_TOOLCHAIN_FILE}")
endif ()

project(cmake_vcpkg_imgui_emscripten)

set(CMAKE_CXX_STANDARD 20)

find_package(Threads REQUIRED)
find_package(OpenGL REQUIRED)
find_package(SDL2 CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)

add_executable(cmake_vcpkg_imgui_emscripten main.cpp)

if(EMSCRIPTEN)
    set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX ".html")
    target_link_libraries(cmake_vcpkg_imgui_emscripten PRIVATE --shell-file ${CMAKE_SOURCE_DIR}/emscripten/shell_minimal.html)
endif()

target_link_libraries(cmake_vcpkg_imgui_emscripten PRIVATE Threads::Threads)
target_link_libraries(cmake_vcpkg_imgui_emscripten PRIVATE ${OPENGL_LIBRARIES})
target_include_directories(cmake_vcpkg_imgui_emscripten PRIVATE ${OPENGL_INCLUDE_DIR})
target_link_libraries(cmake_vcpkg_imgui_emscripten
        PRIVATE
        $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
        $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
        )
target_link_libraries(cmake_vcpkg_imgui_emscripten PRIVATE imgui::imgui)
