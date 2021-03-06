project(Anime4KCPPCore LANGUAGES CXX)

aux_source_directory(src SOURCE)

include_directories(include)
file(GLOB INCLUDE include/*.hpp)

if(Built_In_Kernel)
    add_definitions(-DBUILT_IN_KERNEL)
endif()

if(Use_Legacy_OpenCL_API)
    add_definitions(-DLEGACY_OPENCL_API)
endif()

if(Enable_Fast_Math)
    add_definitions(-DENABLE_FAST_MATH)
endif()

if(Enable_NCNN)
    add_definitions(-DENABLE_NCNN)
endif()

if(Enable_OpenCV_DNN)
    add_definitions(-DENABLE_OPENCV_DNN)
endif()

if(Enable_Video)
    add_definitions(-DENABLE_VIDEO)
endif()

if(Enable_Preview_GUI)
    add_definitions(-DENABLE_PREVIEW_GUI)
endif()

if(Enable_Image_IO)
    add_definitions(-DENABLE_IMAGE_IO)
endif()

add_library(${PROJECT_NAME} SHARED ${INCLUDE} ${SOURCE})

include(${TOP_DIR}/cmake/ThirdPartyForCore.cmake)

install(
    TARGETS ${PROJECT_NAME} EXPORT Anime4KCPPCore
    ARCHIVE DESTINATION core/lib
    LIBRARY DESTINATION core/lib
    RUNTIME DESTINATION bin
)

install(
    FILES ${INCLUDE}
    DESTINATION core/include
)

install(EXPORT Anime4KCPPCore DESTINATION core/cmake)

configure_file(${TOP_DIR}/cmake/Anime4KCPPCoreConfig.cmake.in Anime4KCPPCoreConfig.cmake @ONLY)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Anime4KCPPCoreConfig.cmake DESTINATION core/cmake)
