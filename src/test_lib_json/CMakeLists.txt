# vim: et ts=4 sts=4 sw=4 tw=0

add_executable(jsoncpp_test
    jsontest.cpp
    jsontest.h
    fuzz.cpp
    fuzz.h
    main.cpp
)


if(BUILD_SHARED_LIBS)
    add_compile_definitions( JSON_DLL )
    target_link_libraries(jsoncpp_test jsoncpp_lib)
else()
    target_link_libraries(jsoncpp_test jsoncpp_static)
endif()

# another way to solve issue #90
#set_target_properties(jsoncpp_test PROPERTIES COMPILE_FLAGS -ffloat-store)

# Run unit tests in post-build
# (default cmake workflow hides away the test result into a file, resulting in poor dev workflow?!?)
if(JSONCPP_WITH_POST_BUILD_UNITTEST)
    add_custom_command(TARGET jsoncpp_test
        POST_BUILD
        COMMAND ${CMAKE_CROSSCOMPILING_EMULATOR} $<TARGET_FILE:jsoncpp_test>
    )
endif()
