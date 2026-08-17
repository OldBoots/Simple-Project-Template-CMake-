cmake_minimum_required(VERSION 3.10)

project(hello)

set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if(CMAKE_C_COMPILER_ID MATCHES "GNU|Clang")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
endif()

add_custom_target(clean-all
    COMMAND ${CMAKE_COMMAND} -E remove_directory ${CMAKE_BINARY_DIR}
    COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_BINARY_DIR}
    COMMENT "Clean build dir."
)

find_program(CLANG_FORMAT_EXECUTABLE clang-format)

if(CLANG_FORMAT_EXECUTABLE)
    set(CLANG_FORMAT_CONFIG ${CMAKE_CURRENT_SOURCE_DIR}/.clang-format)
    if(EXISTS ${CLANG_FORMAT_CONFIG})
        file(GLOB_RECURSE SRC_FILES 
            ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c
            ${CMAKE_CURRENT_SOURCE_DIR}/src/*.h
        )
        add_custom_target(fix-format
            COMMENT "Applynig clang-format."
            COMMAND ${CLANG_FORMAT_EXECUTABLE} -i ${SRC_FILES}
            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        )
        add_custom_target(build-format
            COMMENT "Formatting and building."
            COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --target fix-format
            COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --target all
        )
        add_custom_target(check-format
            COMMENT "Checking code style..."
            COMMAND ${CLANG_FORMAT_EXECUTABLE} --dry-run --Werror ${SRC_FILES}
            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        )
    else()
        message(WARNING "clang-format config not found at ${CLANG_FORMAT_CONFIG}")
    endif()
else()
    message(WARNING "clang-format not found. Formatting targets disabled.")
endif()

add_subdirectory(src)