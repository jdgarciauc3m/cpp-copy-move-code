cmake_minimum_required(VERSION 4.0)
project(hello LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

FetchContent_Declare(GSL
    GIT_REPOSITORY "https://github.com/microsoft/GSL"
    GIT_TAG "v4.0.0"
    GIT_SHALLOW ON
)

FetchContent_MakeAvailable(GSL)

add_compile_options(-Wall -Wextra -Werror -pedantic -pedantic-errors -Wconversion -Wsign-conversion)

# Enable clang-tidy
find_program(CLANG_TIDY_EXE NAMES clang-tidy)
if(CLANG_TIDY_EXE)
    set(CMAKE_CXX_CLANG_TIDY "${CLANG_TIDY_EXE};-header-filter=.*")
endif()

add_executable(hello main.cpp)
target_link_libraries(hello PRIVATE Microsoft.GSL::GSL)

