FIND_PACKAGE(Feature)

SET( MYSQLPP_SOURCE_FILES
        beemutex.cpp
        cmdline.cpp
        connection.cpp
        cpool.cpp
        datetime.cpp
        dbdriver.cpp
        field_names.cpp
        field_types.cpp
        manip.cpp
        myset.cpp
        mysql++.cpp
        mystring.cpp
        null.cpp
        options.cpp
        qparms.cpp
        query.cpp
        result.cpp
        row.cpp
        scopedconnection.cpp
        sql_buffer.cpp
        sqlstream.cpp
        ssqls2.cpp
        stadapter.cpp
        tcp_connection.cpp
        transaction.cpp
        type_info.cpp
        uds_connection.cpp
        utility.cpp
        vallist.cpp
        wnp_connection.cpp
)

SET( MYSQLPP_HEADER_FILES
        autoflag.h
        beemutex.h
        cmdline.h
        common.h
        comparable.h
        connection.h
        cpool.h
        datetime.h
        dbdriver.h
        exceptions.h
        field.h
        field_names.h
        field_types.h
        insertpolicy.h
        manip.h
        myset.h
        mystring.h
        noexceptions.h
        null.h
        options.h
        qparms.h
        query.h
        refcounted.h
        result.h
        row.h
        scopedconnection.h
        sql_buffer.h
        sql_types.h
        sqlstream.h
        ssqls2.h
        stadapter.h
        stream2string.h
        tcp_connection.h
        tiny_int.h
        transaction.h
        type_info.h
        uds_connection.h
        utility.h
        vallist.h
        wnp_connection.h
        ${CMAKE_BINARY_DIR}/lib/mysql++.h
        querydef.h
)

IF( SHARED_BUILD )
    ADD_LIBRARY( mysqlpp SHARED ${MYSQLPP_HEADER_FILES} ${MYSQLPP_SOURCE_FILES} )
ENDIF()

IF( STATIC_BUILD )
    ADD_LIBRARY( mysqlpp STATIC ${MYSQLPP_HEADER_FILES} ${MYSQLPP_SOURCE_FILES} )
ENDIF()

TARGET_INCLUDE_DIRECTORIES( mysqlpp PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} PRIVATE ${CMAKE_BINARY_DIR}/lib/ )

IF(MYSQLPP_XCODE)
    SET_PROPERTY(TARGET mysqlpp APPEND PROPERTY COMPILE_OPTIONS -DMYSQLPP_XCODE)
ENDIF()

SET_TARGET_PROPERTIES(mysqlpp PROPERTIES PUBLIC_HEADER "${MYSQLPP_HEADER_FILES}")

TARGET_COMPILE_OPTIONS(mysqlpp PUBLIC ${COMPILE_OPTIONS})

configure_file(mysql++.h.in mysql++.h)

INSTALL( TARGETS mysqlpp
    LIBRARY DESTINATION lib
    PUBLIC_HEADER DESTINATION include/mysql++
)