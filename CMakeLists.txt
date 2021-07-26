# CMake for idprom decode
# by tsihang (tsihang@asterfuion.com)
# 26 July 2021

cmake_minimum_required(VERSION 3.5)


set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
set(CMAKE_C_FLAGS "-g -O3 -Wall -Wextra -MMD -MF --std=gnu99")
#set(CMAKE_C_FLAGS "-g -O3 -Wextra -MMD -MF --std=gnu99")

project(sff)

set(SOURCES
    main.c
)


# Basic packages
aux_source_directory(sm/infra/modules/AIM/module/src aim)
aux_source_directory(sm/infra/modules/AIM/module/src/posix aim_posix)
aux_source_directory(sm/bigcode/modules/IOF/module/src iof)
aux_source_directory(sm/bigcode/modules/cjson/module/src cjson)
aux_source_directory(sm/bigcode/modules/cjson_util/module/src cjson_util)
aux_source_directory(sm/bigcode/modules/sff/module/src sff)
aux_source_directory(sm/bigcode/modules/OS/module/src os)
aux_source_directory(sm/bigcode/modules/timer_wheel/module/src timer_wheel)

aux_source_directory(sm/bigcode/modules/BigData/BigHash/module/src bighash)
aux_source_directory(sm/bigcode/modules/BigData/BigList/module/src biglist)
aux_source_directory(sm/bigcode/modules/BigData/BigRing/module/src bigring)

# sff packages

add_executable(sff
    ${SOURCES}
    ${aim}
    ${aim_posix}
    ${iof}
    ${cjson}
    ${cjson_util}
    ${sff}
    ${os}
    ${timer_wheel}
    ${bighash}
    ${biglist}
    ${bigring})

target_link_libraries(sff -lpthread -lm)

target_include_directories(sff PRIVATE 
	${PROJECT_SOURCE_DIR}
	${PROJECT_SOURCE_DIR}/sm/infra/modules/AIM/module/inc
	${PROJECT_SOURCE_DIR}/sm/infra/modules/AIM/module/inc/AIM
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/IOF/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/cjson/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/cjson_util/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/sff/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/timer_wheel/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/OS/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/timer_wheel/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/BigData/BigHash/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/BigData/BigList/module/inc
	${PROJECT_SOURCE_DIR}/sm/bigcode/modules/BigData/BigRing/module/inc

)

