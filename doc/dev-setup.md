% Setup Your Dev Tools
% Mike Gazes

# Doc history
January 20th, 2019: Start doc.
January 23rd, 2019: Visual Studio installer is like a package manager.

# Context
Epic Games supports development under Microsoft Visual Studio. The *free*
version is Microsoft Visual Studio Community 2017. This installs the necessary
build tools, but a lot of other stuff as well. That bothers a lot of people. It
bothered me.

But it turns out the Microsoft Visual Studio installer lets you
select what to install. At a minimum, you install the *core*, which is about
600MB. The core does not include a compiler. To get a compiler, you install one
of the pre-defined *workload* options, probably `Desktop development with C++`
or `Game development with C++`. You can also do a more granular install of
individual components.

To get the *leanest* set of tools, start with just the *core* and see if it has
what you need.

While not officially supported by Epic Games, community posts claim successful
set up of build tools without Microsoft Visual Studio. The most promising thread
I found was this one, describing a setup with Microsoft Visual Studio Code:
<https://answers.unrealengine.com/questions/761885/possibilities-of-coding-with-microsoft-visual-stud.html>

According to the post, Epic Games has some project-setup support for Microsoft
Visual Studio Code, a slim code editor environment that does not include any
build tools. Using Micrsoft Visual Studio Code lets me focus on the one battle
of adding a C++ compiler, so I am starting here instead of jumping straight to a
Vim setup. Once I have a working environment with Microsoft Visual Studio Code
and the Unreal Engine, I'll replace Microsoft Visual Studio Code with Vim.

I want to build my game for Windows, because all four of my computers, including
my very expensive VR rig, are running Windows as the primary OS, and it is what
my son is used to.

Up to now, my C dev work is ultimately for an embedded target. I only build on
my host Windows computer to run the test suite. This is not an *application* I
need to deploy to other computers. Anyone else running my test suite is going to
build the TestSuite.exe from source. Building the test suite on Windows makes it
sound like I already know how to compile C/C++ on Windows, but that is not the
case. I do all of this work in the POSIX environment provided by Cygwin. Such
executables do not run without the Cygwin dlls. The simplest deployment option
is for the other Windows computers to install Cygwin. I can do this for the
computers I own, but this is unrealistic for sharing my games with friends.

There are two choices: MinGW/MSYS2 and MSVC (Microsoft Visual C++).

At first glance MinGW/MSYS2 seems similar to Cygwin. MinGW stands for
Minimalist GNU for Windows, meaning it provides the GNU utilies, such as gcc,
in a Windows-compatible form. MSYS2 replaces MSYS. MSYS2 provides additional
tools for having a POSIX environment.

The difference is in the goal. Cygwin provides developers with a POSIX
environment on Windows. MSYS2 is for Linux developers to build Windows ports of
their Linux software. This site explains how MSYS2 differs from Cygwin:
<https://github.com/msys2/msys2/wiki/How-does-MSYS2-differ-from-Cygwin>

> Cygwin tries to bring a POSIX-compatible environment to Windows so that most
> software that runs on unices will build and run on Cygwin without any
> significant modifications. Cygwin provides a large collection of packages
> containing such software, and libraries for their development.
> 
> MSYS2 tries to provide an environment for building native Windows software.
> MSYS2 provides a large collection of packages containing such software, and
> libraries for their development. As a large portion of the software uses GNU
> build tools which are tightly coupled to the unix world, this environment is
> also POSIX-compatible, and is in fact based on Cygwin.

So one possible setup is for me to ignore Unreal Engine and Visual Studio
entirely, continue using Cygwin for development, but also install MSYS2 for my
final native Windows builds.

# MSVC means many things
MSVC is definitely the more industry standard choice.

What is confusing is that MSVC is an IDE, not just a set of build tools. I think
this is where the community of hobbyists struggles. Microsoft is targeting
developers used to all-in-one solutions. Linux users, or weirdos like me who use
Cygwin, are used to composable utilities, patching them together for the unique
configuration that suits their needs. Neither approach is better, it always
depends on context. Windows users unfamiliar with the composable-utility
approach see this as death by a thousand tools. For the simplicity of installing
one tool, they are willing to let Microsoft dictate how they should work.

Microsoft recognizes that developers do not want to be locked into Microsoft
Visual Studio, so they modified the Visual Studio installer. The confusing bit
is that this only appears in a blog post. It does not appear prominently
anywhere on their download page. And of course any guidance from Microsoft or
Epic Games recommends people use Microsoft Visual Studio in its entirety. The
assumption is that you do not know how to build your own project from source and
you do not already have your own editor/IDE that you want to use.

So it turns out the Visual Studio installer acts similar to the Cygwin package
manager. It is an executable you run anytime to you want to modify your existing
installation. Start with the *core*. This is only 600MB. Then as you find you
need more, run the installer and select the components you need.

- `Game development with C++` takes 5.49GB, 2.7GB if you exclude the Windows 10
  SDK
    - included:
        - Visual Studio C++ core features
        - Windows Universal C Runtime
        - Visual C++ 2017 Redistributable Update
        - VC++ 2017 version 15.x latest v141 tools
    - optional:
        - C++ profiling tools
        - Windows 10 SDK
        - Cocos
        - Unreal Engine installer
        - Visual Studio Android support for Unreal Engine
- `Desktop development with C++` takes 5.83GB, 2.99GB if you exclude the Windows
  10 SDK, and 1.1GB if you exclude all of the optional items
    - included:
        - Visual Studio C++ core features
    - optional
        - Just-In-Time debugger
        - VC++ 2017 version 15.x latest v141 tools
        - C++ profiling tools
        - Windows 10 SDK
        - Visual C++ tools for CMake
        - Visual C++ ATL for x86 and x64
        - Test Adapter for Boost.Test
        - Test Adapter for Google.Test
- `Linux development with C++` takes 5.24GB
    - included:
        - Visual Studio C++ core features
        - Windows Universal C Runtime
        - Visual C++ for Linux Development
    - optional:
        - Visual C++ tools for CMake and Linux
        - Embedded and IoT Development

You can run Visual Studio with just the *core*. This is different from Visual
Studio Code, the lean text editor/IDE.

- [ ] determine if you can compile with just this, I suspect not

The next step up would be to select the `Desktop development with C++` and
remove all of the optional components.

- [ ] determine if you can compile with just this

# MSYS2 vs MSVC
Assume for the moment that I am able to build and deploy native Windows
applications with MSYS2 or MSVC with equal success. I am not referring to the
experience of installing a binary on an unknown Windows target, not the build
experience.

MSVC feels like I'm jumping through a lot of hoops just to do what I'm used to
doing now with my Vim, gcc, and make. MSYS2 sounds like I can continue
developing as usual and just get the Windows build piece when I need it.

# Unreal Engine vs No engine at all
It will be interesting to see if Unreal recognizes g++ after I install MSYS2. If
not, I think I'll abandon Unreal for now and just stick with SDL2 and OpenGL. So
the final set of tools I need for game development is looking like this:

- IDE:
    - Cygwin
    - Vim
- Compiler:
    - Cygwin
    - gcc / clang
- Debugger:
    - Cygwin
    - gdb
- Development builds:
    - Cygwin
    - Make
    - CMake?
- libs:
    - SDL2
    - OpenGL
- Release Build:
    - MSYS2
    - gcc / clang
    - SDL2.dll (do not statically link to SDL2)

# Tasks
- [ ] install Unreal Engine and Microsoft Visual Studio Code with C++ extension
- [ ] identify a suitable C++ compiler
- [ ] invoke the compiler from Microsoft Visual Studio Code
- [ ] build a small project using Unreal Engine and Microsoft Visual Studio Code
- [ ] build the same project using Unreal Engine and Vim
- [ ] identify a unit-test framework for C++
- [ ] automate unit-testing with Vim

# Installation
## Unreal Engine
1. Create an Epic Games account.
2. Run the installer for the Epic Games Launcher.
3. Sign into the Epic Games Launcher.
4. Click on *Unreal Engine* in the Epic Games Launcher and install the engine.
   This takes a while.
5. Launch the *Unreal Engine*.


## Microsoft Visual Studio Code and C++ extension
1. Download Visual Studio Code.
2. Install Visual Studio Code.
3. Run Visual Studio Code. Click *Extensions View* on left sidebar, find `c++`,
   click *Install*, click *Reload*.

## Chocolatey and Pandoc
I use Pandoc to generate HTML documentation from markdown. Install Pandoc with
Chocolatey.

### Chocolatey
1. Launch PowerShell as an Administrator and run this command:
```powershell
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
2. Restart PowerShell as non-Admin.
3. View Chocolatey help:
```powershell
choco /? | less
```
4. Surprisingly to me, Chocolatey also runs under Cygwin. One benefit of this
   is viewing help from the Cygwin installation of Vim.
   For example, `mintty` from PowerShell to open a bash terminal, then create a
   help file for the `install` command and open it in Vim:
```bash
choco install -help > choco-install.md
vim choco-install.md
```

### Pandoc
1. Run PowerShell as Administrator and install *pandoc* with this command:
```powershell
choco install pandoc
```
2. Generate HTML documentation:
```bash
pandoc -f markdown doc/dev-setup.md -s -o doc/dev-setup.html -c pandoc.css --toc
```
Note the style is included with `-c pandoc.css` and not `-c doc/pandoc.css`,
even though `pandoc.css` is in the `doc` folder.

## MSYS2
- go to <https://www.msys2.org/>
- download the 64-bit version of MSYS2:` msys2-x86_64-YYYMMDD.exe`
- it is not a large download, less than 1GB
- the rest of these instructions are on this page as well
- install by running the downloaded .exe, this does not take up much additional
  hard drive space, so the *less than 1GB* still holds true
- run MSYS2 when installation finishes, this opens a `bash` terminal
- run this command to *update the package database and core system packages*:
```bash
pacman -Syuu
```
- as prompted, close the bash window (click on the "x") and open it up again
- keep running the `pacman -Syuu` command and restarting until there is nothing
  else to update
- I made an alias `msys` in my PowerShell profile to make it easy to launch an
  msys bash terminal from PowerShell

- to search for a library you want to install:
```bash
pacman -Ss lib_name
```
- for example, I want SDL2:
```bash
pacman -Ss SDL2
```
I get this response:
```bash
mingw32/mingw-w64-i686-SDL2 2.0.9-1
    A library for portable low-level access to a video framebuffer, audio
    output, mouse, and keyboard (Version 2) (mingw-w64)
mingw32/mingw-w64-i686-SDL2_gfx 1.0.4-1
    SDL graphics drawing primitives and other support functions (Version 2)
    (mingw-w64)
mingw32/mingw-w64-i686-SDL2_image 2.0.4-1
    A simple library to load images of various formats as SDL surfaces (Version
    2)
mingw32/mingw-w64-i686-SDL2_mixer 2.0.4-1
    A simple multi-channel audio mixer (Version 2) (mingw-w64)
mingw32/mingw-w64-i686-SDL2_net 2.0.1-1
    A small sample cross-platform networking library (Version 2) (mingw-w64)
mingw32/mingw-w64-i686-SDL2_ttf 2.0.14-1
    A library that allows you to use TrueType fonts in your SDL applications
    (Version 2) (mingw-w64)
mingw32/mingw-w64-i686-smpeg2 2.0.0-5
    SDL2 MPEG Player Library (mingw-w64)
mingw64/mingw-w64-x86_64-SDL2 2.0.9-1
    A library for portable low-level access to a video framebuffer, audio
    output, mouse, and keyboard (Version 2) (mingw-w64)
mingw64/mingw-w64-x86_64-SDL2_gfx 1.0.4-1
    SDL graphics drawing primitives and other support functions (Version 2)
    (mingw-w64)
mingw64/mingw-w64-x86_64-SDL2_image 2.0.4-1
    A simple library to load images of various formats as SDL surfaces (Version
    2)
mingw64/mingw-w64-x86_64-SDL2_mixer 2.0.4-1
    A simple multi-channel audio mixer (Version 2) (mingw-w64)
mingw64/mingw-w64-x86_64-SDL2_net 2.0.1-1
    A small sample cross-platform networking library (Version 2) (mingw-w64)
mingw64/mingw-w64-x86_64-SDL2_ttf 2.0.14-1
    A library that allows you to use TrueType fonts in your SDL applications
    (Version 2) (mingw-w64)
mingw64/mingw-w64-x86_64-smpeg2 2.0.0-5
    SDL2 MPEG Player Library (mingw-w64)
```
- anything starting with mingw is a library I can install
- I only want mingw64 libraries
```bash
pacman -Sy mingw-w64-x86_64-SDL2
```
And I get this:
```bash
:: Synchronizing package databases...
 mingw32 is up to date
 mingw64 is up to date
 msys is up to date
resolving dependencies...
looking for conflicting packages...

Packages (9) mingw-w64-x86_64-gcc-libs-8.2.1+20181214-1  mingw-w64-x86_64-gmp-6.1.2-1  mingw-w64-x86_64-libiconv-1.15-3
             mingw-w64-x86_64-libwinpthread-git-7.0.0.5273.3e5acf5d-1  mingw-w64-x86_64-mpc-1.1.0-1  mingw-w64-x86_64-mpfr-4.0.1-2
             mingw-w64-x86_64-vulkan-headers-1.1.92-1  mingw-w64-x86_64-vulkan-loader-1.1.92-1  mingw-w64-x86_64-SDL2-2.0.9-1
```
There were other `SDL2_blah` items that were not installed:
```bash
pacman -Sy mingw-w64-x86_64-SDL2_gfx mingw-w64-x86_64-SDL2_image mingw-w64-x86_64-SDL2_mixer
```
There is no wild-card option to install everything that is `SDL2_` blah, but
instructions here
<https://github.com/orlp/dev-on-windows/wiki/Installing-GCC--&-MSYS2>
show how to install everything returned by a search.

The site also explains how to install and build a library from the command-line
using `wget` to download, `tar` to extract, and `make` to build.

More detailed `pacman` examples are here:
<https://github.com/msys2/msys2/wiki/Using-packages>

## SDL2
- after the package installation I did within `MSYS2`, do I still need to do the
  next step?
- download the source and the runtime binary from here: <https://libsdl.org/download-2.0.php>


