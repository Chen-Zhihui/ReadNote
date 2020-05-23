# find qt5

```cmake
set(Qt5_DIR "C:/Qt/Qt5.12.8/5.12.8/msvc2017_64/lib/cmake/Qt5")
find_package(Qt5 "${QT_MIN_VERSION}"
    CONFIG REQUIRED
    COMPONENTS
        Core
        Gui
        Svg
        Qml
        Quick
        QuickControls2
        QuickTest
)

message(STATUS ${_qt5_install_prefix}/../../bin/windeployqt.exe)
add_custom_command(
    TARGET FluidDemo POST_BUILD
    COMMAND ${_qt5_install_prefix}/../../bin/windeployqt.exe --compiler-runtime --dir ${CMAKE_BINARY_DIR}/bin $<TARGET_FILE:FluidDemo>
)
```

# find exe with qt5

## find qmake

``` cmake
    # Find qmlplugindump
    get_target_property(QMake_EXECUTABLE Qt5::qmake LOCATION)
    get_filename_component(_qmake_path ${QMake_EXECUTABLE} DIRECTORY)
    find_program(QmlPluginDump_EXECUTABLE
        NAMES
            qmlplugindump-qt5
            qmlplugindump
        PATHS
            "${_qmake_path}"
        NO_DEFAULT_PATH
    )
```