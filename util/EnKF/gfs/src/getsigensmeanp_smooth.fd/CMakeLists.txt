cmake_minimum_required(VERSION 2.6)
if(BUILD_UTIL)
  
  set(LOCAL_Fortran_FLAGS "-O3 -fp-model source -convert big_endian -assume byterecl -implicitnone  ${OpenMP_Fortran_FLAGS}" )
  file(GLOB LOCAL_SRC ${CMAKE_CURRENT_SOURCE_DIR}/*.f90)
  set_source_files_properties( ${LOCAL_SRC} PROPERTIES COMPILE_FLAGS ${LOCAL_Fortran_FLAGS} )
  add_executable(getsigensmeanp_smooth.x  ${LOCAL_SRC} )
  set_target_properties( getsigensmeanp_smooth.x PROPERTIES COMPILE_FLAGS ${LOCAL_Fortran_FLAGS} )
  SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_Fortran_FLAGS}" )
  include_directories( ${NEMSIOINC} ${SIGIOINC} ${NETCDF_INCLUDE_DIRS}  ${FV3GFS_NCIO_INCS}) 
  target_link_libraries( getsigensmeanp_smooth.x ${FV3GFS_NCIO_LIBRARIES} ${BACIO_LIBRARY} ${NEMSIO_LIBRARY} ${BACIO_LIBRARY} ${SIGIO_LIBRARY} ${W3NCO_4_LIBRARY} ${SP_4_LIBRARY} ${MPI_Fortran_LIBRARIES} ${NETCDF_Fortran_LIBRARIES} ${NETCDF_C_LIBRARIES})

endif()
