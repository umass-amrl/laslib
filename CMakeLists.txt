PROJECT(laserlib)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

MESSAGE(STATUS "Compiling LASlib")
MESSAGE(STATUS "Using compiler: ${CMAKE_CXX_COMPILER}")
MESSAGE(STATUS "Build Type: ${CMAKE_BUILD_TYPE}")
MESSAGE(STATUS "Arch: ${CMAKE_SYSTEM_PROCESSOR}")

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

IF(${CMAKE_BUILD_TYPE} MATCHES "Release")
  MESSAGE(STATUS "Additional Flags for Release mode")
  SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -march=native -fopenmp -O3 -DNDEBUG")
ELSEIF(${CMAKE_BUILD_TYPE} MATCHES "Debug")
  MESSAGE(STATUS "Additional Flags for Debug mode")
  SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -g")
ENDIF()

IF (!MSVC)
  ADD_COMPILE_OPTIONS(-Wno-deprecated
                      -Wno-write-strings
                      -Wno-unused-result
                      -std=c++11)
ENDIF()
ADD_DEFINITIONS(-DNDEBUG -DUNORDERED -DHAVE_UNORDERED_MAP)

INCLUDE_DIRECTORIES(src/laszip src/laslib)

SET(LAS_SRC
    src/laslib/lasreader.cpp
    src/laslib/laswriter.cpp
    src/laslib/lasreader_las.cpp
    src/laslib/lasreader_bin.cpp
    src/laslib/lasreader_shp.cpp
    src/laslib/lasreader_asc.cpp
    src/laslib/lasreader_bil.cpp
    src/laslib/lasreader_dtm.cpp
    src/laslib/lasreader_ply.cpp
    src/laslib/lasreader_qfit.cpp
    src/laslib/lasreader_txt.cpp
    src/laslib/lasreadermerged.cpp
    src/laslib/lasreaderbuffered.cpp
    src/laslib/lasreaderstored.cpp
    src/laslib/lasreaderpipeon.cpp
    src/laslib/laswriter_las.cpp
    src/laslib/laswriter_bin.cpp
    src/laslib/laswriter_qfit.cpp
    src/laslib/laswriter_wrl.cpp
    src/laslib/laswriter_txt.cpp
    src/laslib/laswritercompatible.cpp
    src/laslib/laswaveform13reader.cpp
    src/laslib/laswaveform13writer.cpp
    src/laslib/lasutility.cpp
    src/laslib/lasfilter.cpp
    src/laslib/lastransform.cpp
    src/laslib/fopen_compressed.cpp
)

SET(LAZ_SRC
    src/laszip/laszip.cpp
    src/laszip/lasreadpoint.cpp
    src/laszip/lasreaditemcompressed_v1.cpp
    src/laszip/lasreaditemcompressed_v2.cpp
    src/laszip/lasreaditemcompressed_v3.cpp
    src/laszip/lasreaditemcompressed_v4.cpp
    src/laszip/laswritepoint.cpp
    src/laszip/laswriteitemcompressed_v1.cpp
    src/laszip/laswriteitemcompressed_v2.cpp
    src/laszip/laswriteitemcompressed_v3.cpp
    src/laszip/laswriteitemcompressed_v4.cpp
    src/laszip/integercompressor.cpp
    src/laszip/arithmeticdecoder.cpp
    src/laszip/arithmeticencoder.cpp
    src/laszip/arithmeticmodel.cpp
    src/laszip/lasindex.cpp
    src/laszip/lasquadtree.cpp
    src/laszip/lasinterval.cpp
)


ADD_LIBRARY(LASlib ${LAS_SRC} ${LAZ_SRC})

ADD_SUBDIRECTORY(src/examples)
