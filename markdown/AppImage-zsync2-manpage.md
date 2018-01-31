% ZSYNC2(1) | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-zsync2-manpage.md -o AppImage-zsync2.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-zsync2-manpage.md -o AppImage-zsync2.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm"
    pandoc AppImage-zsync2-manpage.md -o AppImage-zsync2.html -s -f markdown -t html
    pandoc AppImage-zsync2-manpage.md -o AppImage-zsync2.epub -s -f markdown -t epub3

-->

# Name

**`zsync2`** -- Partial/differential file download client over HTTP(S), the probably easiest efficient way to update (binary) files.

(Note: zsync2 is a working title only. Its name may change in the future.)


# Synopsis

`zsync2` *[options]*  *[path|URL]*


# Description

zsync2 downloads a file over HTTP(S).
It uses a control file to determine whether any blocks in the targetted file are already known to the downloader.
If there are such blocks, then zsync2 only downloads the new or "delta" blocks.
Usually and for convenience reasons, this control file is named just as the targetted file and located at the same path or URL, but with the added suffix '.zsync'.

Its entire functionality is bundled into a library, libzsync2, which makes it easily available for inclusion in other software.


# Options

`-h`, `--help`
:    Display this help menu.

`-i`*[PATH...]*, `--seed-file=`*[PATH...]*
:    Use data from this file during update process. Can be specified more than once.

`-I`, `--insecure`
:    Switch to HTTP insecure mode.

`-j`, `--check-for-changes`
:    Check for changes on the server. Exits with code 1 if the file changed on the server, otherwise 0.

`-k`*[PATH]*, `--copy-zsync-file-to=`*[PATH]*
:    Save copy of .zsync file to given path.

`-r`, `--resolve-redirection`
:    Resolve redirection for given URL and exit.

`-o`*[PATH]*, `--output=`*[PATH]*
:    Path to local file which should be created. If not given, file path in .zsync file will be used.

`--force-update`
:    Skip update check and force update

`-q`, `-s`, `--silent-mode`
:    Quiet mode

`-v`, `--verbose`
:    Switch on verbose mode

`-V`, `--version`
:    Print version and exit

`PATH|URL`
:    PATH or URL to .zsync(2) file

`"--"`
:    use to terminate flag options and force all following arguments to be treated as positional options


# Functional Description

zsync is a well known tool for downloading and updating local files from HTTP servers using the well known algorithms which rsync uses for diffing binary files.
Therefore, it becomes possible to synchronize modifications by exchanging the changed blocks locally using Range: requests.

The system is based on control files called *.zsync* files.
These contain hash sums for every block of data.
First, the control file is generated from and stored along with the actual file it refers to.
(The companion utility `zsyncmake2` can be used to generate such .zsync control files.)
Second, the client downloads the control file.
Next, it lets the same algorithms hash the local file as were used to generate the control file.
Then, just like with rsync, it compares both lists of hash sums.
Then, it fetches the modified blocks from the server.
Last, with the unmodified blocks of binary data from the original files it puts togethter a new file, which eventually replaces the original.

Due to how the system works, nothing but a "dumb" HTTP server is required to make use of zsync2.
This makes it easy to integrate zsync2 into existing systems.


# Hint

Hint: the companion tool named `zsyncmake2` can automatically create a .zsync file for any existing file.

# Possible Applications

A popular application scenario for zsync2 is software deployment.

Here, the popular "update channel" system can be used to describe the update model:
For normal updates (i.e., staying on the same channel), one should call zsync2 with a URL to the *.zsync* file of the latest release of the application.
Without additional effort, zsync2 is then going to update the file accordingly:

* One does not have to compare control data to check for updates etc.
* Information like version numbers for example become purely informational for the user, but irrelevant for the actual update process.

This makes setting up an update infrastructure easier (one just has to set up a static URL to the latest file).


# Real Life Application

This mechanism is implemented in the self-update functions of AppImages built with the help of AppImageKit/AppImageUpdate.


<!--

 # Examples

-->


# History

`zsync2` is a rewrite of the advanced file download and sync tool `zsync`.
`zsync` itself is derived from `zsync-curl`.


# Goals

zsync2 extends the original zsync transport protocol to also support HTTPS.

The rewrite changes fundamental principles of how zsync works.
The new code will be written following the *C++11* standard.
The entire functionality will be bundled in a single library called *libzsync2*.
The library will serve as a base for the new `zsync2` main binary'
The library can also be linked by other projects seeking to make use of its algorithms and functionality.

This project is intended to remain compatible to the original `zsync`, with the zsync file format staying the same etc.
However, the zsync file format will be extended to be able to serve additional purposes.
Such purposes could be for example to add meta info like version numbers, etc.


# Current State

Although zsync2 still shares a lot of the code with the original project, it is as of now not yet fully functional.
While debugging is ongoing, the API is somewhat ready to be used by other projects.
The project is therefore published in this state to allow testing the integration into other projects.


<!--
 # Future Work
-->

# Releases

Releases are available through the GitHub repository:

* [https://github.com/TheAssassin/zsync2/releases](https://github.com/TheAssassin/zsync2/releases)

Currently it will be pre-releases, provided as "continuous" builds, automatically triggered by every code commit through integration into the Travis CI workflow.

It is recommended to make use of the respective .AppImage files, which can be directly run on (almost) any Linux distribution after making it executable.


# Dog Food

The AppImage releases of zsync2 and zsyncmake2 are *"eating their own dog food"*:
They are seeded on the GitHub download URL with their respective .zsync files.
These .zsync files are the product of zsyncmake2.
Therefore both these binaries can be updated using the mechanism described here, with the command line options described above.


# Example Usage

## Get the AppImage

(The following example uses the first-ever released zsync2.AppImage dated "Nov 24, 2017, 02:50 PM GMT+1".
Check at [https://github.com/TheAssassin/zsync2/releases](https://github.com/TheAssassin/zsync2/releases/) for a more current link first!)

    $ wget https://github.com/TheAssassin/zsync2/releases/download/continuous/zsync2-100-e73b240-x86_64.AppImage

## Set Executable Bit of AppImage

    $ chmod a+x zsync2-100-e73b240-x86_64.AppImage

## Run the AppImage

    ./zsync2-100-e73b240-x86_64.AppImage

## Check for Update of AppImage Immediately

     $ ./zsync2-100-e73b240-x86_64.AppImage https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage.zsync

        Checking for changes...
        No changes detected, file is up to date.

## Check for Update of AppImage After a New Release has Happened

     $ ./zsync2-100-e73b240-x86_64.AppImage https://github.com/TheAssassin/zsync2/releases/download/continuous/zsyncmake2-100-e73b240-x86_64.AppImage.zsync

        Checking for changes...
        [...]



<!--  More potential sections...
 # Benefits for Developers
 # Benefits for End Users
 # Scope
 # Homepage
 # Specification
-->


# Code

[https://github.com/TheAssassin/zsync2](https://github.com/TheAssassin/zsync2)


# IRC

The zsync2 developer is also an AppImageKit developer and can be met online in IRC at Freenode in channel #AppImage.


# Known Bugs

The `-u URL` parameter known from the original zsync utility is not yet supported by zsync2.


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
AppImage-linuxdeployqt(1),
AppImage-payload(7),
AppImage-pkg2appimage(1),
AppImage-runtime(7),
AppImage-validate(1),
<!-- AppImage-zsync2(1), -->
AppImage-zsyncmake2(1).


# Developer

zsync2 is developed by @TheAssassin (<theassassin@assassinate-you.net>) based on curl-zsync building on concepts from rsync.


# License

zsync2 is put under the Artistic License v2 since it is a derivative work of software under the same license.


# Author

This manual page was written by Kurt Pfeifle (<kurt.pfeifle@gmail.com>) for the AppImage Project.
It is based on self-descriptions and READMEs written by @TheAssassin for the GitHub source code repository of zsync2 and its predecessors.

