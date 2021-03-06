
# CMAKE_BINARY_DIR

find_package(Boost)
find_package(Boost COMPONENTS unit_test_framework timer system)

add_custom_target(check COMMAND ${CMAKE_CTEST_COMMAND})
add_custom_target(tests)

include_directories(${Boost_INCLUDE_DIR})

if (CI_BUILD)
    file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/test/reports)
    file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/test/valgrind_reports)
    
    add_custom_target(gcovr COMMAND gcovr --xml -e "/usr*" -e "${CMAKE_SOURCE_DIR}/test/*.cpp" -o test/coverage.xml WORKING_DIRECTORY ${CMAKE_BINARY_DIR})
    add_dependencies(gcovr check)
endif()

function(add_boost_test name)
  #add_executable(${name} EXCLUDE_FROM_ALL ${ARGN})
  add_executable(${name} ${ARGN})
  target_link_libraries(${name} ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
                                ${Boost_TIMER_LIBRARY}
                                ${Boost_SYSTEM_LIBRARY})
  
  if (CI_BUILD)
    add_test(${name} ./${name} --output_format=xml --log_level=all --report_level=no --log_sink=${CMAKE_BINARY_DIR}/test/reports/${name}.xml)
  else()
    add_test(${name} ./${name})
  endif()
  
  add_dependencies(check ${name})
  add_dependencies(tests ${name})
endfunction()

