
configure_file(version.h.in ${CMAKE_CURRENT_BINARY_DIR}/version.h)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(NEOVIM_QT_SOURCES util.cpp neovimconnector.cpp neovimconnectorhelper.cpp function.cpp msgpackrequest.cpp msgpackiodevice.cpp auto/neovimapi0.cpp auto/neovimapi1.cpp auto/neovimapi2.cpp auto/neovimapi3.cpp auto/neovimapi4.cpp auto/neovimapi6.cpp)
if(WIN32)
  list(APPEND NEOVIM_QT_SOURCES stdinreader.cpp)
endif()

add_library(neovim-qt STATIC ${NEOVIM_QT_SOURCES})

if(X11_FOUND)
    set(X11_LIBRARIES X11)
    add_definitions(-DWITH_X11)
endif()

target_link_libraries(neovim-qt ${X11_LIBRARIES} Qt5::Network ${MSGPACK_LIBRARIES})

add_subdirectory(gui)
