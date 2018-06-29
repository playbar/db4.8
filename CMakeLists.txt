cmake_minimum_required(VERSION 3.6)
project(ddcode)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14" )

ADD_DEFINITIONS(-DHAVE_CONFIG_H)
ADD_DEFINITIONS(-DLEVELDB_PLATFORM_POSIX)
ADD_DEFINITIONS(-DOS_MACOSX)
#ADD_DEFINITIONS(-DUSE_DB4)


# db
set(DB_LIB_SRC
        db/db.c
        )

add_library(db_lib ${DB_LIB_SRC})
target_include_directories(db_lib PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/db_src
        ${CMAKE_CURRENT_SOURCE_DIR}/db_src/build_unix
        )

# db_cxx
set(DB_CXX_LIB_SRC
        #db_src/db/db.c
        cxx/cxx_dbc.cpp
        )

add_library(db_cxx_lib ${DB_CXX_LIB_SRC})
target_include_directories(db_cxx_lib PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/db_src
        ${CMAKE_CURRENT_SOURCE_DIR}/db_src/build_unix
        )



################

set(EXAMPLES_C_SRC
        examples_c/ex_env.c)

add_executable(examples_c ${EXAMPLES_C_SRC})
target_include_directories(examples_c PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src
        ${CMAKE_CURRENT_SOURCE_DIR}/src/univalue/include
        )
target_link_libraries(examples_c
        db_lib
        )

################


