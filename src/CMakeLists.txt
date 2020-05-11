rock_library(osg_qt4
    SOURCES Dummy.cpp
    HEADERS Dummy.hpp)

rock_executable(osg_qt4_bin Main.cpp
    DEPS osg_qt4)

