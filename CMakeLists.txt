cmake_minimum_required(VERSION 3.25.1)

# Set project name and version.
set(PROJECT_NAME "PluginTemplate")
file(STRINGS VERSION CURRENT_VERSION)
project(${PROJECT_NAME} VERSION ${CURRENT_VERSION})

set(JUCE_DIR "${CMAKE_BINARY_DIR}/dependencies/JUCE")


# Install JUCE framework

if(NOT EXISTS ${JUCE_DIR})
    execute_process(
        COMMAND git clone https://github.com/juce-framework/JUCE.git ${JUCE_DIR}
        RESULT_VARIABLE result
        OUTPUT_VARIABLE output
    )

    if(result)
        message(FATAL_ERROR "Failed to clone JUCE: ${output}")
    endif()
endif()


# Include dependencies

add_subdirectory(${JUCE_DIR})

add_definitions(-DDONT_SET_USING_JUCE_NAMESPACE)

add_subdirectory(Source)
