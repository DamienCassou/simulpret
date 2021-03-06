# More information on building QT project with CMake at http://qt-project.org/quarterly/view/using_cmake_to_build_qt_projects

PROJECT(simulpret)
FIND_PACKAGE(Qt4 REQUIRED)
cmake_minimum_required(VERSION 2.8)

SET(SIMULPRET_SOURCES 
    src/db.cpp
    src/evenement.cpp
    src/main.cpp
    src/pret.cpp
    src/ui/currencydelegate.cpp
    src/ui/evenementdialog.cpp
    src/ui/mainwindow.cpp)
SET(SIMULPRET_HEADERS
    src/db.h
    src/evenement.h
    src/pret.h
    src/ui/currencydelegate.h
    src/ui/evenementdialog.h
    src/ui/mainwindow.h)
SET(SIMULPRET_FORMS
    src/ui/evenementdialog.ui
    src/ui/mainwindow.ui)
SET(SIMULPRET_RESOURCES
    resources/simulpret-resources.qrc)

QT4_WRAP_CPP(SIMULPRET_HEADERS_MOC ${SIMULPRET_HEADERS})
QT4_WRAP_UI(SIMULPRET_FORMS_HEADERS ${SIMULPRET_FORMS})
QT4_ADD_RESOURCES(SIMULPRET_RESOURCES_RCC ${SIMULPRET_RESOURCES})

INCLUDE(${QT_USE_FILE})
ADD_DEFINITIONS(${QT_DEFINITIONS})

# Add build dir to include headre file generated by uic
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR} ${QT_QTSQL_INCLUDE_DIR})

SET(QT_USE_QTSQL TRUE)
# SET(QT_USE_QTTEST TRUE)

ADD_EXECUTABLE(simulpret ${SIMULPRET_SOURCES} ${SIMULPRET_HEADERS_MOC} ${SIMULPRET_FORMS_HEADERS} ${SIMULPRET_RESOURCES_RCC})
TARGET_LINK_LIBRARIES(simulpret ${QT_LIBRARIES} ${QT_QTSQL_LIBRARIES})