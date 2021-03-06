ADD_EXECUTABLE(test_libhif_main hif-self-test.c)
TARGET_LINK_LIBRARIES(test_libhif_main
                      libhif
                      ${REPO_LIBRARY}
                      ${GLIB_LIBRARIES}
                      ${GLIB_GOBJECT_LIBRARIES}
                      ${GLIB_GIO_LIBRARIES}
                      ${GLIB_GIO_UNIX_LIBRARIES}
                      ${CHECK_LIBRARY}
                      ${SOLV_LIBRARY}
                      ${SOLVEXT_LIBRARY}
                      ${EXPAT_LIBRARY}
                      ${ZLIB_LIBRARY}
                      ${RPMDB_LIBRARY})

ADD_TEST(test_libhif_main test_libhif_main)
IF (NOT DISABLE_VALGRIND AND VALGRIND_PROGRAM)
    ADD_TEST(test_libhif_valgrind ${VALGRIND_PROGRAM} --error-exitcode=1 --leak-check=full
             --suppressions=${CMAKE_SOURCE_DIR}/tests/glib.supp
             --suppressions=${CMAKE_SOURCE_DIR}/tests/nss.supp
             --suppressions=${CMAKE_SOURCE_DIR}/tests/giovfs.supp
             --suppressions=${CMAKE_SOURCE_DIR}/tests/librepo.supp
             ${CMAKE_CURRENT_BINARY_DIR}/test_libhif_main)
ENDIF()
