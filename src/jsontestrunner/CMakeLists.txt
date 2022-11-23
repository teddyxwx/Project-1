# The new Python3 module is much more robust than the previous PythonInterp
find_package(Python3 COMPONENTS Interpreter)
# Set variables for backwards compatibility with cmake < 3.12.0
set(PYTHONINTERP_FOUND ${Python3_Interpreter_FOUND})
set(PYTHON_EXECUTABLE ${Python3_EXECUTABLE})

add_executable(jsontestrunner_exe
    main.cpp
)

if(BUILD_SHARED_LIBS)
    add_compile_definitions( JSON_DLL )
    target_link_libraries(jsontestrunner_exe jsoncpp_lib)
else()
    target_link_libraries(jsontestrunner_exe jsoncpp_static)
endif()

set_target_properties(jsontestrunner_exe PROPERTIES OUTPUT_NAME jsontestrunner_exe)

if(PYTHONINTERP_FOUND)
    # Run end to end parser/writer tests
    set(TEST_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../test)
    set(RUNJSONTESTS_PATH ${TEST_DIR}/runjsontests.py)

    # Run unit tests in post-build
    # (default cmake workflow hides away the test result into a file, resulting in poor dev workflow?!?)
    add_custom_target(jsoncpp_readerwriter_tests
        "${PYTHON_EXECUTABLE}" -B "${RUNJSONTESTS_PATH}" $<TARGET_FILE:jsontestrunner_exe> "${TEST_DIR}/data"
        DEPENDS jsontestrunner_exe jsoncpp_test
    )
    add_custom_target(jsoncpp_check DEPENDS jsoncpp_readerwriter_tests)
endif()
