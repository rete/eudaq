# build EUDAQ python exe bindings
option(BUILD_python "Compile Python EUDAQ binding library?" OFF)
IF(BUILD_python)

  FIND_PACKAGE(PythonLibsNew)
  IF(PYTHONLIBS_FOUND)
  MESSAGE(STATUS "Found PythonLibsNew") 
  MESSAGE(STATUS "PYTHON_PREFIX: ${PYTHON_PREFIX}")
  MESSAGE(STATUS "PYTHON_LIBRARIES: ${PYTHON_LIBRARIES}")
  MESSAGE(STATUS "PYTHON_INCLUDE_DIRS: ${PYTHON_INCLUDE_DIRS}")
  MESSAGE(STATUS "PYTHON_SITE_PACKAGES: ${PYTHON_SITE_PACKAGES}")
  MESSAGE(STATUS "PYTHON_IS_DEBUG : ${PYTHON_IS_DEBUG}")
  MESSAGE(STATUS "PYTHON_INCLUDE_PATH: ${PYTHON_INCLUDE_PATH}")

  #INCLUDE_DIRECTORIES(${PYTHON_INCLUDE_DIRS})
  #ADD_LIBRARY( PyIndexReader SHARED 
  #   src/PyIndexReader.cpp
  #)
  #target_link_libraries(PyIndexReader ${EUDAQ_CORE_LIBRARY} ${EUDAQ_THREADS_LIB})
  #ADD_LIBRARY( PyAidaFileReader SHARED 
  #   src/PyAidaFileReader.cpp
  #)
  #target_link_libraries(PyAidaFileReader ${EUDAQ_CORE_LIBRARY} ${EUDAQ_THREADS_LIB})
    
  #INSTALL(TARGETS PyAidaFileReader PyIndexReader
  #   RUNTIME DESTINATION bin
  #   LIBRARY DESTINATION lib
  #   ARCHIVE DESTINATION lib
  #)
    
  ENDIF(PYTHONLIBS_FOUND)

  ADD_LIBRARY( PyEUDAQ SHARED 
    src/PyRunControl.cpp 
    src/PyProducer.cpp
    # src/PyDataCollector.cpp
    src/PyLogCollector.cpp
    )

  target_link_libraries(PyEUDAQ  ${EUDAQ_CORE_LIBRARY} ${EUDAQ_THREADS_LIB})

  INSTALL(TARGETS PyEUDAQ 
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)

ENDIF(BUILD_python)
