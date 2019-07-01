INCLUDE_DIRECTORIES(${FBX_INCLUDE_DIR})
set(OSG_PLUGINS osgPlugins-${OSG_VERSION})
set(TARGET_DEFAULT_PREFIX osgdb_)
set(COLLADA_USE_STATIC OFF)
set(DYNAMIC_OPENSCENEGRAPH TRUE)

SET(TARGET_SRC
    fbxRAnimation.cpp
    fbxRCamera.cpp
    fbxRLight.cpp
    fbxRMesh.cpp
    fbxRNode.cpp
    ReaderWriterFBX.cpp
    WriterCompareTriangle.cpp
    WriterNodeVisitor.cpp
    fbxMaterialToOsgStateSet.cpp
)

SET(TARGET_H
    fbxMaterialToOsgStateSet.h
    fbxReader.h
    ReaderWriterFBX.h
    WriterCompareTriangle.h
    WriterNodeVisitor.h
)

IF(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    REMOVE_CXX_FLAG(-pedantic)
    REMOVE_CXX_FLAG(-Wall)
    REMOVE_CXX_FLAG(-Wunused)
ENDIF()

IF(WIN32)
    SET(TARGET_EXTERNAL_LIBRARIES wininet)
ENDIF(WIN32)

IF(APPLE)
    FIND_LIBRARY(SYS_CONFIG_LIBRARY SystemConfiguration )
    MARK_AS_ADVANCED(SYS_CONFIG_LIBRARY)
    SET(TARGET_EXTERNAL_LIBRARIES iconv ${SYS_CONFIG_LIBRARY})
ENDIF(APPLE)

SET(TARGET_LIBRARIES_VARS FBX_LIBRARY)
SET(TARGET_ADDED_LIBRARIES osgAnimation)

#### end var setup  ###
SETUP_PLUGIN(fbx)
set_target_properties(${TARGET_TARGETNAME} PROPERTIES PREFIX "")
