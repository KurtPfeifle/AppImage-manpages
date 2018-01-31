% ZSYNCMAKE2(1) | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-zsyncmake2-manpage.md -o AppImage-zsyncmake2.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-zsyncmake2-manpage.md -o AppImage-zsyncmake2.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-zsyncmake2-manpage.md -o AppImage-zsyncmake2.html -s -f markdown -t html
    pandoc AppImage-zsyncmake2-manpage.md -o AppImage-zsyncmake2.epub -s -f markdown -t epub3

-->


# Name

**`zsyncmake2`** - Create a *.zsync* file for an existing file


# Synopsis

`zsyncmake2` *`[options]`* *`[path/to/]filename`*


# Description

zsync2 downloads a file over HTTP(S).
It uses a control file to determine whether any blocks in the targetted file are already known to the downloader.
If there are such blocks, then zsync2 only downloads the new or "delta" blocks.

zsyncmake2 creates such a control file.
This control file is named just as the targetted file and located at the same path, but with the added suffix '.zsync'.


# Options

`-h`, `--help`
:    Display short help hints.


`-u`*[URL]*, `--url=`*[URL]*
:    URL the .zsync file should point to (may be relative)

`-b`*[blocksize]*, `--blocksize=`*[blocksize]*
:    Specify the blocksize to the underlying rsync algorithm.
     A smaller blocksize may be more efficient for files where there are likely to be lots of small, scattered changes between downloads;
     a larger blocksize is more efficient for files with fewer or less scattered changes.
     This blocksize must be a power of two.
     If not specified, zsyncmake2 chooses one which it thinks is best for this file (currently either 2048 or 4096 depending on file size) - so normally you should not need to override the default.

`-c`*[key=value...]*, `--custom-header=`*[key=value...]*
:

`filename`
:    Name of existing file for which zsyncmake2 should generate a .zsync file.

`"--"`
:    Terminate option flags and force all following arguments to be treated as positional parameters.


# Functional Description

The original file is divided into blocks.
For each block a hash value is created.
For each block and its byte range, the respective hash value is stored in the .zsync control file.


# Hint

Hint: the companion tool named `zsync2` can read the .zsync file for an existing file.
It then proceeds to compare this existing file with with the the info provided by the .zsync file.
If the comparison determines that there are differences, zsync2 downloads the blocks with the differences only, and inserts them into the original file to be updated.


# Releases

Releases are available through the GitHub repository:

* [https://github.com/TheAssassin/zsync2/releases](https://github.com/TheAssassin/zsync2/releases)

Currently it will be pre-releases, provided as "continuous" builds, automatically triggered by every code commit through integration into the Travis CI workflow.

It is recommended to make use of the respective .AppImage files, which can be directly run on (almost) any Linux distribution after making it executable.


# Dog Food

The AppImage releases of zsync2 and zsyncmake2 are *"eating their own dog food"*:
They are seeded on the GitHub download URL with their respective .zsync files.
These .zsync files are the product of zsyncmake2.
Therefore both these binaries can be updated using the mechanism described in the zsync2 man page.

You can verify if the .zsync file from the GitHub distribution channel is the same as one which you create locally.


<!--
 # Example Usage

 ## Get the AppImage

(The following example uses the first-ever released zsync2.AppImage dated "Nov 24, 2017, 02:50 PM GMT+1".
Check at [https://github.com/TheAssassin/zsync2/releases](https://github.com/TheAssassin/zsync2/releases/) for a more current link first!)

    $ wget https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage
    $ wget https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage.zsync

 ## Rename downloaded .zsync file

    $ mv ./zsyncmake2-100-e73b240-x86_64.AppImage.zsync ./zsyncmake2-100-e73b240-x86_64.AppImage.zsync.remote

 ## Set Executable Bit of AppImage

    $ chmod a+x zsyncmake2-100-e73b240-x86_64.AppImage

 ## Run the zsncmake2 AppImage to create a local version of its .zsync file

    $ ./zsyncmake2-100-e73b240-x86_64.AppImage ./zsyncmake2-100-e73b240-x86_64.AppImage

 ## Compare the .zsync.remote with the locally generated .zsync file

    $ ls -l *.zsync*
    $ md5sum *.zsync*

-->

## Check for Update of AppImage Immediately

     $ ./zsync2-100-e73b240-x86_64.AppImage https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage.zsync

        Checking for changes...
        No changes detected, file is up to date.

## Check for Update of AppImage After a New Release has Happened

     $ ./zsync2-100-e73b240-x86_64.AppImage https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage.zsync

        Checking for changes...
        [...]



<!--
 # Main Features
 # Benefits for Developers
 # Benefits for End Users
 # Scope
 # Description of Tools
 # History
 # Current and Future Work
 # Specification
 # List of available AppImage-d Software
 # Homepage
-->



# Code

[https://github.com/TheAssassin/zsync2](https://github.com/TheAssassin/zsync2)


# IRC

The zsyncmake2/zsync2 developer is also an AppImageKit developer and can be met online in IRC at Freenode in channel #AppImage.


# Known Bugs

None so far.
But this code is very little tested, and still in its infancy.


# Bug Tracker

[https://github.com/TheAssassin/zsync2/issues](https://github.com/TheAssassin/zsync2/issues)


# Wiki

[https://github.com/TheAssassin/zsync2](https://github.com/TheAssassin/zsync2) -- Currently no content yet.


# See Also

AppImage-AppDir(7),
AppImage-AppImage(1),
AppImage-AppImageKit(7),
AppImage-AppImageUpdate(1),
AppImage-AppRun(7),
AppImage-FAQ(7),
AppImage-Legacy(7),
AppImage-Overview(7),
AppImage-appimaged(1),
AppImage-appimagetool(1),
AppImage-appimageupdatetool(1),
AppImage-linuxdeployqt(1),
AppImage-payload(7),
AppImage-pkg2appimage(1),
AppImage-runtime(7),
AppImage-validate(1),
AppImage-zsync2(1).
<!-- AppImage-zsyncmake2(1). -->


# Developers

zsync2 is developed by @TheAssassin (<theassassin@assassinate-you.net>) based on curl-zsync building on concepts from rsync.


# License

zsync2 is put under the Artistic License v2 since it is a derivative work of software under the same license.

# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.

