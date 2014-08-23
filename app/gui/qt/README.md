# OS X

## Dev Build

* Download Qt 5.3.1+ http://qt-project.org/downloads
* Run the setup wizard and install to a known location which we'll call /path/to/qt
* Grab a copy of the QScintilla libs http://www.riverbankcomputing.co.uk/software/qscintilla/download and untar into a known location which we'll call /path/to/qscintilla
* Build QScintilla:
  - cd /path/to/qscintilla/Qt4Qt5 
  - generate makefile: /path/to/qt/5.3/clang_64/bin/qmake qscintilla.pro
  - make
* Open Project in Qt Creator
  - Open Qt Creator
  - Menu -> File -> Open File or Project -> /path/to/sonic-pi/app/gui/qt/SonicPi.pro
* Change where build output is
  - Projects tab -> Build Directory - change to known location which we'll call /path/to/app
* Add this to SonicPi.pro
    LIBS += -L /path/to/qscintilla/Qt4Qt5/ -lqscintilla2
    INCLUDEPATH += /path/to/qscintilla/Qt4Qt5/
    DEPENDPATH += /path/to/qscintilla/Qt4Qt5/
* Build project - should see app dir structure in /path/to/app
* Copy all dylibs to new app dir: 
  - cp /path/to/qscintilla/Qt4Qt5/*.dylib /path/to/app/Sonic-Pi.app/Contents/MacOS/
* Copy this as a Info.plist into the root of Sonic-Pi.app:
  
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
            <key>NSPrincipalClass</key>
            <string>NSApplication</string>
            <key>NSHighResolutionCapable</key>
            <string>True</string>
            <key>CFBundleIconFile</key>
            <string>app.icns</string>
            <key>CFBundlePackageType</key>
            <string>APPL</string>
            <key>CFBundleGetInfoString</key>
            <string>Created by Qt/QMake</string>
            <key>CFBundleSignature</key>
            <string>????</string>
            <key>CFBundleExecutable</key>
            <string>Sonic Pi</string>
            <key>CFBundleIdentifier</key>
            <string>com.yourcompany.Sonic Pi</string>
            <key>NOTE</key>
            <string>This file was generated by Qt/QMake.</string>
    </dict>
    </plist>

## Final Build

* Move qscintilla libs from MacOS dir to Packages dir
* Statically link in Qt framework : 
  - ~/Development/Qt/5.3/clang_64/bin/macdeployqt ~/Development/apps/sonic-pi/Sonic-Pi.app
  
  