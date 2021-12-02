set(OSGQT_QT_VERSION 5)
rock_find_qt5(Gui OpenGL)
qt5_wrap_cpp(SOURCES_MOC QGraphicsViewAdapter)

configure_file(Version.in Version)

rock_library(osgQt
    USE_BINARY_DIR
    SOURCES
        GraphicsWindowQt.cpp
	QWidgetImage.cpp
	QGraphicsViewAdapter.cpp
	${SOURCES_MOC}
    HEADERS Export
            GraphicsWindowQt
	    QGraphicsViewAdapter
	    QWebViewImage
            QWidgetImage
            ${CMAKE_CURRENT_BINARY_DIR}/Version
    DEPS
    	    Qt5::Gui
	    Qt5::OpenGL
)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/osgQt.pc
        DESTINATION lib/pkgconfig
        RENAME openscenegraph-osgQt.pc)
