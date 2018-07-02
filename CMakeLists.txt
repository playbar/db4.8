cmake_minimum_required(VERSION 3.6)
project(db4.8)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14" )

ADD_DEFINITIONS(-DHAVE_CONFIG_H)
ADD_DEFINITIONS(-DLEVELDB_PLATFORM_POSIX)
ADD_DEFINITIONS(-DOS_MACOSX)
#ADD_DEFINITIONS(-DUSE_DB4)


# db
set(DB_LIB_SRC
        btree/bt_compact.c
        btree/bt_compare.c
        btree/bt_compress.c
        btree/bt_conv.c
        btree/bt_curadj.c
        btree/bt_cursor.c
        btree/bt_delete.c
        btree/bt_method.c
        btree/bt_open.c
        btree/bt_put.c
        btree/bt_rec.c
        btree/bt_reclaim.c
        btree/bt_recno.c
        btree/bt_rsearch.c
        btree/bt_search.c
        btree/bt_split.c
        btree/bt_stat.c
        btree/bt_upgrade.c
        btree/bt_verify.c
        btree/btree_auto.c
        btree/btree_autop.c
        common/crypto_stub.c
        common/db_byteorder.c
        common/db_compint.c
        common/db_err.c
        common/db_getlong.c
        common/db_idspace.c
        common/db_log2.c
        common/db_shash.c
        common/dbt.c
        common/mkpath.c
        common/openflags.c
        common/os_method.c
        common/util_arg.c
        common/util_cache.c
        common/util_log.c
        common/util_sig.c
        common/zerofill.c
        db/crdel_auto.c
        db/crdel_autop.c
        db/crdel_rec.c
        db/db.c
        db/db_am.c
        db/db_auto.c
        db/db_autop.c
        db/db_cam.c
        db/db_cds.c
        db/db_conv.c
        db/db_dispatch.c
        db/db_dup.c
        db/db_iface.c
        db/db_join.c
        db/db_meta.c
        db/db_method.c
        db/db_open.c
        db/db_overflow.c
        db/db_ovfl_vrfy.c
        db/db_pr.c
        db/db_rec.c
        db/db_reclaim.c
        db/db_remove.c
        db/db_rename.c
        db/db_ret.c
        db/db_setid.c
        db/db_setlsn.c
        db/db_sort_multiple.c
        db/db_stati.c
        db/db_truncate.c
        db/db_upg.c
        db/db_upg_opd.c
        db/db_vrfy.c
        db/db_vrfy_stub.c
        db/db_vrfyutil.c
        db/partition.c
        dbreg/dbreg.c
        dbreg/dbreg_auto.c
        dbreg/dbreg_autop.c
        dbreg/dbreg_rec.c
        dbreg/dbreg_stat.c
        dbreg/dbreg_util.c
        env/env_alloc.c
        env/env_config.c
        env/env_failchk.c
        env/env_file.c
        env/env_globals.c
        env/env_method.c
        env/env_name.c
        env/env_open.c
        env/env_recover.c
        env/env_region.c
        env/env_register.c
        env/env_sig.c
        env/env_stat.c
        fileops/fileops_auto.c
        fileops/fileops_autop.c
        fileops/fop_basic.c
        fileops/fop_rec.c
        fileops/fop_util.c
        hash/hash.c
        hash/hash_auto.c
        hash/hash_conv.c
        hash/hash_dup.c
        hash/hash_func.c
        hash/hash_meta.c
        hash/hash_method.c
        hash/hash_open.c
        hash/hash_page.c
        hash/hash_rec.c
        hash/hash_reclaim.c
        hash/hash_stat.c
        hash/hash_upgrade.c
        hash/hash_verify.c
        hmac/hmac.c
        hmac/sha1.c
        lock/lock.c
        lock/lock_deadlock.c
        lock/lock_failchk.c
        lock/lock_id.c
        lock/lock_list.c
        lock/lock_method.c
        lock/lock_region.c
        lock/lock_stat.c
        lock/lock_stub.c
        lock/lock_timer.c
        lock/lock_util.c
        log/log.c
        log/log_archive.c
        log/log_compare.c
        log/log_debug.c
        log/log_get.c
        log/log_method.c
        log/log_put.c
        log/log_stat.c
        mp/mp_alloc.c
        mp/mp_bh.c
        mp/mp_fget.c
        mp/mp_fmethod.c
        mp/mp_fopen.c
        mp/mp_fput.c
        mp/mp_fset.c
        mp/mp_method.c
        mp/mp_mvcc.c
        mp/mp_region.c
        mp/mp_register.c
        mp/mp_resize.c
        mp/mp_stat.c
        mp/mp_sync.c
        mp/mp_trickle.c
        mutex/mut_alloc.c
        mutex/mut_failchk.c
        mutex/mut_fcntl.c
        mutex/mut_method.c
        mutex/mut_pthread.c
        mutex/mut_region.c
        mutex/mut_stat.c
        mutex/mut_stub.c
        mutex/mut_tas.c
        os/os_abort.c
        os/os_abs.c
        os/os_addrinfo.c
        os/os_alloc.c
        os/os_clock.c
        os/os_config.c
        os/os_cpu.c
        os/os_ctime.c
        os/os_dir.c
        os/os_errno.c
        os/os_fid.c
        os/os_flock.c
        os/os_fsync.c
        os/os_handle.c
        os/os_getenv.c
        os/os_map.c
        os/os_mkdir.c
        os/os_open.c
        os/os_pid.c
        os/os_rename.c
        os/os_root.c
        os/os_rpath.c
        os/os_rw.c
        os/os_seek.c
        os/os_stack.c
        os/os_stat.c
        os/os_tmpdir.c
        os/os_truncate.c
        os/os_uid.c
        os/os_unlink.c
        os/os_yield.c
        qam/qam.c
        qam/qam_auto.c
        qam/qam_autop.c
        qam/qam_conv.c
        qam/qam_files.c
        qam/qam_method.c
        qam/qam_open.c
        qam/qam_rec.c
        qam/qam_stat.c
        qam/qam_upgrade.c
        qam/qam_verify.c
        rep/rep_auto.c
        rep/rep_backup.c
        rep/rep_elect.c
        rep/rep_lease.c
        rep/rep_log.c
        rep/rep_method.c
        rep/rep_record.c
        rep/rep_region.c
        rep/rep_stat.c
        rep/rep_util.c
        rep/rep_verify.c
        repmgr/repmgr_auto.c
        repmgr/repmgr_elect.c
        repmgr/repmgr_method.c
        repmgr/repmgr_msg.c
        repmgr/repmgr_net.c
        repmgr/repmgr_posix.c
        repmgr/repmgr_queue.c
        repmgr/repmgr_sel.c
        repmgr/repmgr_stat.c
        repmgr/repmgr_util.c
        txn/txn.c
        txn/txn_auto.c
        txn/txn_autop.c
        txn/txn_chkpt.c
        txn/txn_failchk.c
        txn/txn_method.c
        txn/txn_rec.c
        txn/txn_recover.c
        txn/txn_region.c
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

