IF (NOT G2O_USE_CHOLMOD)
  RETURN()
ENDIF()

ADD_LIBRARY(solver_cholmod ${G2O_LIB_TYPE}
  solver_cholmod.cpp
  linear_solver_cholmod.h
)

INCLUDE_DIRECTORIES(${CHOLMOD_INCLUDE_DIR})

SET_TARGET_PROPERTIES(solver_cholmod PROPERTIES OUTPUT_NAME ${LIB_PREFIX}solver_cholmod)

ADD_DEFINITIONS(${BLAS_DEFINITIONS} ${LAPACK_DEFINITIONS})
TARGET_LINK_LIBRARIES(solver_cholmod ${CHOLMOD_LIBRARIES} ${BLAS_LIBRARIES} ${LAPACK_LIBRARIES} core)

INSTALL(TARGETS solver_cholmod
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)

FILE(GLOB headers "${CMAKE_CURRENT_SOURCE_DIR}/*.h" "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp")

INSTALL(FILES ${headers} DESTINATION include/g2o/solvers/cholmod)
