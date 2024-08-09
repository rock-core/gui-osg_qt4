find_package(Qt4 COMPONENTS QtGui QtOpenGL)
find_package(Qt5 COMPONENTS Gui Widgets OpenGL)

if(Qt4_FOUND)
  QT4_WRAP_CPP( QT4_SOURCES_H_MOC QGraphicsViewAdapter OPTIONS "-f" )
  set(OSGQT_QT_VERSION 4)

  configure_file(Version.in Version)

  rock_library(osgQt
      USE_BINARY_DIR
      SOURCES GraphicsWindowQt.cpp
              QGraphicsViewAdapter.cpp
              QWidgetImage.cpp
              ${QT4_SOURCES_H_MOC}
      HEADERS Export
              GraphicsWindowQt
              QGraphicsViewAdapter
              QWebViewImage
              QWidgetImage
              ${CMAKE_CURRENT_BINARY_DIR}/Version
  )
  target_link_libraries(osgQt Qt4::QtGui Qt4::QtOpenGL)
  target_include_directories(osgQt PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/qt4)

  install(FILES ${CMAKE_CURRENT_BINARY_DIR}/osgQt.pc
          DESTINATION lib/pkgconfig
          RENAME openscenegraph-osgQt.pc)
endif()

if(Qt5_FOUND)
  qt5_wrap_cpp(QT5_SOURCES_MOC QGraphicsViewAdapter)
  set(OSGQT_QT_VERSION 5)

  configure_file(Version.in qt5/osgQt/Version)

  rock_library(osgQt5
      USE_BINARY_DIR
      SOURCES
          GraphicsWindowQt.cpp
  	QWidgetImage.cpp
  	QGraphicsViewAdapter.cpp
  	${QT5_SOURCES_MOC}
      HEADERS Export
              GraphicsWindowQt
              QGraphicsViewAdapter
              QWebViewImage
              QWidgetImage
              ${CMAKE_CURRENT_BINARY_DIR}/qt5/osgQt/Version
      DEPS
      	    Qt5::Gui
  	    Qt5::OpenGL
      NOINSTALL
  )
  target_include_directories(osgQt5 PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/qt5)

  install(TARGETS osgQt5
      LIBRARY DESTINATION lib
      ARCHIVE DESTINATION lib
      RUNTIME DESTINATION bin)

  install(FILES
          Export
          GraphicsWindowQt
          QGraphicsViewAdapter
          QWebViewImage
          QWidgetImage
          ${CMAKE_CURRENT_BINARY_DIR}/qt5/osgQt/Version
      DESTINATION include/osgQt5/osgQt/)

  install(FILES ${CMAKE_CURRENT_BINARY_DIR}/osgQt5.pc
          DESTINATION lib/pkgconfig
          RENAME openscenegraph-osgQt5.pc)
endif()

