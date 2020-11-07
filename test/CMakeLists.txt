cmake_minimum_required(VERSION 3.8)

find_package(GTest)

set(This qpyConsoleTests)

set(Sources
    qpyconsole_tests.cpp
)
add_executable(${This} ${Sources})

target_link_libraries(${This} PUBLIC
    GTest::Main
    lib-qpyconsole
)

add_test(
    NAME ${This}
    COMMAND ${This}
)

set(This qConsoleTests)

set(Sources
    qconsole_tests.cpp
)
add_executable(${This} ${Sources})

target_link_libraries(${This} PUBLIC
    GTest::Main
    lib-qconsole
)

add_test(
    NAME ${This}
    COMMAND ${This}
)
