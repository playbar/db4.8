cmake_minimum_required(VERSION 3.6)
project(ddcode)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14" )

ADD_DEFINITIONS(-DHAVE_CONFIG_H)
ADD_DEFINITIONS(-DLEVELDB_PLATFORM_POSIX)
ADD_DEFINITIONS(-DOS_MACOSX)
#ADD_DEFINITIONS(-DUSE_DB4)


# db
set(DB_LIB_SRC
        btree/bt_compress.c
        common/db_err.c
        common/os_method.c
        db/db.c
        db/db_method.c
        env/env_method.c
        txn/txn.c
        txn/txn_auto.c
        txn/txn_chkpt.c
        txn/txn_method.c
        txn/txn_rec.c
        txn/txn_recover.c
        txn/txn_stat.c
        txn/txn_util.c
        )

add_library(db_lib ${DB_LIB_SRC})
target_include_directories(db_lib PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/
        ${CMAKE_CURRENT_SOURCE_DIR}/build_unix
        )

# db_cxx
set(DB_CXX_LIB_SRC
        #db_src/db/db.c
        cxx/cxx_dbc.cpp
        )

add_library(db_cxx_lib ${DB_CXX_LIB_SRC})
target_include_directories(db_cxx_lib PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/build_unix
        )



################

set(EXAMPLES_C_SRC
        examples_c/ex_env.c)

add_executable(examples_c ${EXAMPLES_C_SRC})
target_include_directories(examples_c PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/
        ${CMAKE_CURRENT_SOURCE_DIR}/build_unix
        )
target_link_libraries(examples_c
        db_lib
        )

################

set(EXAMPLES_CXX_SRC
        examples_cxx/EnvExample.cpp)

add_executable(examples_cxx ${EXAMPLES_CXX_SRC})
target_include_directories(examples_cxx PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/
        ${CMAKE_CURRENT_SOURCE_DIR}/build_unix
        )
target_link_libraries(examples_cxx
        db_cxx_lib
        )

################

