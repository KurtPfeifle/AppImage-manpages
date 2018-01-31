% APPIMAGEFAQ(1) AppImage Frequently Asked Questions | The AppImage Documentation Project
%
% __date__

<!-- Generate man, HTML, EPUB or PDF output like so:

    DATE=$(date "+%Y-%m-%d")
    VERSION=0.0.1
    # replace line 5 in this file, above: $DATE instead of '__date__'
    pandoc AppImage-FAQ-manpage.md -o AppImage-FAQ.man  -s -f markdown -t man   -V footer:"Manual Page Version $VERSION, $DATE"
    pandoc AppImage-FAQ-manpage.md -o AppImage-FAQ.pdf  -s -f markdown -t latex -V footer:"Manual Page Version $VERSION" -V geometry:"margin=2.0cm, paperwidth=595pt, paperheight=297mm" \
                                                                  -H fancyheaderfooter.tex \-\-toc -V classoption:"twoside"

    pandoc AppImage-FAQ-manpage.md -o AppImage-FAQ.html -s -f markdown -t html
    pandoc AppImage-FAQ-manpage.md -o AppImage-FAQ.epub -s -f markdown -t epub3

-->


# Name

**`AppImage-FAQ`** - Frequently Asked Questions with Answers regarding AppImages, AppImageKit and their Design & Development


# Synopsis

Many questions -- short answers.


# Go on!

**What is the most important feature of the stuff you guys do?**

:   We like the design principle of *"One Application = One File."*


**So what exactly is an application that is at the same time one file only?**

:   That's what we call an "AppImage".

    This way, no *installation* is needed to run an application.
    Also no *package management* is needed.

    As a result you will end up with *"One Application = One File = One Package = AlmostAnyRecentDistro"*.


**And that's all? Even when I want to test hundreds of AppImages and their versions I do not need to have a package manager working for me?**

:   Yes, that's all.
    No, you don't need a package manager for AppImages.

    You ought to keep your disk space and home directly neatly organised, if you do not like to have your applications distributed wildly around the place -- but that's what you do anyway, right?
    Just put them into one folder, and you are done.


**What is the special thing about AppImages then?**

:   If done right, they basically run on most Linux distros, old and new.

    You can carry them around on a USB stick, and get it to run on the CentOS notebook of your friend, even though you downloaded it for your openSUSE Tumbleweed and normally use it there.
    In principle it will be able to run on many dozens of Linux versions, old and new.
    If it doesn't, you found a bug, which we most likely can fix.

    An AppImage also runs from a network share.
    Or from an *sshfs*-mounted remote server.

    We regularly test AppImages on more than 100 ISO Live systems which we keep sticking around for this purpose.
    To make life even easier, we do not run them from CD.
    No need to juggle these silvery disks.
    We put them as ISO images onto a single medium, from where we can boot them up as needed.


**How do you boot all these ISO Live systems from a single medium? Is there any trick we need to know about and you are willing to share with us?**

:   Sure.

    I'm using another project of mine, which is also on GitHub: [SystemImageKit](https://github.com/probonopd/SystemImageKit).
    Warning: it's not polished yet, and therefore has not many users.
    But it has been working for me since many years.

    That makes me confident to say that AppImage was successfully tested to work on many more different systems than other new packaging methods will ever even touch.
    Ok, that was a bit unfair to say... because you hardly can put a brandnew, still maturing package management system on a random five year old Live distro, can you?
    However, an AppImage will easily work (or not -- in which case it is a bug in the AppImage).

    Seriously, my setup with SystemImageKit allows me to test really quickly any AppImage on almost any Linux Live system which was ever published in the last few years.


**Is this why I've heard people saying about AppImages: *"Build Once, Run Anywhere"*?**

:   Basically, yes.

    Well, our AppImages don't run on *Windows*.
    And currently our building tools only create AppImages which run on x86-64 CPU architectures.
    So for example, i386 and i586 (both 32bit) are not covered.
    Most people run 64bit systems nowadays.
    But ARM and Raspberry Pi systems are also still missing...
    While it wouldn't be difficult at all to add these -- we are just lacking the man power to expand to these CPU architectures.

    So if one of your readers is willing to tackle a port of AppImageKit to Raspberry and other ARM platforms:
    we are more than willing to lend enough support to make it a success, but we can't do it by ourselves.


**Do AppImages ship with a secure sandbox or firewall?  You know, in order to isolate their apps from the system and from other applications?**

:   No.


**Why not?**

:   We believe that you should be able to pick your own sandboxing / firewalling solution.

    It was a design decision from the beginning to NOT implement our own sandbox or firewall solution.
    Instead we chose to make it very easy for external sandboxing/firewalling utilities to take care of the protection from and for AppImages.

    If in doubt, we believe in *"Do one thing --  but do it RIGHT!"*
    Our thing is to provide the tools for packaging with the "1 app = 1 file" principle.
    We leave the business of sandboxing and firewalling to the people who understand the realm of sandboxing and firewalling.
    People who understand it better than we do that ourselves.
    People who understand it FULLY and therefore dare to develop in this area.


**Isn't this "isolation", "sandboxing" and "firewalling" thing pretty important nowadays? At least it is all the buzz I keep hearing about Snap and Flatpak, which seem to be doing pretty well in this area and seem to be projects competing with you...**

:   They both follow a COMPLETELY different philosophy from ours.
    Even though they also try to address the cross-distribution compatibility issue, they do so in very different ways.
    They are much more like traditional package managers whereas AppImage is much more like a .dmg disk image on the Mac.

    Both do not at all care about our "1 app = 1 file" principle.
    Both need their own framework installed on your system FIRST in order to run their package formats.
    And you need to be root in order to install their respective frameworks. --
    If your distro-of-choice does not support Snap or Flatpak, then you are out of luck (even though that barrier may go away over time if Red Hat and Canonical continue to agree on things).
    But currently Flatpak and Snap are not supported out of the box (i.e., without having to install extras using the package manager) on many systems.

    Also, both are alternative *package managing* systems.
    You need to learn a new way of *installing* software.
    Even if you are a command line addict, you'll have to learn a new syntax first.
    And we hear, it is not so easily grokked even by "old timers".

    One day these early warts of both systems will be overcome however.
    And maybe one of them will become the predominant new package manager -- but they'll then still be *package managers*.


**What's wrong with that? What's wrong with package managers?**

:   Nothing!

    Nothing, if they work the same across a large range of distributions.
    Nothing, if they can install the same package un-changed onto Red Hat from three years ago, Ubuntu and Debian from today, or openSUSE Tumbleweed from tomorrow.

    Nothing, if I can run the latest nightly build of my favorite application on, say, Debian Stable, without it changing any of the libraries in the system.
    Or on an Enterprise distribution like SUSE Linux Enterprise without losing me the "supported" status.
    Nothing, if I can finally go to a project's download page and grab, next to the Windows *.exe* and the macOS *.dmg*, something for Linux that "just works" and doesn't require me to fiddle around (as root!) on the command line with GPG signatures, *sources.list* entries, PPA repositories and the like.

    However, currently that is still a pipe dream.

    If one of these two, Snap or Flatpak wins the competition between the two, and in some distant future becomes *the* only or predominant way to provision Linux software packages, that's possibly a good thing.
    At least it would be progress compared to the mess we have today.
    At least there would be one unified way to install applications on most or even all Linux distros.

    Even if it was only the second-best of the two to win the competition:
    that is bound to improve the situation over what we have today.

    It would most likely be a *better* package manager than all from today, but it would still be a package manager....


**Again -- what's wrong with package managers as we have them now?**

:   Let me answer with a counter question:
    Who *wants* a package managager anyways?

    System administrators.
    People who put together operating systems.
    Corporate IT for "managed systems".

    But not end users on personal machines.

    What you *do* want is applications which simply work.
    Work out of the box!

    Why were package managers invented in the first place?
    Obviously, because so far we seem to have not figured out how to put applications into a shape so that they simply work out of the box.
    Obviously, because managing applications was not just drag-and-drop but so complicated to manage that you needed a "manager" to do it.


**You think package managing systems are not a nice thing to have per se, but only a 'dirty' tool?**

:   We invented package managers to serve us as a tool, so we eventually could run the application which we really wanted.
    It was good that we had them.
    Nothing 'dirty' about it.

    Package management systems nevertheless remain duct tape, or crutches to help us walk in the software sphere.
    Sometimes in life crutches are really useful and nice to have.
    Just don't let them acquire a life of their own, don't miss when it's time to leave them behind.

    They served us to overcome that initial obstacle and to INSTALL the software for us.

    Softare installation and un-installation is quite a complicated task, if you look at it...
    Which is why a package management system also needs human packaging specialists, highly skilled people who have to be very meticulous in their work, no doubt about it.
    And which is why we hold good packagers in high esteem, usually.
    They have a high reputation, and they deserve it!

    But haven't we forgotten that they were serving us only to provide us with crutches?
    Crutches we need because the software we want to use arrives in an un-usable shape?
    I want to arrive at a situation were I do not limb any longer, where I do not need crutches, package managers and packaging humans any more.
    Where the preparation of any software into a directly-runnable shape is easy and automated.
    Where that is part of the software development process itself.
    These previous packagers would finally be able to put their high skills and their smartness and their long experience to even better use, instead of hunting down boring packaging problems again and again.


**You seem to think a deeper change to the software building process is called for than what it looks at first when you encounter a working AppImage?**

:   Yes.
    The whole building process has to change and improve.
    To one where whenever programmers invoke the *make* command on their computers, the outcome is an AppImage.
    Not a binary which only HE/SHE can run on his/her computer alone, and no-where else.
    And when the current development stage is ready for shipment:
    where they have to hand over their code to a packager first, who then puts it into a shape the package managing system accepts, which then will put it on the user's computer.

    Programmers, after running *make* should directly see and run the same binary which the end user would see and run.
    They should be able to pass that same binary to their testers, project managers, colleagues, end-users and whomever without any special preparation.
    And once it is ready to ship, ship it as is.

    Some people seem to have become so familiar with software package managing systems and their human maintainers that they take them for granted.
    As if these weare a means for themselves.
    As if the $DEITY, when it created $universe had proclaimed: *"Let There Be Light. And Package Managers. Because Open Source Software (and everbody else) will need them! Believe me."*

    We should finally show some insight.
    Or are we THAT much used to think The Earth Is Flat that we do not see beyond our small village steeple any more?


**How does AppImage fit into the picture with Snapcraft and Flatpak then?**

:   As said before, AppImage has a very different focus.
    Becoming a package management system certainly isn't it.
    It's meant to be so simple for the user that you can do everything with drag-and-drop.

    An AppImage can be started and tested straight away, by any user, without needing to become root, without preparing the system, without any additional framework, without requiring prior support from the Distro Gods That Be and without "installing" it.

    One of the most important goals of AppImage is to place a tool into the hands of developers of software, of upstream developers.
    A tool  which allows them to *directly distribute* their products in pre-built form to their end-users.
    So they can have a straight line to their end users, who can directly take software and simply run it, without intermediaries.
    While application authors are in *full control* of the end user experience.
    Where they can *support* their binaries.
    Without an intermediary *packager*.
    Without an intermediary distro *repository*.
    Without an intermediary *package managing system*.
    Without an intermediary *App Store* that is practically mandatory.

    Without all kinds of intermediary gatekeepers and technical obstacles which have to be overcome in order to provide dozens of different binary packages in their respective formats so the software can run on dozens of different Linux distros.

    With AppImage, a software developer needs to package only *one* thing (and can automate this using Continuous Integration systems such as Travis CI on GitHub or the Open Build Service), and be sure it runs on dozens of distributions.
    When handling bug reports, she will look at exactly the same binary that her user has a problem with.

    With AppImage, developers have a nice way around all gatekeeping institutions making it a difficult thing to fullfill their wish to get their code out *fast* to *most* users.

    From what we see, completely irrespective of each one's technical merits, neither Snap nor Flatpak do get rid of "App Stores" and Gatekeepers.
    Snapcraft is tied in to the Canonical/Ubuntu walled garden; Flatpak's one is that of RedHat.

    And even if a developer or a group of them wants their stuff eventually get distributed in the "conservative" way through official distro channels:
    there are still frequent occasions in your life where you want your hot-new and steaming-fresh results results of your late-night shifts get out very fast.
    Getting it into the hands of your testers, QA volunteers, translators, artwork and icon designers, documentation writers and whom not.

    How else are you distributing binary code to them FAST?
    A way which is also SAFE for their systems' stability?
    Safe because it does not mess with their installed libraries?
    And which does not require them to first jump through dozens of loops first just in order to get their systems made ready to install your new hot alpha or beta quality shit just to test it and work on it?
    Ok, if they all have big hardware to run enough Virtual Machines and store lots of snapshots, you already had a way in the past.
    But now AppImage can do the same, and does it even better, faster, in less time and cheaper.


**Uff... this is pretty heavy stuff! And this was your answer about the "isolation" and "firewalling" I asked?**

:   Sorry, I got carried a way a bit.
    But admit it: you compared us to Snap and Flatpak -- so I wanted to make very clear where, why and how a comparison is not adequate at all.


**Ok, let me try again. Which external tools can I use for sandboxing / firewalling with AppImages then?**

:   Look for *[Firejail](https://firejail.wordpress.com/)*  and *[Bubblewrap](https://github.com/projectatomic/bubblewrap)*.



**Is there a HowTo of running an AppImage inside a sandbox?**

:   For one regarding [Firejail look at their documentation](https://firejail.wordpress.com/documentation-2/appimage-support/).



**They say that your method to achieve your goal *"1 app = 1 file"* is leading to bloat. They say, I end up with dozens of versions of the same library in my file system, where I'd need only one! They say, you're wasting my precious disk space...**

:   First, AppImages (if done right), bundle only those libraries which very likely are not available on all the systems you are targeting.
    Assume a recent enough version in the default installation.
    Yes, this may give you a little extra overhead of bytes -- on paper.
    "Little", because these bytes are *compressed* inside the AppImage, and never get extracted on disk.
    Not even when the AppImage runs!
    These bytes remain always locked inside the (read-only) AppImages.

    Overall, AppImages could even *save* a lot of space if you built a system which uses them for all the additional applications.

    Second, ...

**Waaiiiiit! I do not believe you: what about when the AppImage runs? It does need to be expanded then, for sure!**

:   Yes, it needs to expand.
    This expansion only happens into *memory* (RAM).
    It occurs when the payload application starts and required libs load.
    But almost never the complete app -- only these parts which the user currently makes use of.
    This is also like with any other app:
    To run, it has to be loaded into RAM first.

    AppImage extraction can happen very fast, and this design means that less (slow) disk I/O is needed.
    So depending on the application and disk configuration it may actually *speed things up*.

    An AppImage-d app requests the same amount of RAM during runtime as the equivalent "standard" app does.

**Sorry to have interrupted -- but I needed this clarification. What was your second point again?**

:   Second, as you could also conclude from the other answer -- the "dozens of versions" of the same library (even if that number was true) will never "end up in your file system".
    They will at all times remain encapsulated in the read-only AppImage file system.

    AppImages do not -- and cannot -- mess with your system libraries.
    These will at all times be left alone and not modified.
    Do you realize that every DEB or RPM you install can do *anything* to every part of your system, because its preinstall script runs as root?

**But isn't a typical RPM or DEB package also compressed when it is downloaded and installed? Isn't the AppImage advantage here purely ficticious?**

:   Yes, RPMs or DEBs are compressed while they are downloaded and even while they are stored on disk.

    However, once they become *installed* they are expanded onto disk space.
    (Sometimes people do not even delete their packages from the local storage...)

    And this expansion typically is surprisingly large.
    The install step typically scatters hundreds and even thousands of files across the system.
    Granted, the package managers usually are very good in keeping their house tidy, and collect all these files again to remove them if you decide to uninstall a package for good.
    But what if a friend comes along and says "I like this app, can you transfer it over to me?" --
    Good luck if you haven't kept around the RPM or DEB.


**Can you give me an example? One which a lot of Linux people would be using? How much space does that translate to for, say, LibreOffice?**

:   Take the latest 5.4.3.2 release of LibreOffice.
    The basic packages (RPM or DEB) without any extra language, local help file or plugin support weigh in at around 270 MByte.
    That's for download and storage *before* installation.

    Now install the beauties:
    on both systems you'll now have more than 8.000 files distributed over ~900 directories and subdirectories consuming an extra of 960 MByte of disk volume.
    At this point you have had to provide (270 + 960 =) 1.230 MByte of disk space.
    Ok, now you delete the DEB/RPM packages again: you've paid your LibreOffice installation with 960 MByte of consumed HDD.
    And you've paid with your precious lifetime: time needed for unpacking, installing, uninstalling.
    Update comes along, the whole thing starts over again.

    Compare that to the equivalent LibreOffice.AppImage file:
    initial downloading isn't any cheaper -- you also have to get around 270 MByte.
    Now save the "install" step.
    Not needed.
    Now make executable and run the beauty.
    Still no more disk space needed.
    (Unless you create a huge document with it -- but that's a different story...)
    Your system still has only 1 extra file to cope with, no extra directories (unless you bedded the beauty into its own, newly created one), and you lost "only" 270 Mbyte of free HDD.

    With these "savings" alone (almost 1 GByte), we could bundle a lot of duplicate libraries into the AppImage, I can tell you, and you would probably never-ever even notice it.

    Update comes along.
    Using AppImageUpdate, you only download the few MBs that have changed since the last version.
    We call that "binary delta updates".
    Happens within seconds.
    Done!

    So how's that for a comparison?
    What do you now say in respect to "bloat"?

<!--

*** Already addressed as a side note above ***

**But isn't there any other "overhead"? Will this expansion, every time you run the AppImage, not cost extra CPU cycles? Will not everything become more slow, less responsive and lagging?**

:   Yes, there certainly is SOME overhead like this.

    But we have not found it bothering enough to investigate more deeply and find out what percentage this overhead does amount to.
    Overall, we find that for any typical GUI application you will not notice any difference in how it performs.
    The minor penalty costs of extra CPU cycles which the expansion of the compressed application into memory costs at runtime is easily covered by the huge improvemens of CPU power in today's systems.

    Why don't you simply test it on your own?
    Is it REALLY slower?
    Can you "feel" it?
    Can you measure it?
    Tell us what you find!

-->

<--
*** Already said many times ***

**Do I need to be root in order to use an AppImage-d application?**

:   No.

-->

**So I can put any AppImage somewhere into my $HOME directory and run it from there?**

:   Yes.


**AppImages are only for individual users then? And each one has to get her/his own copy of an AppImage if they want to use it?**

:   No.

    If the local system admin puts the AppImages into a system wide $PATH location, all local system users can run them.
    It's just like with any other application.


**Sounds good so far... But aren't you a bit too much obsessed by your project? Hasn't your "one app = one file" principle now become a little dogma? Won't you ever make a compromise about this? Say, I wanted to integrate my collected AppImages into my desktop...**

:   Oh, we *have* this already!
    It's called the *"appimaged"*, the AppImage Daemon.

    But it's completely optional.
    You do not *need* it to run AppImages.
    It just makes it much more convenient.


**What does it do?**

:   Whenever you bring a new AppImage onto your system (and don't hide it in some far-far-away directory location) or into your $HOME directory, the daemon discovers the AppImage.
    It then extracts the payload application's .desktop and Icon files and puts them into the start menu.
    This way you can start the AppImage without needing to go to the command line.


**But, but... isn't that act of extracting the .desktop and Icon files a sort of "installation"??**

:   We call it "desktop integration".
    We only put the desktop files, icons, MIME types, file associations and such into the appropriate places inside the user's home directory.
    We do not install the application in the traditional sense.
    Not sure I like all this file scattering stuff, Apple's Launch Services appear to handle this kind of thing more elegantly...
    But well, that's the state of the Linux Desktop as of today.

<!--

:   Ok, now you've got me.
    Caught in the act!
    You found me red-handed...

    Guilty as accused!  ;-)
    Yes, in this case we *temporarily* "install" the .desktop and the icon files into the user's desktop environment.

-->



**How do I remove the new menu entries, .desktop and icon files from the start menu again? (Now we have a case of clutter, I knew it!)**

:   Fear not.
    The daemon will also clean up again.
    If you remove/delete/move the AppImage it will keep track and update the menus.
    Even if you rename it to a name *without* the .AppImage suffix!
    Once the AppImage is gone for good, it will also wipe the menus for you.


**Where can I get this magic daemon? Sure now I need to find a package from my distro! What do I do if they don't have it?**

:   You're covered.

    We offer the *appimaged* as an AppImage... of course!!
    we love to eat our own dogfood, after all.

    Just download it, make it executable and run it.
    Don't forget to run it for once with the `--help` parameter, so you get an impression about the details of handling it.
    For distributions such as Nitrux which are integrating *appimaged* right into the system, we recommend doing so using a normal distribution package.
    It's then part of the base system, after all - which is rightfully managed by the distribution and its tools.


**In the end, you do not look as dogmatic as I thought...**

:   There's a difference between firm principles and a fixed dogma.

    We don't mind some little helper tools, as long as they are *optional* and only make running and handling of AppImages more smooth and comfortable to users.
    As long as we cannot directly embed this functionality into the AppImage.
    And as long as any AppImage can still run and function on its own without the helpers.

    In the end we are pretty pragmatic.
    What gets the job done, we will make use of.
    As long as our basic principle stays in one piece, that is  :-)


**Why is there such an inconsistent naming convention with your tools? Some go with all lowercase, some with CamelCase spelling?**

:   CamelCase names indicate a graphical user interface (GUI) applications, whereas lowercase names indicate command line tools.
    Sounds familiar to Mac users?


**Is there an AppImage AppStore?**

:   In the model that we envision, users typically get their AppImages directly from the authors ("upstream").
    So the role of an "App Store" would mainly be the role of a catalog, pointing to these AppImages.

    To facilitate this, we are buidling a crowd-sourced database of metadata describing available AppImages.
    Whoever wants to use this data for populating App Stores (like openDesktop.org) or App Centers (like NX Software Center) is free to use this data.

    Everyone can add applications by a simple pull request, containing just a one-liner with the URL of the GitHub repository or AppImage download.
    An automated sanity check will kick in to make sure that the AppImage passes our tests, and then it is ready to be merged into the catalog.

<!--
    We hear however that some Linux distributions are pondering the idea to set up an AppStore (or a department of the one they already have) which specializes in AppImages.
    What we DO have is this:

        1. A crowd-sourced aggregation of AppImage-URLs.
            We maintain it on [GitHub]().
        1. A collection of AppImage creating "recipies" which can be run as a script.
            It is also on [GitHub](https://github.com/AppImage/AppImages/tree/master/recipes).
            They have been built by Travis CI once in the past and the results were uploaded to Bintray.
            However, these are not kept current.
            They represent outdated versions of the respective app.
            Only look at them as an example of how AppImage do work.
-->


**Why don't you provide your own collection of AppImages? Why don't you run your own AppImage AppStore?**

:   We want to provide the tools to make AppImages.
    Tools to be used by the upstream software developers.
    We do not want make AppImages ourselves on a massive scale.
    One needs intimate knowledge of any application if you want to make quality assurance for it.
    We do not have that knowledge about thousands of projects out there.
    Their developers have, their users have...


**An example Linux distro which embraces AppImages?**

:   On the tools side, openSUSE embraced AppImage with the Open Build Service and their hosted openSUSE Build Service.
    Not only can you generate AppImages on their large build farm for Intel 64-bit, Intel 32-bit, ARM 64-bit, and ARM 32-bit machines.
    The resulting AppImages will also automatically be signed with a GPG key and work with AppImageUpdate binary delta updates - without you as the developer having to do anything extra or fancy.

    On the desktop, Nitrux currently is leading in terms of out-of-the-box AppImage integration, but it is still pretty young.
    Other distributions have expressed interest, particularly smaller or even niche ones who cannot afford to dream of their own ecosystems in the way Red Hat and Canonical do.

    With a project that has been in the making for over a decade, you may wonder why not more distributions have already integrated AppImage.
    Well, AppImage was designed to work without distributions having to do anything -- besides providing a working FUSE setup, which is pretty standard anyway, and providing a rock-solid and stable platform for applications..

    That being said, there is a number of issues complicating Linux as a desktop platform:
    it's simply because distributions cannot agree on some common base.
    We'd like to start a discussion around that.
    When you start to think about the "Desktop Linux Platform" rather than about different distributions silos, it becomes quite obvious that something needs to be done.
    https://github.com/AppImage/AppImageKit/wiki/Desktop-Linux-Platform-Issues
    Unfortunately, it appears that the Linux Foundation, great is it is as an institution, is apparently focusing on anything but the "Linux Desktop Platform" lately.
    I think a thoroughly crafted and followed next-generation Linux Standards Base for the desktop would help the platform greatly.


<!--
Nein, heißt NICHT "Nutrix..."
-->



<!--

***Already explained***
**Why don't you create AppImages en masse?**

:   TODO


**Benefits for Developers**

:   TODO


**Benefits for End Users**

:   TODO


**Scope**

:   TODO


**Description of Tools**

:   TODO


**History**

:   TODO


**What are you currently working on? What are you planning for future work?**

:   TODO

-->

**Does AppImage have a formal specification?**

:   https://github.com/AppImage/AppImageSpec


**Where is your Code?**

:   https://github.com/AppImage/


**Where can I get in touch with you guys online?**

:   The AppImage developers meet in the #AppImage IRC channel on Freenode, and you are welcome to join and talk to them.


<!--

**Are there known bugs with AppImages?**

:   TODO


**Where is your Bug Tracker?**

:   TODO

-->


**Do you have a Wiki?**

:   https://github.com/AppImage/AppImageKit/wiki


**Is there a centrally maintained list of available AppImages?**

:   https://appimage.github.io/apps/


**Do you have a Homepage?**

:   https://appimage.org


<!--

**Do you have a logo for your project? Do you like it? Or do you want a new and better one?**

:   TODO

-->

**Do you have "job openings"? Which areas are you in need of helping hands mostly?**

:   Always looking for volunteers, especially in the areas of desktop integration and build systems integration.
    C, C++, CMake skills required.
    Also, we are looking for GUI people, e.g., to integrate AppImageUpdate binary delta updates seamlessly.
    Qt and Gtk+ skills required.

    Last but not least, graphic artists, writers, user experience experts.
    And, since we don't have a Marketing department, we're always happy if our users talk about AppImage and share their experiences.
    You can also help the cause by asking your favorite application project to start providing AppImages, like here:
    https://bugzilla.mozilla.org/show_bug.cgi?id=1249971 - only if projects hear from many users that there is real demand will they consider making them.
    If you are a developer, you can also go out on GitHub and send Pull Requests to your favorite application projects that implement continuous builds, like here:


**Are there man pages about your stuff?**

:   Soon. Look for

    AppImage-AppDir(7),
    AppImage-AppImage(5),
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

    and ask your favorite distro to make a package of manpages  :-)

    (But SOME info of what these provide you know now already.
    However, there is more to learn, if you want to PACKAGE AppImages yourself.
    If you are only "using" AppImages, there is probably not much more you need.)


**Developers**

:   AppImage is developed by Simon Peter and a growing team of contributors.
    Simon is also the one who formulated and then pursued the packaging principle of *"One App = One File"* since over 13 years already.
    And he's not looking like he's ever willing to make any compromises on THIS one...



