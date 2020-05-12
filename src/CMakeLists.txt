find_package(Qt4 REQUIRED QtGui QtOpenGL)
QT4_WRAP_CPP( SOURCES_H_MOC QGraphicsViewAdapter OPTIONS "-f" )
set(OSGQT_QT_VERSION 4)

configure_file(Version.in Version)

rock_library(osgQt
    USE_BINARY_DIR
    SOURCES GraphicsWindowQt.cpp
            QGraphicsViewAdapter.cpp
            QWidgetImage.cpp
            ${SOURCES_H_MOC}
    HEADERS Export
            GraphicsWindowQt
            QGraphicsViewAdapter
            QWebViewImage
            QWidgetImage
            ${CMAKE_CURRENT_BINARY_DIR}/Version
)
target_link_libraries(osgQt Qt4::QtGui Qt4::QtOpenGL)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/osgQt.pc
        DESTINATION lib/pkgconfig
        RENAME openscenegraph-osgQt.pc)
