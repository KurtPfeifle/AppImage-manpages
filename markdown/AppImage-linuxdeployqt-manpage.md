% LINUXDEPLOYQT(1) | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-linuxdeployqt-manpage.md -o AppImage-linuxdeployqt.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-linuxdeployqt-manpage.md -o AppImage-linuxdeployqt.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-linuxdeployqt-manpage.md -o AppImage-linuxdeployqt.html -s -f markdown -t html
    pandoc AppImage-linuxdeployqt-manpage.md -o AppImage-linuxdeployqt.epub -s -f markdown -t epub3

-->

<!-- 
 linuxdeployqt (which despite its Qt focus is useful as a general purpose library gatherer / bundler,
-->




# Name

**`linuxdeployqt`** -- take an application as input and make it self-contained by copying in the Qt libraries and plugins which the application uses.


# Synopsis

`linuxdeployqt`  *<app-binary|desktop file>*  *[options]*


# Description

`linuxdeployqt` is a command line tool which prepares an application to run from an AppDir (see *`AppImage-Appdir(7)`*)

Optionally from this bundle you can generate an AppImage, or with the help of [fpm](https://github.com/probonopd/linuxdeployqt/issues/9), into cross-distro DEB and RPM packages.

Despite its Qt focus, linuxdeployqt is useful as a general purpose library gatherer and bundler.
The tool as well as its name is inspired by two other tools named `windowsdeployqt` and `macdeployqt`.


# Options

`-verbose=<0-3>`
:   0 = no output,

    1 = error/warning (default),

    2 = normal,

    3 = debug

`-no-plugins`
:   Skip plugin deployment

`-appimage`
:   Create an AppImage (implies `-bundle-non-qt-libs`)

`-no-strip`
:   Don't run 'strip' on the binaries

`-bundle-non-qt-libs`
:   Also bundle non-core, non-Qt libraries

`-executable=<path>`
:   Let the given executable use the deployed libraries too

`-qmldir=<path>`
:   Scan for QML imports in the given path

`-always-overwrite`
:   Copy files even if the target file exists

`-qmake=<path>`
:   The qmake executable to use

`-no-translations`
:   Skip deployment of translations.


## Differences to `macdeployqt`

`linuxdeployqt` is conceptually based on Qt's [Mac Deployment Tool](http://doc.qt.io/qt-5/osx-deployment.html), `macdeployqt`.
`macdeployqt` lives in the set of tools applications of the Qt Toolkit.
`linuxdeployqt` however has been changed to a slightly different logic and to other tools needed for Linux:

* Instead of an `.app` bundle for macOS, this produces an [AppDir](http://rox.sourceforge.net/desktop/AppDirs.html) for Linux (see also `AppImage-AppDir(7)`).
* Instead of a `.dmg` disk image for macOS, this produces an [AppImage](http://appimage.org/) for Linux.
  An AppImage is quite similar to a .dmg but it directly executes the contained application rather than just opening a window on the desktop from where the application can be launched with an extra action.


# Main Features

By default `linuxdeployqt` deploys the same Qt instance which qmake on the `$PATH` points to.
The '-qmake' option can be used to point to the qmake executable to be used instead.

Plugins related to a Qt library are copied in with the library.

See the "Deploying Applications on Linux" topic in the AppImageKit Wiki documentation for more information about deployment on Linux.


# Installation

1.  Download **linuxdeployqt-x86_64.AppImage** from the [Releases](https://github.com/probonopd/linuxdeployqt/releases) page.
1.  `chmod a+x` it.

If you would like to build `linuxdeployqt` from source instead, see [BUILDING.md](https://github.com/probonopd/linuxdeployqt/blob/master/BUILDING.md).


# Benefits for Developers



# Benefits for End Users



# Scope



# Examples



# History



## Known issues

**This may not be fully working yet.**
See [GitHub Issues](https://github.com/probonopd/linuxdeployqt/issues) for known issues.
Use with care, run with maximum verbosity, submit issues and pull requests.
Help is appreciated.


# See Also

AppImage-AppDir(7),
AppImage-AppImage(5),
AppImage-AppImageKit(7),
AppImage-AppImageUpdate(1),
AppImage-AppRun(7),
AppImage-FAQ(7),
AppImage-Legacy(7),
<!-- AppImage-Overview(7), -->
AppImage-appimaged(8),
AppImage-appimagetool(1),
AppImage-appimageupdatetool(1),
AppImage-linuxdeployqt(1),
AppImage-payload(7)
AppImage-pkg2appimage(1),
AppImage-runtime(7),
AppImage-validate(7),
AppImage-zsync2(1),
AppImage-zsyncmake2(1).


# linuxdeployqt Ressources

- **linuxdeployqt Source Code:** [github.com/probonopd/linuxdeployqt](https://github.com/probonopd/linuxdeployqt)
- **linuxdeployqt Download:** [github.com/probonopd/linuxdeployqt/releases](https://github.com/probonopd/linuxdeployqt/releases) (`linuxdeployqt`)
- **linuxdeployqt Bug Tracker:** [github.com/probonopd/linuxdeployqt/issues](https://github.com/probonopd/linuxdeployqt/issues)
- **linuxdeployqt Wiki:** [github.com/probonopd/linuxdeployqt/wiki](https://github.com/probonopd/linuxdeployqt/wiki)
- **linuxdeployqt on IRC:** [webchat.freenode.net/?channels=appimage](https://webchat.freenode.net/?channels=appimage)



# Developers

linuxdeployqt is developed by Simon Peter (<probono@puredarwin.org>) and others.


# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.

