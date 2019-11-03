cmake_minimum_required(VERSION 3.9)
project(CMakeOverload)

enable_testing()

# Number of generated tests
# These numbers are for Intel i7-8750HQ - increase if you have a faster chip:
# 1000 - works
# 2000 - takes a disproportionately long time
# 3000 and up - configuration crashes with:
#   ctest.exe --show-only=json-v1 -C Debug did not finish after 1m 0s, 0ms
# Tweak this to cause (or not cause) crashes
set(TestCount 5000)

# Get a list of tests from the python script
execute_process(
    COMMAND python "${CMAKE_CURRENT_SOURCE_DIR}/list.py" ${TestCount}
    OUTPUT_VARIABLE TestsString
    OUTPUT_STRIP_TRAILING_WHITESPACE)

# Format the list in a way which works with CMake's foreach
# (semicolon-separated)
string(REPLACE "\n" ";" TestsList ${TestsString})

# For each entry in the list, create a test which just prints it out
foreach(Test ${TestsList})
    add_test(
        NAME "Test-${Test}"
        COMMAND powershell -Command "echo ${Test}")
endforeach()
