cmake_minimum_required(VERSION 3.12.2)

project(CLion)

set(CMAKE_CONFIGURATION_TYPES "Debug;Release"
        CACHE STRING "Configuration types" FORCE)

add_executable(CLion
        forward.cpp
        forward.h
        main.cpp
        )
# Additional include directories
set_property(TARGET CLion
        APPEND PROPERTY INCLUDE_DIRECTORIES
        $<$<CONFIG:Debug>:
        "C:/Program Files/MobileRobots/Aria/lib64";
        "C:/Program Files/MobileRobots/Aria/bin64";
        "C:/Program Files/MobileRobots/Aria/include";
        "C:/Program Files/MobileRobots/Aria">
        $<$<CONFIG:Release>:
        "C:/Program Files/MobileRobots/Aria/lib64";
        "C:/Program Files/MobileRobots/Aria/bin64";
        "C:/Program Files/MobileRobots/Aria/include";
        "C:/Program Files/MobileRobots/Aria">
        )

# Preprocessor definitions
target_compile_definitions(CLion PRIVATE
        $<$<CONFIG:Debug>:_MBCS;>
        $<$<CONFIG:Release>:_MBCS;>
        )

#[[# SDL check
target_compile_options(CLion PRIVATE
        "$<$<CONFIG:Debug>:/sdl>"
        "$<$<CONFIG:Release>:/sdl>"
        )]]

# Minimal rebuild
if (MSVC)
    target_compile_options(CLion PRIVATE
            "$<$<CONFIG:Debug>:/Gm->"
            "$<$<CONFIG:Release>:/Gm->"
            )
endif ()

# Precompiled header files
if (MSVC)
    target_compile_options(CLion PRIVATE
            ""
            )
endif ()

# Additional library directories
if (MSVC)
    target_link_options(CLion PRIVATE
            $<$<CONFIG:Debug>:
            /LIBPATH:"C:/Program Files/MobileRobots/Aria/lib64">
            $<$<CONFIG:Release>:
            /LIBPATH:"C:/Program Files/MobileRobots/Aria/lib64">
            )
else ()
    target_link_options(CLion PRIVATE
            $<$<CONFIG:Debug>:
            -L"C:/Program Files/MobileRobots/Aria/lib64">
            $<$<CONFIG:Release>:
            -L"C:/Program Files/MobileRobots/Aria/lib64">
            )
endif ()

# Link libraries
set_property(TARGET CLion
        APPEND PROPERTY LINK_LIBRARIES
        "$<$<CONFIG:Debug>:AriaDebugVC14.lib>"
        "$<$<CONFIG:Release>:AriaDebugVC14.lib>"
        )





#[[cmake_minimum_required(VERSION 3.14)
project(CLion)

set(CMAKE_CXX_STANDARD 14)

add_executable(CLion main.cpp)]]

#[[target_link_libraries(C:/Program Files/MobileRobots/Aria)
target_link_libraries(C:/Program Files/MobileRobots/Aria/include)
target_link_libraries(C:/Program Files/MobileRobots/Aria/bin64)
target_link_libraries(C:/Program Files/MobileRobots/Aria/lib64)]]


