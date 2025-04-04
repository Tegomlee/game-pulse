# Global
cmake_minimum_required(VERSION 3.26)
project(GamePulse C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# GamePulse
add_library(gamepulse SHARED
  src/gamepulse.c
)

target_include_directories(gamepulse PUBLIC
  ${CMAKE_SOURCE_DIR}/include
)

target_compile_definitions(gamepulse PUBLIC
  GP_EXPORT
)

# Tests with Unity (Not the engine)
include(FetchContent)

FetchContent_Declare(
  unity
  GIT_REPOSITORY https://github.com/ThrowTheSwitch/Unity.git
  GIT_TAG        master
)
FetchContent_MakeAvailable(unity)

enable_testing()
add_test(NAME GamePulseTests COMMAND gamepulse_tests)

# add_executable(gamepulse_tests
#   tests/gamepulse_test.c
# )

# target_link_libraries(gamepulse_tests
#   gamepulse
#   unity
# )

# target_include_directories(gamepulse_tests PRIVATE
#   ${CMAKE_SOURCE_DIR}/include
#   ${unity_SOURCE_DIR}/src
# )
