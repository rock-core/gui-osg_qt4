QT4_WRAP_CPP( SOURCES_H_MOC ${SOURCES_H} OPTIONS "-f" )
set(OSGQT_QT_VERSION 4)

configure_file(Version.in Version)

rock_library(osgQt
    USE_BINARY_DIR
    SOURCES GraphicsWindowQt.cpp
            QGraphicsViewAdapter.cpp
            QWidgetImage.cpp
    HEADERS Export
            GraphicsWindowQt
            QGraphicsViewAdapter
            QWebViewImage
            QWidgetImage
            ${CMAKE_CURRENT_BINARY_DIR}/Version
)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/osgQt.pc
        DESTINATION lib/pkgconfig
        RENAME openscenegraph-osgQt.pc)
