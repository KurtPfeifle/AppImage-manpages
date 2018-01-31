% APPIMAGEUPDATETOOL(1) | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-appimageupdatetool-manpage.md -o AppImage-appimageupdatetool.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-appimageupdatetool-manpage.md -o AppImage-appimageupdatetool.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-appimageupdatetool-manpage.md -o AppImage-appimageupdatetool.html -s -f markdown -t html
    pandoc AppImage-appimageupdatetool-manpage.md -o AppImage-appimageupdatetool.epub -s -f markdown -t epub3

-->


# Name

**`appimageupdatetool`** -- Little command line utility to help users automatically upgrade AppImages on their system.


# Synopsis

`appimageupdatetool` *-h | --help*

`appimageupdatetool` *[option]* *<some>.AppImage*


# Description



# Options



# Main Features



# Benefits for Developers



# Benefits for End Users



# Specification



# Example List of Updateable AppImages



# See Also

AppImage-AppDir(7),
AppImage-AppImage(5),
AppImage-AppImageKit(7),
AppImage-AppImageUpdate(1),
AppImage-AppRun(7),
AppImage-FAQ(7),
AppImage-Legacy(7),
AppImage-Overview(7),
AppImage-appimaged(8),
<!-- AppImage-appimageupdatetool(1), -->
AppImage-appimagetool(1),
AppImage-linuxdeployqt(1),
AppImage-payload(7)
AppImage-pkg2appimage(1),
AppImage-runtime(7),
AppImage-validate(7),
AppImage-zsync2(1),
AppImage-zsyncmake2(1).


# AppImageUpdate Ressources

**AppImageUpdate:**

- **AppImageUpdate Tools Source Code:** [github.com/AppImage/AppImageUpdate](https://github.com/AppImage/AppImageUpdate)
- **AppImageUpdate Downloads:** [github.com/AppImage/AppImageUpdate/releases](https://github.com/AppImage/AppImageUpdate/releases) (`AppImageUpdate` (GUI) and `appimageupdatetool` (CLI))
- **AppImageUpdate Bug Tracker:** [github.com/AppImage/AppImageUpdate/issues](https://github.com/AppImage/AppImageUpdate/issues)
- **AppImageUpdate Wiki:** [github.com/AppImage/AppImageUpdate/wiki](https://github.com/AppImage/AppImageUpdate/wiki)



# Developers

AppImageUpdate, AppImageKit and related tools are developed by Simon Peter (<probono@puredarwin.org>) and others.


# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.

