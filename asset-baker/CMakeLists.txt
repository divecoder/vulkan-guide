set(CMAKE_CXX_STANDARD 17)
# CUDA
FIND_PACKAGE(CUDA)
IF(CUDA_FOUND)
    IF(MINGW)
        MESSAGE(STATUS "Looking for CUDA - not supported on MinGW")
        UNSET(CUDA_FOUND)
    ENDIF(MINGW)
    IF(CUDA_FOUND)
        SET(HAVE_CUDA ${CUDA_FOUND} CACHE BOOL "Set to TRUE if CUDA is found, FALSE otherwise")
        MESSAGE(STATUS "Looking for CUDA - found")
    ENDIF(CUDA_FOUND)
ELSE(CUDA_FOUND)
    MESSAGE(STATUS "Looking for CUDA - not found")
ENDIF(CUDA_FOUND)
# Add source to this project's executable.
add_executable (baker
"asset_main.cpp")

set_property(TARGET baker PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:extra>")

target_include_directories(baker PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

target_link_libraries(baker PUBLIC tinyobjloader stb_image json lz4 assetlib tinyGLTF nvtt glm assimp ${CUDA_LIBRARIES})

