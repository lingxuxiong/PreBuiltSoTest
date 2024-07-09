# the minimum version of CMake.
cmake_minimum_required(VERSION 3.4.1)
project(SoTest)

set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

set(LIB_CUPS mycups)

set(CUPS_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/third_party/cups/include)
set(CUPS_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/third_party/cups/libs/${OHOS_ARCH})
add_library(${LIB_CUPS} SHARED IMPORTED)
set_target_properties(${LIB_CUPS} PROPERTIES IMPORTED_LOCATION ${CUPS_LIBRARIES}/libcups.z.so)
message("CUPS_LIBRARIES:" + ${CUPS_LIBRARIES})

if(DEFINED PACKAGE_FIND_FILE)
    include(${PACKAGE_FIND_FILE})
endif()

include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include
                    ${CUPS_INCLUDE_DIRS}
)

add_library(entry SHARED hello.cpp)

target_link_libraries(entry PUBLIC libace_napi.z.so libhilog_ndk.z.so ${LIB_CUPS})