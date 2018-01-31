% APPIMAGE(7) | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-AppImage-manpage.md -o AppImage-AppImage.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-AppImage-manpage.md -o AppImage-AppImage.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-AppImage-manpage.md -o AppImage-AppImage.html -s -f markdown -t html
    pandoc AppImage-AppImage-manpage.md -o AppImage-AppImage.epub -s -f markdown -t epub3

-->



# Name

**`some.AppImage`** - Method to bundle an application into a single file capable to directly run on a big number of Linux distros


# Synopsis

`some.AppImage`  *`[options]`* *`[ [file1 [ [file2] ] .... ]`*


# Description

An AppImage can be used without requiring root privileges, and without requiring as a pre-condition to have any specific runtime or framework installed.

The name of an AppImage can be anything and use all characters which are legal for filenames.
Giving it the `.AppImage` suffix is simply a convention and not required.
Users may choose to rename an AppImage as they deem convenient.
(It is completely up to them to be able to identify AppImage files easily then.)

AppImages are Linux applications packaged in a "distro agnostic" way so they can run on a large range of recent and not-so-recent Linux distributions.


# Options and Parameters

`[options]`

:   Start options and parameters passed to the AppImage fall into three categories:

     1. *Native options*: these are all these options which the embedded application may support.
     1. *General AppImage options*: these are supported by all recently created AppImages (of type 2).
     1. *Options specific to this AppImage*: these are options which the AppImage packager chose to support in this specific AppImage package.

    Details follow below.

    *(Note: There are two types of AppImages.
    The "type 1" is deprecated.
    If you encounter one, kindly ask its packager to create future versions as type 2 AppImages.
    This man page mainly applies to type 2 AppImages.)*


`[file1 [ [file2] ] .... ]`

:   Whether you can pass one or more filenames to the AppImage is completely up to its embedded payload application.
    Such a filename may be the name of an existing document to be opened or a new document to be created.

    Note:

    1. Some applications *need* a filename to start up (example: 123xyzABC TODO).
    1. For some applications it is optional to pass a filename to them (example: LibreOffice).
    1. Some applications do *not support* a filename when starting them (example: 123xyzABC TODO).

# Native Application Options

The *native* options supported by the embedded application can not be described here exhaustively:
their specific names, their meanings and how many are available at all are different from application to application.

The AppImage passes these options unchanged to the embedded payload application.


## General Examples

`-h`, `--help`, `--usage` or `--version`

:   These will print to `<stdout>` the messages (if any) which the payload application wants to print there.

    If `-h` would normally invoke the standard web browser and open a HTML file or a remote URL, the AppImage will do the same.

`--verbose`

:   Ask the payload application for more verbose output.
    This only works for the AppImage if the payload supports this parameter.

## Application-specific Examples

`./KDevelop-5.2.0-x86_64.AppImage --license`

:   Ask KDevelop inside the AppImage to display its license.

`./LibreOfficeDev-daily-x86_64.AppImage ---impress`

:   This will start LibreOffice Impress (the LibreOffice part responsible for creating and displaying presentation slides) and will at the same time create an empty Impress document.

`./powershell-6.0.0-beta.9-x86_64.AppImage -ExecutionPolicy RemoteSigned`

:   Start a new PowerShell session, set the default execution policy to `RemoteSigned` and save it in the `$env:PSExecutionPolicyPreference` environment variable.
    This does not change the PowerShell execution policy of future sessions.

`./nvim-nightly.appimage --noplugin`

:   Start the NeoVim editor without loading any plugins.



# General AppImage Options

Recently created (type 2) AppImages support some general options which all follow the `--appimage-*` naming convention.
Option names starting with the `--appimage` prefix are reserved.
They may not be used by the payload application.

`--appimage-help`

:    Print all AppImage options with a short explanation.
     The number of available options may increase in the future.
     Currently supported options follow below.

`--appimage-mount`

:    Mount the embedded file system image without starting it, print mount point and wait for termination.
     Termination can happen by sending the usual SIGINT signal, for example through the keyboard shortcut `Ctrl+c`.

     This is useful for AppImage packagers to debug, modify or repair an AppImage.
     Users normally should not need to do it.

`--appimage-extract`

:    Extract the payload application of the AppImage into an AppDir.
     The name of the AppDir currently is *squashfs-root*.
     This may change in the future.

     This is useful for AppImage packagers to debug, modify or repair an AppImage.
     Users normally should not need to do it.

     How to re-compress the AppDir into an AppImage, see **`appimagetool(1)`**.

`--appimage-offset`

:    Print the byte offset to the start of the embedded file system image.

`--appimage-signature`

:    Print the digital signature which may be embedded in the AppImage.

`--appimage-updateinfo[rmation]`

:    Print all update info which may be embedded in the AppImage.

     If there is no output, the AppImage packager has not prepared the AppImage for semi-automatic updates.
     The reason for this may be: he does not yet know this option, which was not present in the AppImage technology from the beginning.
     You may want to ask him to package his future AppImages with this feature enabled.

`--appimage-version`

:    Print the version of AppImageKit tools which have been used to create the AppImage.
     (Note, in order to see the version of the payload application embedded in the AppImage, you'll have to use whatever *native* parameter the payload application supports to reveal its version info.
     Examples: `-v`, `-version`, `-V` or `--version`.)

`--appimage-portable-config`

:    Create an empty subdirectory with exactly the same name + path as the AppImage, but an additional `.config` suffix.
     The AppImage will use this directory from now on as if `XDG_CONFIG_CONFIG` environment variable had been set to point to it.

`--appimage-portable-home`

:    Create an empty subdirectory with exactly the same name + path as the AppImage, but an additional `.home` suffix.
     The AppImage will use this directory from now on as if `PATH` environment variable had been set to point to it.



# Package Specific Options

The *package specific* options implemented by the AppImage packager for a specific package can not be described here.
They are completely up to the packager.
They are mentioned here purely to establish as common knowledge the fact that this is possible.


## Examples

1. The AppImage for ImageMagick ...
1. An AppImage packager may chose to let the AppImage user access embedded man pages by some mechanism he implements through a custom *AppRun* embedded into the AppImage.
   For example he could choose to simply use `--man` as the first parameter of AppImage invokation to make the AppRun display the respective man page embedded.
   (See **`AppRun(1)`** for more details.)



# Main Features



<!--
 # Benefits for Developers



 # Benefits for End Users



 # Scope



 # Description of Tools



 # History



 # Current and Future Work



 # Specification



 # Code
-->


#Bugs

If you find an AppImage which does not work as expected you may contact the AppImageKit developers as well as the packager of the AppImage (who in most cases will be completely different entities).
Please provide any info you can collect by applying commands and parameters as described above to the AppImage giving you problems.

The reason for your problem frequently lays in a wrong way of packaging, but it may well be a bug in AppImageKit tools used to build the package.

The two parties named above may need to cooperate in order to fix it and make it work for you and your distribution.


# IRC

The AppImage developers can be met online in IRC at Freenode in channel #AppImage.



<!--
 # Bug Tracker


 # Wiki



 # List of available AppImage-d Software



 # Homepage
-->

# Notable Examples

1. Microsoft uses an AppImage of *PowerShell* to distribute version 6.0.0.0-Alpha to Linux users who may be interested to familiarize with this object-oriented shell.
1. The developers of *Subsurface*, an end-user GUI application for hobby and professional divers for dive logging, planning and evaluation, which was started by Linus Torvalds, distribute their Linux releases as AppImages.
1. Most Free and Open Source programs which are important to the *3D printing community* are available as AppImages.
1. The *ImageMagick* developers have recently started to distribute pre-built binaries of their most recent versions in the 7.x series as AppImages.
1. The *Nitrux* Linux distribution bases their complete software center (which allows user to add extra software on their systems) on AppImages.
1. The *Open Build Service* (OBS) allows its users to automatically build AppImages and provides an easy to use framework with all tools and dependencies to do so.


# Files

`/path/nameof.AppImage`

:   An AppImage can be stored in any path readable by the user.
    The executable bit needs to be set in order to run it.

    An AppImage does not need to carry the suffix '.AppImage'.
    It may be re-named by the owning user to any convenient name, with or without suffix.

    Also, any number of symlinks pointing to the real AppImage may be created and they will start the AppImage as well.
    (Note, whether you can *run* multiple instances of the AppImage concurrently is up to the embedded application:
    *some* apps do not allow multiple concurrent instances to run.)

`/path/nameof.AppImage.config`

:   A subdirectory with the exact same name and path as the AppImage, but the appended suffix of `.config`, can be created.

    This is completely optional and not required to run the AppImage.

    If existing, upon its next start the AppImage will automatically treat it as its `XDG_CONFIG_PATH` environment variable and write all config settings it may need to remember into that directory.

    The `.AppImage.config` directory may be created manually.
    More convenient for the user may be to cause the AppImage to create this directory by itself.
    The AppImage will do this if run from the command line with appended parameter `--appimage-portable-config`.

    If the AppImage is renamed, the subdirectory must be renamed accordingly.

    Using the `XDG_CONFIG_PATH` variable is useful, if the user wants to use multiple Versions of an AppImage-d application concurrently and keep their configurations cleanly separated or if she wants to use an AppImage side-by-side with the "installed" version of the application under the control of the package manager

`/path/nameof.AppImage.home`

:   A subdirectory with the exact same name and path as the AppImage, but the appended suffix of `.home` can be created.

    This is completely optional and not required to run the AppImage.

    If existing, upon its next start the AppImage will automatically treat it as its `HOME` environment variable and write all date it may need to remember into that directory by default.

    The `.AppImage.home` directory may be created manually.
    More convenient for the user may be to cause the AppImage to create this directory by itself.
    The AppImage will do this if run from the command line with appended parameter `--appimage-portable-home`.

    If the AppImage is renamed, the subdirectory must be renamed accordingly.

    Using the `HOME` variable is useful, if the user wants to use multiple Versions of an AppImage-d application concurrently and keep their date cleanly separated or if she wants to use an AppImage side-by-side with the "installed" version of the application under the control of the local package manager.


# See Also

AppImage-AppDir(7),
<!-- AppImage-AppImage(7), -->
AppImage-AppImageKit(7),
AppImage-AppImageUpdate(1),
AppImage-AppRun(7),
AppImage-FAQ(7),
AppImage-Legacy(7),
AppImage-Overview(7),
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

# Developers

AppImage as the concept to implement the idea of "One App = One File" is pursued by Simon Peter (<probono@puredarwin.org>) since 2004 even if at times under different project names.
The concept builds on the much older design of AppDirs (application directories), such as is still used in macOS with the `.app` structure which implements the idea of "One Dir = One App".
AppImages push the envelope and go beyond their ancestors in that they are compressed into a single file as a filesystem (using SquashFS) instead of living just in a separate directory.


# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.

