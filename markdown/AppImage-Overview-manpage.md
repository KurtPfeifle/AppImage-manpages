% APPIMAGEOVERVIEW(1) AppImage Technology Overview | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-Overview-manpage.md -o AppImage-Overview.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-Overview-manpage.md -o AppImage-Overview.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-Overview-manpage.md -o AppImage-Overview.html -s -f markdown -t html
    pandoc AppImage-Overview-manpage.md -o AppImage-Overview.epub -s -f markdown -t epub3

-->

# Name

**`AppImageOverview`** -- Description of the general concepts of 'AppImages': Linux binaries represented by a single file and capable to directly run on a broad range of distributions without any modification.

<!--

 # Synopsis

`./some_app.AppImage  [ --appimage-help | --appimage-mount | --appimage-extract | --appimage-updateinfo | ... ]`

-->


# Description

<!--
An implementation of the AppDir concept as a single compressed file in order to advance this idea to the "1 application = 1 file" stage (and even to "Several applications = 1 file").
-->

An AppImage is a compressed AppDir.
(See `man AppDir` for details about the latter.)
However, it is not simply just compressed, but additionally contains very small "AppRun" and "runtime" binaries which work together to execute the AppDir payload application(s) residing inside:

* The runtime creates a temporary mountpoint and FUSE-mounts the payload AppDir.
* The AppRun serves as a proxy that invokes the payload application from the AppDir.

The AppRun can be either a "standard" binary provided by the AppImageKit set of tools.
Or it can be a custom utility (even implemented as a shell script) which applies some additional magic when invoking the payload, such as implementing additional command line parameters and switches for the AppImage it is responsible for.
This could be to invoke the display of a man page for the payload application for example.
How this is exactly done is up to the packager of the AppImage.

An AppImage is never uncompressed when it runs: it is only mounted (using FUSE) to an automatically created mountpoint temporarily from where its AppDir payload is executed.
As an AppImage, its internal contents cannot be changed, they are read-only.

However, you can extract any AppImage with the command `"./<whatever>.AppImage --appimage-extract"`.
This will create a writable AppDir which also lets you also execute its payload, but now you can additionally modify its content.
This is useful if you want to debug a problem within the original AppImage or want to modify or fix it before you finally re-package it back into a modified/fixed AppImage.


# Main Features

An AppImage implements the fundamental, simple and beautiful software design philosphy of "One Application == One File".
(It can even realize the idea of "Several applications == One file".)

An AppImage lets you store any application in as small an amount of disk space as you can imagine, while at the same time keeping its software payload fully functional.

An AppImage can be run...

1. from any location on a disk,
1. from any externally connected storage device (such as an USB thumbdrive),
1. from any remotely mounted computer (for example an "sshfs" file system) or
1. even via a shared directory on the network.

An AppImage...

1. can be renamed to any other name,...

1. does not rely on the *`.AppImage`* filename extension

1. and runs even through a symlink pointing to it.

An AppImage does not need root privileges to run -- it does not even need to "install".
Just download it and run (after making it executable).

An AppImage does not mess with your base system libraries (because it does not "install").

An AppImage does not conflict with files installed and controlled by your local package management system (such as APT, RPM, YUM, ZYPPER, SMART or whatever they may be called).

An AppImage for any software 'XYZ' can run side-by-side with the system-installed software 'XYZ' (or with another 'XYZ'-AppImage) without any interference, even if their versions are very different.
(CAVEAT: see 'Known Caveats', below.)

An AppImage for software 'ABC' is an excellent tool to make available pre-releases for beta-testing to the community of your own QA, translator, artist and other contributors and users.

An AppImage can be made for any kind of Linux software, be it Free and Libre Open Source Software or closed source / proprietary software.

An AppImage is the quickest and most hassle-free way for users of any Linux distro to test (and even permanently run) a software that is not available in the repository and stores of their distro of choice.

An AppImage is the least work for packagers to do if they want to distribute working binaries of a software to as wide an audience as possible.

An AppImage gives back control to upstream developers of any software over one major distribution channel:
because they can always host their own AppImage on systems under their own control, sign it with their own GPG keys and make it their only "official" releases, taking away the gatekeepers and middlemen and Distro package policies which may disallow the distribution of "bleeding edge" software.

An AppImage is the best way to bring initially released (or newly updated) software onto any systems which have it not available thru their official channels.

An AppImage can be automatically integrated into desktop environments and the start menus of most systems by running the optional **`appimaged`** (AppImage Daemon) on the system.

An AppImage is easily created automatically if the software's source code is hosted on GitHub and if the automatic building of its binaries is enabled through Travice CI (Continuous Integration).

An AppImage can also be automatically and easily created through the Open Build Service (OBS) of openSUSE.

An AppImage can be created through different ways:

(1) Convert an existing binary package (such as DEB or RPM or TGZ).
(2) Bundle automatically GitHub / Travis CI builds as AppImage.
(3) Use *``linuxdeployqt`* for your Qt or non-Qt application.
(4) Use *`electron-builder`* for Electron apps.
(5) Manually build an AppDir and run *`appimagetool`* against it.
(6) Completely build your own AppImage from scratch by following the current AppImage specification (see below).

An AppImage can be made to self-update using the AppImageUpdate GUI utility or the `appimageupdatetool` CLI tool.
Both these are great in so far as they will not download all the bytes for a completely new AppImage version.
Instead they fetch only the binary "delta" of bytes and patch the previous AppImage to a new one.
This saves bandwidth, space and time for the end users as well as for the hosting service.

# Known Caveats

While an AppImage will never mess with your system libraries, there are known cases where a payload application may try to save its own settings and data files into its own standard location in the invoking user's *$HOME/.config/<application>* directory or similar.
This can cause un-intentional over-writing of the user's previous settings.
To avoid such situations, please make use of the *`--appimage-home`* parameter (for details, please see *`man AppImage-Appimage`*).


# Dog food

AppImage developers like to *"eat their own dog food"*:
They provide all their tools pre-compiled as AppImages, and they use AppImage-d binaries of their own tools in many of their automatic Travis CI build processes.


# Main Features



# Benefits for Developers



# Benefits for End Users



# Scope



# Description of Tools



# Examples



# History



# Current and Future Work



# Specification



# List of available AppImage-d Software



# License

The general ideas of AppImage and the AppImageKit tools are under the permissive MIT License.


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


# AppImage Ressources

**General:**

- **AppImage Format Specification:** [github.com/AppImage/AppImageSpec](https://github.com/AppImage/AppImageSpec)
- **AppImage Homepage:** [appimage.org/](https://appimage.org/)
- **AppImage License (MIT):** [github.com/AppImage/AppImageKit/blob/appimagetool/master/LICENSE](https://github.com/AppImage/AppImageKit/blob/appimagetool/master/LICENSE)
- **AppImage on IRC:** [webchat.freenode.net/?channels=appimage](https://webchat.freenode.net/?channels=appimage)
- **List of AppImages** (crowd-sourced): [appimage.github.io/apps/](https://appimage.github.io/apps/)

**AppImageKit:**

- **AppImageKit Tools Source Code:** [github.com/AppImage/AppImageKit](https://github.com/AppImage/AppImageKit)
- **AppImageKit Tools Downloads:** [github.com/AppImage/AppImageKit/releases](https://github.com/AppImage/AppImageKit/releases) (`appimaged` and `appimagetool`)
- **AppImageKit Bug Tracker:** [github.com/AppImage/AppImageKit/issues](https://github.com/AppImage/AppImageKit/issues)
- **AppImageKit Wiki:** [github.com/AppImage/AppImageKit/wiki](https://github.com/AppImage/AppImageKit/wiki)

**linuxdeployqt:**

- **linuxdeployqt Source Code:** [github.com/probonopd/linuxdeployqt](https://github.com/probonopd/linuxdeployqt)
- **linuxdeployqt Download:** [github.com/probonopd/linuxdeployqt/releases](https://github.com/probonopd/linuxdeployqt/releases) (`linuxdeployqt`)
- **linuxdeployqt Bug Tracker:** [github.com/probonopd/linuxdeployqt/issues](https://github.com/probonopd/linuxdeployqt/issues)
- **linuxdeployqt Wiki:** [github.com/probonopd/linuxdeployqt/wiki](https://github.com/probonopd/linuxdeployqt/wiki)

**AppImageUpdate:**

- **AppImageUpdate Tools Source Code:** [github.com/AppImage/AppImageUpdate](https://github.com/AppImage/AppImageUpdate)
- **AppImageUpdate Downloads:** [github.com/AppImage/AppImageUpdate/releases](https://github.com/AppImage/AppImageUpdate/releases) (`AppImageUpdate` (GUI) and `appimageupdatetool` (CLI))
- **AppImageUpdate Bug Tracker:** [github.com/AppImage/AppImageUpdate/issues](https://github.com/AppImage/AppImageUpdate/issues)
- **AppImageUpdate Wiki:** [github.com/AppImage/AppImageUpdate/wiki](https://github.com/AppImage/AppImageUpdate/wiki)

**zsync2:**

- **zsyn2 Tools Source Code:** [github.com/AppImage/zsync2](https://github.com/AppImage/zsync2)
- **zsyn2 Downloads:** [github.com/AppImage/zsync2/releases](https://github.com/AppImage/zsync2/releases) (`zsync2` and `zsyncmake2`)
- **zsyn2 Bug Tracker:** [github.com/AppImage/zsync2/issues](https://github.com/AppImage/zsync2/issues)
- **zsyn2 Wiki:** [github.com/AppImage/zsync2/wiki](https://github.com/AppImage/zsync2/wiki)


# Developers

The AppImage concept was originally devised by Simon Peter (<probono@puredarwin.org>) based on previous ideas of others and is now pushed forward by him and others through the AppImageKit project on GitHub.


# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.

